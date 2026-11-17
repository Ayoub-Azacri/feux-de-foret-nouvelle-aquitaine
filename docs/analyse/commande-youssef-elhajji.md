# Analyse de la commande - Youssef EL HAJJI

## 1. Les questions

Quatre questions dont la réponse aiderait la direction à trancher.

1. Dans quelles communes ou zones forestières de Gironde a-t-on enregistré le plus de départs de feux et de surfaces brûlées ces dernières années ? 

2. À partir de quel niveau de la Météo des forêts la majorité des feux démarrent-ils réellement en Gironde ?

3. Combien de journées d'alerte élevée ont eu lieu sans aucun départ de feu et à l'inverse combien de feux ont démarré alors que l'indice était au plus bas ?

4. Est-ce que l'indice de la Météo des forêts se trompe plus souvent en Gironde que dans les départements voisins comme les Landes ?

## 2. Les termes inconnus

Les mots de la commande que vous ne savez pas définir précisément, ou qui peuvent se comprendre de plusieurs façons.

| Terme | Ce que je crois qu'il veut dire | Ce qu'il faudrait vérifier |
|---|---|---|
| **SDIS** | L'organisme public des sapeurs-pompiers qui gère les secours et la lutte contre les incendies dans le département 33. | Comment est découpé leur budget annuel et qui prend la décision finale d'engager des dépenses de renfort ? |
| **Départs de feu** | Le tout début d'un incendie repéré sur le terrain, qu'il soit petit ou grand. | À partir de quelle surface brûlée ou de quel type de feu le SDIS l'enregistre-t-il officiellement ? |
| **Météo des forêts** | La carte publiée chaque jour en été par Météo-France indiquant le niveau de risque d'incendie par couleur. | Quels paramètres météo précis (température, vent, humidité de l'air ou du sol) sont pris en compte dans le calcul de cet indice ? |
| **Dispositif renforcé** | Le déploiement de moyens supplémentaires (plus de pompiers de garde, véhicules prépositionnés) les jours à risque. | Quels effectifs et véhicules composent exactement ce dispositif, et quel est son coût financier pour une seule journée ? |
| **Seuil actuel** | Le niveau de risque à partir duquel le SDIS déclenche actuellement ses renforts et qui fait débat en interne. | Quelle est la valeur ou la règle exacte utilisée aujourd'hui, et sur quel texte ou protocole interne repose-t-elle ? |
| **Chefs de centre** | Les officiers qui dirigent les différentes casernes de pompiers réparties sur le territoire de la Gironde. | Pourquoi leurs avis divergent-ils : est-ce que leurs casernes sont situées dans des zones aux végétations ou climats différents ? |

## 3. Les besoins

La décision à éclairer, en une phrase : 

Déterminer où positionner en priorité les pompiers et à quel niveau météo précis activer le dispositif renforcé pour protéger la forêt girondine à l'été 2027 sans dépasser le budget.

Ce qui manque dans la commande pour y répondre (une information, une précision, une hypothèse à confirmer) :

- Le montant exact du budget disponible pour la saison 2027 et le coût financier d'une journée de dispositif renforcé.
- La valeur exacte du seuil de déclenchement actuel qui est critiqué par les chefs de centre.
- L'historique détaillé des départs de feux en Gironde sur les dernières années (dates, heures précises, communes et surfaces brûlées notamment pour 2022 et 2026).
- L'historique des prévisions quotidiennes de la Météo des forêts pour comparer l'indice prévu avec les feux réels.
- La règle officielle du SDIS pour comptabiliser un « départ de feu » (taille minimale de la surface brûlée).

## 4. Les données

Pour chaque question, la donnée qu'il vous faudrait idéalement pour répondre.

| Question | Donnée idéale | Grain (une ligne = ?) | Période | Fraîcheur | Emprise géographique |
|---|---|---|---|---|---|
| 1 | Historique complet des incendies recensés avec leur localisation et les dégâts constatés. | Un feu déclar (date, heure, commune, coordonnées GPS, surface brûlée en hectares). | 10 à 15 ans d'historique (2012-2026), incluant les étés records 2022 et 2026. | Annuelle (données historiques consolidées après chaque saison). | Département de la Gironde (33). |
| 2 | Historique des prévisions quotidiennes de la Météo des forêts croisé avec les feux réels survenus le même jour. | Un jour par commune (date, niveau de danger météo prévu, nombre de feux observés). | Les saisons estivales (juin à septembre) des 5 dernières années (2022 à 2026). | Quotidienne (l'indice étant calculé et diffusé chaque jour). | Département de la Gironde (33). |
| 3 | Tableau de comparaison quotidien entre le niveau d'alerte météo et la réalité du terrain (feux ou aucun feu). | Un jour par secteur de surveillance (date, niveau d'alerte, indicateur oui/non de départ de feu, nombre de départs). | Saisons estivales de 2022 à 2026. | Quotidienne. | Département de la Gironde (33). |
| 4 | Historique comparatif de l'indice Météo des forêts et des départs de feux entre la Gironde et les départements voisins. | Un jour par département (date, département, niveau d'indice météo, nombre de feux déclarés). | Saisons estivales de 2022 à 2026. | Quotidienne. | Région Nouvelle-Aquitaine (Gironde, Landes, Dordogne, Lot-et-Garonne) et France. |