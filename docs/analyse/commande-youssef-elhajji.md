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

## 5. Confrontation des questions analytiques au catalogue de sources

### Tableau de couverture par question

| Question | BDIFF (Incendies) | Météo des forêts | BD Forêt V2 | Stations horaires | Couverture globale | Décision |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Question 1** : Communes et zones de Gironde concentrant les départs de feux et surfaces brûlées | complet (colonnes code_insee, date_premiere_alerte, surface_totale_brulee_ha, surface_foret_ha, code_departement) | absent (ne contient aucun historique de sinistres ni découpage communal) | partiel (cartographie du pin maritime mais millésime ancien 2012-2015 ignorant les feux de 2022 et sans historique) | absent (mesures physiques uniquement, aucun enregistrement de sinistres) | complet | conserver |
| **Question 2** : Niveau de la Météo des forêts déclenchant la majorité des feux réels | partiel (fournit la date exacte date_premiere_alerte et code_departement 33, mais sans l'indice météo) | partiel (fournit niveau_j1 de 1 à 4 par date et num_dep, mais historique restreint à 2024-2026 sans l'été 2022) | absent (cartographie végétale statique, aucune donnée de vigilance quotidienne) | partiel (température T, vent FF et humidité U à l'heure du feu AAAAMMJJHH pour vérifier les conditions réelles) | partiel | approximer |
| **Question 3** : Journées d'alerte élevée sans feu (fausses alertes) et feux sous indice faible | partiel (fournit les jours avec feux date_premiere_alerte, mais ne liste pas les jours calmes sans feu) | partiel (calendrier complet par date et niveau_j1 pour repérer les alertes, mais historique limité à 2024-2026) | absent (aucune variable temporelle d'alerte) | partiel (variables T, FF, FXY, U et drapeaux qualité QT, QFF pour auditer les anomalies physiques) | partiel | approximer |
| **Question 4** : Comparaison du comportement de l'indice entre la Gironde et les départements voisins (Landes) | partiel (couvre la Gironde et les Landes via code_departement 33 et 40, mais sans données d'alerte) | partiel (couvre les départements 33 et 40 par num_dep et niveau_j1, mais restreint aux saisons 2024-2026) | absent (cartographie forestière uniquement) | absent (fichier local limité au département 33, sans les stations du département 40) | partiel | approximer |

### Détail des arbitrages et décisions

#### Question 1 : Communes et zones de Gironde concentrant les départs de feux et surfaces brûlées
* Degré global retenu : complet
* Manque identifié : Aucun manque bloquant pour l'analyse à l'échelle communale. On note simplement l'absence des coordonnées GPS précises dans l'export tabulaire brut (le flux WFS IGN serait nécessaire pour le tracé exact des contours de feux).
* Décision retenue : conserver
* Justification métier et technique : La BDIFF fournit directement le nombre de départs et les surfaces brûlées agrégées par code_insee sur tout l'historique 2006-2024. Cela suffit amplement pour identifier les communes prioritaires où prépositionner les moyens d'intervention du SDIS 33.
* Limite ou biais induit : L'analyse s'arrête aux frontières administratives communales sans descendre au niveau de la parcelle forestière fine.

#### Question 2 : Niveau de la Météo des forêts déclenchant la majorité des feux réels
* Degré global retenu : partiel
* Manque identifié : Absence de données ouvertes sur la Météo des forêts pour la saison de crise 2022 (le dispositif n'a été créé qu'en 2023, les archives ne démarrent qu'en 2024).
* Décision retenue : approximer
* Justification métier et technique : Nous croisons la BDIFF et la Météo des forêts sur la période commune 2024-2026 par la date et le numéro de département. Pour l'été record 2022, nous utilisons les relevés physiques de nos stations météo horaires (température T dépassant 35 °C, vent FF et sécheresse de l'air U) comme proxy pour reconstituer les jours à risque extrême.
* Limite ou biais induit : Le proxy météorologique physique n'intègre pas la formule exacte de l'Indice Forêt Météo (IFM) de Météo-France, mais il capture fidèlement les pics de chaleur ayant conduit aux feux de Landiras et La Teste-de-Buch.

#### Question 3 : Journées d'alerte élevée sans feu (fausses alertes) et feux sous indice faible
* Degré global retenu : partiel
* Manque identifié : Manque de l'historique des alertes pour 2022 et absence des données opérationnelles internes du SDIS 33 (signalements d'appels 18/112 non suivis d'intervention).
* Décision retenue : approximer
* Justification métier et technique : Nous construisons la matrice de confusion sur les saisons complètes 2024 à 2026 en générant un calendrier de référence croisé avec la table de faits des feux réels. Les stations météo horaires et leurs drapeaux de contrôle qualité (QT, QFF) permettent d'auditer les jours de divergence (par exemple une alerte élevée sans feu expliquée par une absence réelle de vent local).
* Limite ou biais induit : Le taux de fausse alerte est calculé à l'échelle globale du département 33, ce qui peut masquer le fait qu'une alerte départementale rouge était justifiée pour le Sud-Gironde même si aucun feu ne s'est déclaré sur la zone viticole du Nord.

#### Question 4 : Comparaison du comportement de l'indice entre la Gironde et les départements voisins (Landes)
* Degré global retenu : partiel
* Manque identifié : Pas d'historique 2022 pour la Météo des forêts et absence des relevés de stations météo horaires pour les Landes (40) dans notre fichier local de Gironde.
* Décision retenue : approximer
* Justification métier et technique : Les tables BDIFF et Météo des forêts disposent toutes deux d'une couverture nationale. Nous effectuons le benchmark comparatif du taux d'erreur de l'indice entre la Gironde (33) et les Landes (40) sur les saisons 2024 à 2026 via les clés code_departement et num_dep.
* Limite ou biais induit : Le comparatif ne peut pas intégrer les comportements respectifs lors de la saison exceptionnelle de 2022, faute d'antériorité de l'indice Météo-France.