# Tournoi

### description: Les règles officielles et le guide de démarrage du Tournoi Numerai

## Présentation du tournoi Numerai

### Introduction

Le tournoi Numerai est l'endroit où vous créez des modèles de Machine Learning sur des données financières abstraites pour prédire le marché boursier. Vous pouvez miser sur vos modèles avec la crypto-monnaie NMR pour gagner des récompenses en fonction de vos performances.

Les modèles ayant une mise sur Numerai sont combinés pour former le Meta Modèles qui contrôle le capital du fonds spéculatif Numerai sur le marché boursier mondial.

Regardez ce court-métrage pour découvrir comment tout s´articule :

{% embed url="https://www.youtube.com/watch?v=dhJnt0N497c" %}

### Résumé

1. Inscrivez-vous sur [https://numer.ai/](https://numer.ai/)
2. Téléchargez la base de données avec des données d'entraînement et des exemples de scripts
3. Construisez votre modèle et soumettez vos prédictions à Numerai
4. Miser des NMR sur vos modèles pour gagner / perdre en fonction des performances
5. Automatisez vos soumissions hebdomadaires et augmentez votre mise au fil du temps

### Données

Au cœur du Tournoi Numerai se trouve la base de données gratuites. Elle est constituée de données financières de haute qualité qui ont été nettoyées, régularisées et offusquées.

Chaque `id` correspond à un stock à une époque spécifique `era`. Les caractéristiques `features` décrivent les divers attributs quantitatifs du stock à l'époque. La cible `target` représente une mesure abstraite de la performance \~ 4 semaines dans le futur.

### Modélisation

Votre objectif est de construire un modèle pour prédire la cible future en utilisant des caractéristiques financières réelles qui correspondent au marché boursier actuel.

Voici un exemple de base utilisant XGBoost sous Python. Nous entraînons le modèle en utilisant les données historiques et faisons des prédictions sur les données réelles du tournoi.

```python
from numerapi import NumerAPI
import pandas as pd
import lightgbm as lgb

napi = NumerAPI()
napi.download_dataset("v5.0/train.parquet")
training_data = pd.read_parquet("v5.0/tra.parquet")

features = [f for f in training_data.columns if "feature" in f]

model = lgb.LGBMRegressor(
      n_estimators=2000,
      learning_rate=0.01,
      max_depth=5,
      num_leaves=2 ** 5,
      colsample_bytree=0.1
)
model.fit(
      training_data[features],
      training_data["target"]
)
```

Vous pouvez utiliser n'importe quel langage ou structure pour créer votre modèle. Consultez nos [scripts](https://github.com/numerai/example-scripts) pour d'autres exemples de modèles et de cahiers de recherche exploratoire. Rendez-vous sur le [forum](https://forum.numer.ai) pour découvrir les derniers sujets de recherche de l'équipe et de la communauté.

### Soumissions

Chaque `samedi 18h00 UTC`, un nouveau `round` s'ouvre et de nouvelles données de tournoi sont publiées. Pour participer, vous devez soumettre vos dernières prévisions avant la date limite du `lundi 14h30 UTC`.

{% hint style="info" %}
Vous devez soumettre vos predictions **chaque semaine** pour participer au Tournoi Numerai!
{% endhint %}

Vous pouvez télécharger les dernières données et soumettre vos prédictions manuellement à l'aide du site Web.

Vous pouvez également vous connecter directement à notre [API GraphQL](https://api-tournament.numer.ai/) ou via les clients api officiels [Python](https://github.com/uuazed/numerapi) et [R](https://github.com/Omni-Analytics-Group/Rnumerai). Voici un exemple de base utilisant le client api Python.

```python
import numerapi
napi = numerapi.NumerAPI("public_id", "secret_key")

# download data
napi.download_current_dataset(unzip=True)

# upload predictions
napi.upload_predictions("predictions.csv", model_id="model_id")
```

Vous pouvez également déployer votre modèle dans le cloud et automatiser l'ensemble de votre flux de soumission hebdomadaire avec la structure [Numerai Compute](https://github.com/numerai/numerai-cli).

```bash
# setup your cloud infrastructure
numerai setup

# copy the example model
numerai docker copy-example

# deploy the example model 
numerai docker deploy
```

### Diagnostique

À chaque soumission, nous vous montrerons des métriques de diagnostic pour vous aider à comprendre les performances et les caractéristiques de risque de votre modèle au cours des ères de validation historiques.

{% hint style="warning" %}
L'utilisation répétée de cet outil d'évaluation historique conduira rapidement à un «overfitting». Traitez les diagnostics uniquement comme une vérification finale dans votre processus de recherche de modèle.
{% endhint %}

En savoir plus sur le diagnostic de modèle dans le [forum](https://forum.numer.ai/t/model-diagnostics-update/902).

### Notation

Vous êtes principalement noté sur la corrélation (`corr`) entre vos prédictions et les cibles. Plus la corrélation est élevée, mieux c'est.

```python
# method='first' breaks ties based on order in array
ranked_predictions = predictions.rank(pct=True, method="first")
correlation = np.corrcoef(labels, ranked_predictions)[0, 1]
```

Vous êtes également noté sur votre [contribution au méta-modèle](https://app.gitbook.com/s/-LmGruQ\_-ZYj9XMQUd5x/numerai-tournament/scoring/meta-model-contribution-mmc) (`mmc`) et la [corrélation neutre](https://app.gitbook.com/s/-LmGruQ\_-ZYj9XMQUd5x/numerai-tournament/scoring/feature-neutral-correlation) (`fnc`). Plus la contribution du méta-modèle et la corrélation neutre des caractéristiques sont élevées, mieux c'est.

Chaque soumission sera notée sur la durée du tour d'environ 4 semaines. Les soumissions recevront leur premier score à partir du jeudi après la date limite du lundi et le score final le mercredi 4 semaines plus tard pour un total de 20 scores.

Puisqu'un tour prend environ 4 semaines pour être résolu, si vous soumettez de nouvelles prédictions chaque semaine, vous recevrez plusieurs scores (jusqu' à 4) qui se chevauchent chaque jour des 4 tours en cours.

Les scores réels de votre modèle peuvent être consultés publiquement sur sa page de profil de modèle. Voici un exemple des scores finaux d'un modèle au cours des 20 derniers tours.

Vous pouvez également zoomer sur un tour spécifique et voir les 20 scores quotidiens du tour.

### Miser

Vous pouvez éventuellement `miser` des [NMR](https://www.coinbase.com/price/numeraire) sur votre modèle pour gagner ou perdre en fonction de vos scores en `corr` et / ou `mmc`. Vous ne pouvez pas miser sur vos scores `fnc`.

Miser signifie bloquer des NMR dans un [smart contract](https://github.com/numerai/tournament-contracts) sur la blockchain [Ethereum](https://ethereum.org/en/whitepaper/). Pour la durée de la mise, Numerai a la permission d'ajouter ou retirer des paiements à partir des NMR bloqués.

Vous pouvez gérer votre mise sur le site Web. Lorsque vous augmentez votre mise, les NMR sont transférés de votre portefeuille au contrat de mise. Lorsque vous diminuez votre mise, les NMR sont transférés du contrat de mise vers votre portefeuille après un délai d'environ 4 semaines. Vous pouvez également changer votre type de mise, qui détermine les scores (`corr` et/ou `mmc`) sur lesquels vous voulez miser.

### Paiements

Les paiements sont fonction de la valeur de votre mise et des scores. Plus la valeur de votre mise est élevée et plus vos scores sont élevés, plus vous gagnerez. Si vous avez un score négatif, une partie de votre mise sera perdue. Les paiements sont limités à ±25% de la valeur de la mise par tour.

```python
payout = stake_value * payout_factor * (corr * corr_multiplier + mmc * mmc_multiplier)
```

La `stake_value` est la valeur de votre mise le premier jeudi (jour de score) du tour.

Le `payout_factor` est un nombre qui évolue avec les NMR totaux misés sur tous les modèles du tournoi. Plus les NMR totaux misés sont au-delà du seuil de 300K, plus le facteur de paiement diminue.

Le`corr_multiplier` et `mmc_multiplier` sont configurables par vous pour contrôler votre exposition à chaque score. Vous disposez des options multiplicateur suivantes.

| **options multiplicateur de corr** | **options multiplicateur de mmc** |
| ---------------------------------- | --------------------------------- |
| 1.0x                               | 0.0x, 0.5x, 1.0x, 2.0x            |

{% hint style="info" %}
La courbe des facteurs de paiement et les options de multiplicateur disponibles peuvent être et seront mises à jour par Numerai à l'avenir en même temps que des révisions majeures du tournoi.
{% endhint %}

Voici quelques exemples de calculs de paiement. Les 2 premiers exemples montrent l'impact de l'ajustement des multiplicateurs de score. Le 3ème exemple montre comment un score négatif peut provoquer une perte. Le 4ème exemple montre comment le paiement est plafonné à ±25% de la valeur de la mise.

| mise    | facteur de paiement | corr  | multiplicateur corr | mmc   | multiplicateur mmc | paiement  |
| ------- | ------------------- | ----- | ------------------- | ----- | ------------------ | --------- |
| 100 NMR | 0.8                 | 0.02  | 1.0x                | 0.002 | 2.0x               | 1.92 NMR  |
| 100 NMR | 0.8                 | 0.02  | 1.0x                | 0.002 | 0.0x               | 1.6 NMR   |
| 100 NMR | 0.8                 | -0.03 | 1.0x                | 0.002 | 0.5x               | -2.32 NMR |
| 100 NMR | 0.8                 | 0.15  | 1.0x                | 0.1   | 2.0                | 25 NMR    |

Avec chaque score quotidien, une nouvelle mise à jour quotidienne de votre paiement est également calculée. Ces paiements quotidiens ne sont qu´à titre indicatif car seul le paiement final d'un tour compte. Vous pouvez suivre vos paiements quotidiens avec l'application [Numerai Payouts](https://docs.numer.ai/community-content/community-built-products#numerai-payouts) créée par la communauté..

Les paiements finaux sont reversés automatiquement dans votre mise à la fin du tour(Wednesday). Lorsque vous commencez à miser, la valeur de votre mise restera constante pendant les 4 premiers tours. Ensuite, la valeur de votre mise sera mise à jour chaque semaine en fonction de votre paiement du tour il y a 4 semaines.

La valeur de votre mise augmentera tant que vous continuerez à avoir des scores positifs. Voici quelques exemples de projections de paiement en supposant que le modèle obtienne des scores positifs fixes chaque semaine pendant 52 semaines.

### Classement

Le classement peut être trié en fonction de le `corr`, `mmc` et `fnc` du modèle.

Gardez un œil sur le classement pour voir comment vos modèles se comparent aux autres modèles en termes de performances et de rendements de la mise.

### Support

Nous sommes ici pour vous aider.

Retrouvez-nous sur [Discord](https://discord.gg/n2YgnHEM) pour toute question, besoin de support et commentaires !
