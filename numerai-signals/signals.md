# Signals

### description: Les règles officielles et le guide de démarrage de Numerai Signals

## Présentation de Numerai Signals

[Numerai Signals](https://signals.numer.ai) vous permet de soumettre vos propres signaux boursiers et de découvrir à quel point ils sont originaux par rapport à tous les autres signaux sur Numerai. Vous pouvez miser sur vos signaux avec la crypto-monnaie NMR pour gagner des récompenses. Les meilleurs signaux les plus originaux sont utilisés dans le fond d´investissement de Numerai.

Numerai Signals fait partie du plan directeur Numerai visant à créer le dernier fonds spéculatif au monde. Lisez l'article [Medium](https://medium.com/numerai/building-the-last-hedge-fund-introducing-numerai-signals-12de26dfa69c) et regardez [le court-métrage ](https://youtu.be/GWeC2PK4yXQ) pour en savoir plus sur la façon dont tout cela s'articule.

### Résumé

1. Inscrivez-vous à [Numerai Signals](https://signals.numer.ai) ou connectez-vous avec votre compte de tournoi Numerai existant.
2. Téléchargez votre propre signal sur l'univers boursier de Numerai pour recevoir des diagnostics de performance, de risque et de rentabilité sur la partie historique de votre signal.
3. Miser vous NMR sur la partie en direct de votre signal pour gagner ou perdre des NMR en fonction de vos performances par rapport aux objectifs customisés de Numerai.
4. Automatisez le téléchargement hebdomadaire de votre signal en vous connectant directement à notre API et augmentez le montant de votre mise au fil du temps.

### Qu´est ce qui représente des signaux boursiers ?

Les signaux boursiers sont des sources de données numériques sur les actions utilisées par les fonds d´investissement quantitatifs comme Numerai pour construire des portefeuilles.

Des exemples de signaux boursiers comprennent :

* [Signaux fondamentaux](https://www.investopedia.com/terms/f/fundamentalanalysis.asp)  ([ratio P/E](https://www.investopedia.com/terms/p/price-earningsratio.asp), [rendement du dividende](https://www.investopedia.com/terms/d/dividendyield.asp), [notations des analystes](https://www.investopedia.com/terms/r/rating.asp))
* [Signaux techniques ](https://www.investopedia.com/terms/t/technicalindicator.asp) ([MACD](https://www.investopedia.com/terms/m/macd.asp), [RSI](https://www.investopedia.com/terms/r/rsi.asp), [MFI](https://www.investopedia.com/terms/m/mfi.asp))
* [Signaux de données alternatifs ](https://en.wikipedia.org/wiki/Alternative\_data\_\(finance\)) ([transactions par carte de crédit](https://secondmeasure.com/), [images satellite](https://www.theatlantic.com/magazine/archive/2019/05/stock-value-satellite-images-investing/586009/), [sentiment des médias sociaux](https://www.swaggystocks.com/dashboard/wallstreetbets/realtime))
* [Signaux mixtes ](https://www.investopedia.com/terms/m/multifactor-model.asp) ([facteurs de risque Barra](https://www.investopedia.com/terms/b/barra-risk-factor-analysis.asp), [facteurs Fama-French](https://www.investopedia.com/terms/f/famaandfrenchthreefactormodel.asp))

Alors que les données sous-jacentes utilisées pour générer ces signaux peuvent être très différentes (données financières vérifiées vs images de parkings), les signaux eux-mêmes ont tous le même format de base - une liste de boursiers chacun avec une valeur numérique associée.

### Création de signaux

#### Données et outils

Pour créer votre propre signal, vous devrez d'abord acquérir des données boursières.

{% hint style="info" %}
Si vous êtes un «data scientist» sans données boursières considérez plutôt participez au [Tournoi Numerai](https://numer.ai/).
{% endhint %}

Si vous n'avez pas déjà accès aux données boursières, il existe un certain nombre de fournisseurs de données gratuits ou bon marché sur Internet tels que [Yahoo Finance](https://finance.yahoo.com/), [Quandl](https://www.quandl.com/), et [Koyfin](https://www.koyfin.com/).

Il existe également des plates-formes qui facilitent la création de signaux tels que [QuantConnect](https://www.quantconnect.com/), et [Alpaca](https://alpaca.markets/).

Consultez cette discussion sur le [Forum](https://forum.numer.ai/t/free-or-cheap-data-for-erasure-numerai-quant/350) pour obtenir une liste de sources de données, plateformes et des outils populaires utilisés par notre communauté.

{% hint style="success" %}
Trouver des données uniques et différenciantes est essentiel pour créer des signaux originaux.
{% endhint %}

#### Univers

L'univers boursier Numerai Signals couvre à peu près les 5000 plus grandes valeurs du monde. L'univers est mis à jour chaque semaine, mais en général, seules quelques actions à faible volume entreront ou sortiront au cours d'une semaine donnée. Vous pouvez voir le dernier univers en téléchargeant le [dernier univers](https://numerai-signals-public-data.s3-us-west-2.amazonaws.com/universe/latest.csv).

Vous pouvez voir l'univers historique en téléchargeant les [cibles historiques](https://numerai-signals-public-data.s3-us-west-2.amazonaws.com/signals\_train\_val\_bbg.csv). Ce fichier contient des données jusqu'au troisième vendredi le plus récent, en raison des cycles de signaux résolus deux mercredis (11 days) après leur ouverture. Au cours de la quatrième semaine du mois, les données du premier vendredi du mois seront la date avec les données disponibles les plus récentes.

#### Soumissions

Lorsque vous soumettez un signal à Numerai Signals, vous devez inclure au moins deux colonnes :

* Une colonne `cusip`, `sedol`, ou `ticker` - les valeurs doivent être des tickers valides associés au type de ticker dans l'en-tête.    &#x20;
* Une colonne `signal` - les valeurs doivent être comprises entre 0 et 1 (exclusif).

De plus, pour qu'une soumission soit valide :

* Il doit y avoir au moins 10 lignes avec des prédictions pour les tickers dans l'univers boursier Signals pour la période `live` actuelle.
* Un ticker ne peut pas apparaître plus d'une fois dans la période de temps `live` actuelle.

Les soumissions avec seulement deux colonnes sont supposées correspondre à la période de temps `live` actuelle.

Vous pouvez également télécharger votre signal sur une période de `validation` historique pour recevoir des mesures de diagnostic sur vos performances, vos risques et vos revenus potentiels. La période de validation s'étend sur `374` semaines de `20130104` à `20200228`.

Les soumissions qui incluent la période de `validation` doivent inclure deux colonnes supplémentaires :

* Une colonne `friday_date` - les valeurs doivent être des vendredis car les périodes de la semaine commencent le vendredi dans Numerai Signals. &#x20;
* Une colonne  `data_type` - les valeurs ne peuvent être que live ou validation. Les lignes avec `data_type` de type `live` doivent contenir la date du vendredi le plus récent.&#x20;

Téléchargez le dernier exemple de soumission [ici](https://numerai-signals-public-data.s3-us-west-2.amazonaws.com/example\_signal/latest.csv).

#### Diagnostique

Une fois votre soumission acceptée, elle sera mise en file d'attente pour les diagnostics. Cela prend généralement 10 à 15 minutes selon le nombre de semaines et de tickers qui couvrent votre soumission.

Ces diagnostics vous servent de guide pour estimer si votre signal est suffisamment bon pour valoir la peine d'être misé. Il est important de noter que les signaux avec des diagnostics solides au cours de la période de `validation` historique peuvent ne pas obtenir de bons résultats dans les périodes `live` actuelles ou futures.

{% hint style="warning" %}
L'utilisation répétée de cet outil d'évaluation historique conduira rapidement à un «overfitting». Traitez les diagnostics uniquement comme une vérification finale de votre processus de création de signaux.
{% endhint %}

Toutes les cibles historiques utilisées pour calculer les diagnostics sont disponibles [ici](https://numerai-signals-public-data.s3-us-west-2.amazonaws.com/signals\_train\_val\_bbg.csv).

#### API et automatisation

{% hint style="info" %}
Vous devez soumettre votre signal le plus récent à Numerai chaque semaine
{% endhint %}

Vous pouvez automatiser votre flux de travail de soumission en utilisant[Numerai Compute](https://docs.numer.ai/tournament/compute) et notre [API GraphQL](https://api-tournament.numer.ai/) ou le client python officiel.

{% embed url="https://github.com/uuazed/numerapi#usage-example---numerai-signals" %}

### évaluation du signal

#### Neutralisation

Numerai a une variété de signaux existants. Nos signaux existants incluent les facteurs Barra (comme la taille, la valeur, le momentum, etc.) les facteurs de risque pays et secteur, ainsi que les caractéristiques des actions personnalisées.

{% hint style="info" %}
**Définition**: Un signal ou une cible est considéré comme «neutralisé» après que Numerai l'a transformé pour avoir une corrélation nulle avec l'un des signaux existants de Numerai tels que les facteurs Barra, le pays, les facteurs sectoriels et d'autres caractéristiques de stock customisées.
{% endhint %}

Chaque signal téléchargé sur Numerai Signals est neutralisé avant d'être évalué. Le but de la neutralisation est d'isoler la composante originale ou orthogonale du signal qui n'est pas déjà présente dans les signaux connus.

{% hint style="info" %}
Si vous soumettez une simple combinaison linéaire de quelques signaux bien connus, il y aura peu voire pas de composante orthogonale après la neutralisation.
{% endhint %}

Les cibles utilisées pour évaluer les signaux sont également neutralisées. Les cibles sont en effet le «rendement spécifique» ou le «rendement résiduel» customisé de Numerai.

Les données utilisées pour effectuer la neutralisation ne sont pas fournies, ce qui signifie que le processus est une «boîte noire». Cependant, vous pouvez utiliser les diagnostics historiques de votre signal pour estimer l'impact de la neutralisation sur votre signal dans le futur, bien qu'il soit important de noter que les signaux avec des scores élevés au cours de la période historique peuvent ne pas bien performer dans un cycle présent ou futur.

Le code utilisé pour implémenter la neutralisation est open source. Vous pouvez en savoir plus sur le processus de neutralisation dans cet exemple :

{% embed url="https://github.com/numerai/example-scripts/blob/master/SignalsScoringExample.ipynb" %}

Ou consultez le forum pour comprendre les implications plus larges de l'exposition et de la neutralisation des `features`.

{% embed url="https://forum.numer.ai/t/model-diagnostics-feature-exposure/899" %}

Les signaux ayant une corrélation très élevée avec les rendements boursiers ultérieurs peuvent avoir de très mauvais résultats sur Numerai Signals et les signaux avec une faible corrélation avec les rendements ultérieurs peuvent obtenir de bons résultats.

En d'autres termes, les «bons» signaux avec une forte valeur prédictive lorsqu'ils sont considérés seuls peuvent avoir un mauvais score sur Numerai Signals. Cela met en évidence l'aspect unique clé de Signals: Numerai Signals ne consiste pas à prédire les rendements boursiers, il s'agit de trouver des signaux originaux que Numerai ne possède pas déjà.

#### **Retours Cibles Neutralisés sur Six Jours**

Les signaux sont évalués par rapport à un objectif customisé «boîte noire» créé par Numerai. Cet objectif est basé sur des rendements ultérieurs neutralisés sur 6 jours (sans tenir compte des 2 premiers jours).

La raison pour laquelle les signaux sont évalués sur un horizon de 6 jours (moins les 2 premiers jours) est que les signaux qui ne fonctionnent que sur des horizons de temps courts sont impossibles à mettre en œuvre pour les grands fonds d´investissement. Par exemple, même si un signal peut prédire avec précision le rendement d'une heure des actions, il n'est pas très utile s'il faut 24 heures à un fond d´investissement pour investir pleinement dans cette position. Les signaux les plus utiles pour les grands fonds d´investissement ont un pouvoir prédictif sur un horizon de temps long, également connu sous le nom de «low alpha decay».

Pour plus d'informations sur les jours de marché exacts qui composent les 6 jours de retours neutralisés ultérieurs, consultez la section suivante sur les dates et délais.

#### Notation

Avant la notation, les signaux sont d'abord classés entre \[0, 1] puis neutralisés. Enfin, le score est calculé en prenant la corrélation de Spearman entre le signal neutralisé et la cible. Ce score est simplement appelé `corr` dans ce document et sur le site Web.

En neutralisant votre signal avant de le noter, Numerai l'aligne sur la cible ce qui améliore ses performances par rapport à la cible. Puisque la cible est également neutralisée, l'étape de neutralisation optimise efficacement votre signal pour de meilleures performances sans que Numerai ait à fournir les données utilisées pour la neutralisation.

Par exemple, si votre signal n'est pas neutralisé face aux risques pays, Numerai Signals neutralisera votre signal face aux risques pays avant de le noter afin que vous puissiez vous concentrer sur la création d'un signal original sans avoir à vous soucier de la neutralisation du risque pays.

Si vous n'avez que des signaux sur un sous-ensemble de l'univers (par exemple, uniquement des signaux sur les actions américaines), vous avez toujours la possibilité de les soumettre à Signals et bien performer. Pour chaque action de l'univers où vous avez des signaux manquants, Numerai les remplira automatiquement avec la valeur médiane après le classement du signal.

#### Contribution au méta-modèle

Si `corr` est une mesure de la corrélation de votre signal avec une cible neutralisée par tous les signaux connus de Numerai, la contribution au méta-modèle (MMC) est une mesure de la corrélation de votre signal avec une cible neutralisée par tous les signaux connus de Numerai et tous les autres signaux implantés sur les signaux numériques. Ce score est simplement appelé `mmc` dans ce document et sur le site Web.

Le `mmc` d'un signal est calculé en construisant d'abord un signal spécial appelé le méta-modèle des signaux, qui est défini comme la moyenne pondérée par la mise de tous les signaux (classés et neutralisés) sur Numerai Signals pour un tour donné. Le `mmc` d'un signal est la corrélation du signal avec la cible après avoir été neutralisé par le méta-modèle des signaux.

{% hint style="success" %}
Une MMC élevée et régulière sur Signals est doublement impressionnant car cela signifie que votre signal a un avantage sur toutes les données de Numerai ainsi que sur la combinaison de tous les autres signaux sur Numerai Signals.
{% endhint %}

MMC est un concept tiré du tournoi principal Numerai et le système de notation est très similaire. Voir la section [contribution au méta-modèle ](https://docs.numer.ai/tournament/metamodel-contribution) dans la documentation du Tournoi Numerai pour plus de détails sur la façon dont nous calculons MMC sur Numerai..

Notez que le calcul du MMC de Numerai Signals est complètement séparé de celui du Tournoi Numerai. Plus précisément, seules les soumissions à Numerai Signals sont utilisées pour construire le méta-modèle de Signals.

### Miser <a href="#staking" id="staking"></a>

Vous pouvez éventuellement `miser` des [NMR](https://www.coinbase.com/price/numeraire) sur votre modèle pour gagner ou perdre en fonction de vos scores `corr` et / ou `mmc`.

Miser signifie bloquer des NMR dans un [smart contract](https://github.com/numerai/tournament-contracts) sur la blockchain [Ethereum](https://ethereum.org/en/whitepaper/). Pour la durée de la mise, Numerai a la permission d'ajouter ou supprimer des paiements sur la base des NMR bloqués.

{% hint style="danger" %}
Il est important de noter que l'opportunité de miser votre signal **n'est pas** une offre de Numerai de participer à un contrat d'investissement, un titre, un swap basé sur le rendement d'éventuels actifs financiers, une participation dans le fond de Numerai, ou dans Numerai lui-même ou tout frais que nous récupérons. Les paiements seront effectués à notre discrétion, sur la base d'une cible de boîte noire qui ne sera pas divulguée aux utilisateurs. Fondamentalement, Numerai Signals est un service proposé par Numerai qui permet aux utilisateurs d'évaluer la valeur de leurs signaux, en utilisant la mise de NMR comme moyen de valider les signaux «réels». En retour, Numerai utilise les signaux jalonnés et les données associées dans le fond d´investissement Numerai. Les utilisateurs ayant des attentes différentes ne doivent pas miser sur leurs signaux. **Veuillez lire nos** [**Conditions de Service**](https://numer.ai/terms) **pour plus d'informations.**
{% endhint %}

Vous pouvez gérer votre mise sur le site Web. Lorsque vous augmentez votre mise, les NMR sont transférés de votre portefeuille vers un contrat de mise. Lorsque vous diminuez votre mise, les RMN sont transférés du contrat de mise vers votre portefeuille après un délai d'environ 4 semaines. Vous pouvez également changer votre type de mise, qui détermine les scores (`corr` et / ou `mmc`) sur lesquels vous voulez miser.

![](https://gblobscdn.gitbook.com/assets%2F-LmGruQ\_-ZYj9XMQUd5x%2F-MTwWeGztnW6NaH6Sd\_A%2F-MTxK8xvV36McXIClWAt%2Fimage.png?alt=media\&token=aea91c60-7079-439b-bbd6-f64e9d8c26d7)

### Paiements

#### Fonction de paiement

Les paiements sont fonction de la valeur de votre mise et des scores. Plus la valeur de votre mise est élevée et plus vos scores sont élevés, plus vous gagnerez. Si vous avez un score négatif, une partie de votre mise sera perdue. Les paiements sont limités à ± 25% de la valeur de la mise par tour.

La `stake_value` est la valeur de votre mise le premier vendredi (jour de score) du tour.

Le `payout_factor` est un nombre qui évolue avec les NMR totaux misés sur l´ensemble des modèles du tournoi. Plus les NMR totaux misés dépassent le seuil de 100K est élevé, plus le facteur de paiement est bas.

Le `corr_multiplier` et `mmc_multiplier` sont configurés par vous pour contrôler votre exposition à chaque score. Vous disposez des options de multiplicateur suivantes.

| **options de multiplicateur corr** | **options de multiplicateur mmc** |
| ---------------------------------- | --------------------------------- |
| 2.0x                               | 0.0x, 0.5x, 1.0x, 2.0x            |

{% hint style="info" %}
La courbe des facteurs de paiement et les options de multiplicateur disponibles peuvent être mises à jour et seront mises à jour par Numerai à l'avenir en même temps que les principales révisions des tournois.
{% endhint %}

Voici quelques exemples de calculs de paiement. Les 2 premiers exemples montrent l'impact de l'ajustement des multiplicateurs de score. Le 3ème exemple montre comment un score négatif peut provoquer une brûlure. Le quatrième exemple montre comment le paiement est plafonné à ± 25% de la valeur de la mise.

| mise    | facteur de paiement | corr  | multiplicateur corr | mmc   | multiplicateur mmc | paiement |
| ------- | ------------------- | ----- | ------------------- | ----- | ------------------ | -------- |
| 100 NMR | 0.8                 | 0.02  | 2.0x                | 0.002 | 2.0x               | 3.52 NMR |
| 100 NMR | 0.8                 | 0.02  | 2.0x                | 0.002 | 0.0x               | 3.2 NMR  |
| 100 NMR | 0.8                 | -0.03 | 2.0x                | 0.002 | 0.5x               | -4.8 NMR |
| 100 NMR | 0.8                 | 0.15  | 2.0x                | 0.07  | 2.0                | 25 NMR   |

#### Croissance de la mise

Avec chaque score quotidien, une nouvelle mise à jour quotidienne de votre paiement est également calculée. Ces paiements quotidiens ne qu´ à titre indicatif et seul le paiement final d'un tour compte. Les paiements finaux sont reversés dans votre mise à la fin du tour (mercredi).

La valeur de votre mise augmentera tant que vous continuerez à avoir des scores positifs. Voici quelques exemples de projections de paiement en supposant que le modèle obtienne des scores positifs constants chaque semaine pendant 52 semaines.

### Dates et délais

#### Date des données vs date d'entrée en vigueur

Il existe deux types de dates dans Numerai Signals

* `data_date` - dates correspondant aux données boursières sous-jacentes. Toutes les `data_dates` font référence à la clôture du marché à cette date et n'incluent pas d'heure. Par exemple, les valeurs de la colonne `friday_date` des soumissions sont de type `data_date`.
* `effective_date` - dates correspondant aux actions ou événements qui ont lieu sur Numerai Signals et peuvent inclure une heure qui est toujours spécifiée en UTC. Il y a généralement un délai entre `data_date` et `effective_date` en raison des fuseaux horaires et du temps nécessaire au traitement des données boursières. Sauf indication contraire, toutes les dates mentionnées sur le site et dans ce document sont de type `effective_date`.&#x20;

#### Tours

Les soumissions, mises, scores et les paiements sont regroupés en `tours` numérotées pour en faciliter les échanges.

Un nouveau `tour` commence tous les `samedis - 18h00 UTC`. La date limite pour les soumissions et le jalonnement est fixée au `lundi - 14h30 UTC`. Les soumissions tardives ne seront pas notées et ne compteront pas pour les paiements. Les changements de mise effectués après la date limite s'appliqueront au tour suivant.

Les soumissions à temps seront notées et les paiements en attente sont calculés le vendredi, samedi, mardi et mercredi. Les valeur mise sont verrouillées d'ici vendredi lors de la "sélection de mise", ce qui signifie que les paiements du tour précédent sont automatiquement ajoutés à la mise du tour suivant. Le score et le paiement du mercredi sont considérés comme le score final et le paiement du tour.

L'univers du tour est défini par la `data_date` du vendredi précédent. Les 4 jours de notation et de paiement sont basés sur des retours neutralisés `3 jours-2 jours`, `4 jours-2 jours`, `5 jours-2 jours` et `6 jours-2 jours`. Il y a un décalage de 2 jours entre la fermeture du marché pendant une journée et le moment où les données deviennent disponibles pour la notation. Par exemple, les rendements neutralisés `6 jours-2 jours` sont jusqu'à la clôture du marché du lundi, mais ne sont disponibles que mercredi.

### Classement

Le classement peut être trié en fonction de la réputation du `corr`, `corr20` et `mmc` du modèle. La [Reputation](https://docs.numer.ai/tournament/reputation) est la moyenne pondérée d'une métrique donnée au cours des 20 dernières rondes.

Gardez un œil sur le classement pour voir comment vos modèles se comparent aux autres modèles en termes de performances et de rendements de la mise.

### Aide

Nous sommes ici pour aider.

Retrouvez-nous sur [RocketChat](https://community.numer.ai) pour toute question, besoin d'assistance et commentaire !
