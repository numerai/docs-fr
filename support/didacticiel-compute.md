# Didacticiel Compute

### description: Ce didacticiel vous aide pour migrer Compute vers la version 0.3.0 de la CLI

## Tutoriel de Compute

[Regardez la vidéo sur YouTube](https://youtu.be/-3y0N7fqfOI).

IMPORTANT! Après avoir installé la dernière version de numerai-cli, utilisez l'indicateur `--help` à tout moment si vous ne savez pas quoi faire.

![](https://lh4.googleusercontent.com/Z2tOBeUHGNwCv7OCqhiPwEOBQPZxfgQu7vF5hGADFhpw6xKWOa4UaO8EKbCWKveJ4aRgcMHC8OLh-TJvf7qK8epgzAoR9gnNucFAtaUUgv5mWgUsYjsgty-lGj2hgNWklDZy3GwK)

\[00:30] Ouvrez votre interpréteur de commandes et tapez `pip install --upgrade numerai-cli` puis appuyez sur ENTRER.

![](https://lh3.googleusercontent.com/HRyRFQO\_wqSoepe037Qs7nFE0oCtqZdKx4t6sKKSab88pLBaUB1rp5890Ajmbd8F\_H\_4dkO17D\_L9YOWFDtsIHzNj39hVXDVdSptsZpgFiPFuB8PLCuuDoL-ul44ZPfOtnsBNUPg)

\[01:09] Vérifiez les options disponibles pour les cœurs de processeur et la RAM en tapant `numerai list-constants` puis appuyez sur ENTER

![](https://lh3.googleusercontent.com/OmyFE37\_rGmPSyXfRUmkE8pmPrY7FbnRwqnLFDOoE6FEc8qMU0HpflRjuWVtPPg6jMuricsJpLmKAuB\_qyWtTlklcYBrtmbiwuw6vVlmbscz8htV8hgAqpYdtieYGblJBV-ia\_1s)

\[02:00] Vous devez faire une mise à jour à partir du répertoire de votre précédente installation de Compute. Certaines personnes ont utilisé 'example-numerai', vous devrez donc diriger votre interpréteur de commandes vers ce répertoire. Dans mon cas, Compute a été installé dans C:\Users\Jon\example-numerai donc je tape: cd C:\Users\Jon\example-numerai

![](https://lh3.googleusercontent.com/tYZ\_5X\_QRM4XWKpN1A533TjeeCykhv2ESlvLERXRvZ\_J69jxk8j13sx5jP-SyFcXx7QyCNgsq7pdcfkeSGDenUQwRjI01kq-h1lcBlqMxdIShHI7MEbitcuf0A5ukSmfWFvTKEac)

\[02:27] Ensuite, tapez `numerai upgrade` et appuyez sur ENTER

![](https://lh6.googleusercontent.com/jefXvZopiVR5PxvRqrQpog3WbsyiQITlaJdDY2wdCE1VmuT-8ilmAIYZedOeWSbfDborilxs0w9hczIftRzhBgx4cfSD5a6S9SAQYMVVZhriAe-6SA60cbsWoOs-AicvBRfvKifK)

\[03:08] Il vous sera demandé si vous souhaitez continuer. Tapez «y» et appuyez sur ENTER.

![](https://lh4.googleusercontent.com/m871qIYIErv-3pwzGkqcCDHNawfsPiU2ABCpfYqs34x6E4DAtjDopacmoXjRwccFYXVWYe4i3Romb1lLspUeclzAFMn4BSO-NAbXGcXK-Y4en-bFif2afw\_J8\_uStvGlSBaI55jT)

\[07:27] Après avoir examiné les options disponibles pour configurer le nœud numerai `--help` nous procédons en indiquant à numerai-cli la taille prédéfinie à utiliser pour notre nœud et le chemin d'accès au dossier contenant notre modèle. Pour cet exemple, je tape numerai node config -s mem-lg -p C:\Users\Jon\ex-nomi et appui sur ENTRER

Lorsque vous êtes invité à entrer le nom du modèle, assurez-vous d'identifier le modèle correct, car le webhook sera enregistré sous ce nom de modèle.

Tapez `votre nom de mod&egrave;le` et appuyez sur ENTRER. Pour cet exemple, j'ai tapé `twitch_example_nomi` et appuyé sur ENTRER

![](https://lh5.googleusercontent.com/suOSIpGR6\_Gk9CIgrmRdQj0RWTgP89Y-gwjz6oI9TpSXEhMTqpm08C7LeOhGm48q\_GOho8uFD3gTLHAI-M2P2QGNqPXd5PZPkuG9zi1eZe2fKzkDmTLSouNagcrO7RQpEPcWSIzw)

\[08:48] Après le message de confirmation d'installation, numerai-cli nous recommande de déployer et de tester le nœud. Testez d'abord localement. Faites-le en tapant `numerai node test -l -v` et appuyez sur ENTRER

![](https://lh3.googleusercontent.com/H1a0OCVFGzb2NvcIu-IFXs3P-VVB9C1f9YAcFH3XiVbsmBjNM3FWs\_mjBECPsNCXwJVk-REOSRgTkWh3iZnjExsTFaa-YuTVOc52gmDD6pFUwbebqnrKTGL\_oweeFWG0opzE3IpJ)

\[12:00] Si votre test local a réussi, déployez votre mode sur AWS. Faites-le en tapant `numerai node deploy` et appuyez sur ENTRER. Tapez `votre nom de mod&egrave;le` et appuyez sur ENTRER.

![](https://lh4.googleusercontent.com/-7h0rRCAWppXwC7-cbM9msmJ5iQcmHAz7xUPhPRn0j1FpTPXJ88ffVVqz3zpeLx9jTLnciMynAiMvy1mtKP89MXjsmw\_ZyuCtLFTM1CiF051RpRMyMFN5xnGrWf7DSEpgkOt9rWL)

\[12:50] Une fois votre mode déployé, effectuez un dernier test en déclenchant le webhook. Tapez `numerai node test -v` et appuyez sur ENTRER puis tapez`your model name` et appuyez sur ENTRER.

Si votre test final a réussi, vous avez terminé! Répétez l'étape de configuration du nœud pour chaque nœud supplémentaire que vous souhaitez déployer. Vous pouvez enfin profiter de vos week-ends!
