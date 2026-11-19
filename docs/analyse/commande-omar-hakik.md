# Analyse de la commande SDIS 33 (saison feux 2027)

Auteur : Omar HAKIK (Responsable sources)  
Date : 17 novembre 2026  
Contexte : Préparation opérationnelle de la saison estivale 2027 en Gironde (Nouvelle-Aquitaine)  
Commanditaire : Direction du Service Départemental d'Incendie et de Secours de la Gironde (SDIS 33)  

## 1. Les questions

Quatre questions dont la réponse aiderait la direction à trancher :

1. Dans quelles communes de Gironde y a-t-il le plus souvent des feux et le plus d'hectares brûlés ?
2. Combien de feux se déclarent réellement pour chaque couleur de la Météo des forêts (vert, jaune, orange, rouge) ?
3. Combien de feux ont démarré les jours où l'indice était vert ou jaune, et y avait-il du vent fort ce jour-là ?
4. Est-ce que la Météo des forêts marche moins bien en Gironde que dans les autres départements de la région et en France ?

## 2. Les termes inconnus

Les mots de la commande à clarifier pour éviter les malentendus :

| Terme | Ce que je crois qu'il veut dire | Ce qu'il faudrait vérifier |
| :--- | :--- | :--- |
| **SDIS** | Service Départemental d'Incendie et de Secours (corps des pompiers au niveau départemental). | Son budget opérationnel alloué à la campagne feux de forêt et ses effectifs mobilisables. |
| **Météo des forêts** | Indice de danger feux de forêt publié par Météo-France (échelle de 4 couleurs : vert, jaune, orange, rouge). | Comment l'indice est calculé et si les pompiers l'utilisent tel quel sur le terrain. |
| **Dispositif renforcé** | Mesure opérationnelle exceptionnelle coûteuse (gardes postées, renforts caserne). | Le coût journalier complet d'une journée de mobilisation renforcée pour le SDIS 33. |
| **Guet armé / vigie** | Surveillance active des massifs depuis des tours ou camions postés en forêt. | Les horaires d'activation, la localisation des tours de guet et le temps d'intervention visé (< 10 min). |
| **Départ de feu** | Éclosion d'un incendie nécessitant une intervention. | Le délai d'extinction et la surface finale brûlée. |

## 3. Les besoins

**La décision à éclairer, en une phrase :**  
> Décider où placer les camions de pompiers en Gironde et à partir de quelle couleur météo déclencher les renforts pour l'été 2027, tout en respectant le budget.

**Ce qui manque dans la commande pour y répondre :**  
- Le budget exact dont disposent les pompiers pour tout l'été 2027.
- Combien coûte réellement une journée de renforts (essence, camions, heures supplémentaires).
- Quelle est la couleur météo qui sert de seuil aujourd'hui (orange ou rouge ?).
- L'historique interne des interventions des pompiers de Gironde (leurs rapports de feux des années passées).

## 4. Les données

Pour chaque question, la donnée qu'il faudrait idéalement pour répondre :

| Question | Donnée idéale | Grain (ce que représente 1 ligne) | Période | Fraîcheur | Emprise géographique |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Q1 (Où sont les feux ?)** | Liste de tous les incendies passés avec la commune et la surface brûlée | Un feu de forêt | 10 ans (2015 à 2025) | Une fois par an | La Gironde et départements voisins |
| **Q2 (Feux par couleur météo)** | Historique des couleurs Météo des forêts croisé avec les départs de feux réels | Une journée par département | 5 ans (2020 à 2025) | Tous les jours en été | La Gironde |
| **Q3 (Feux avec météo verte/jaune)** | Mesures de vent et de chaleur les jours où un feu a démarré sous indice bas | Une heure sur une station météo | 5 ans (2020 à 2025) | Toutes les heures | Les stations météo de Gironde |
| **Q4 (Comparaison France)** | Nombre de feux et indice Météo des forêts dans tous les départements pour comparer | Une journée par département | 5 ans (2020 à 2025) | Tous les jours en été | Toute la France |

## 5. Confrontation des questions analytiques au catalogue de sources

### Tableau de couverture par question

| Question | BDIFF (Incendies) | Météo des forêts | BD Forêt V2 | Stations horaires | Couverture globale | Décision |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Question 1** : Communes et surfaces brûlées | complet : recensement de chaque feu réel par commune (code_insee) et surface brûlée (surface_totale_brulee_ha, surface_foret_ha) | absent : aucun feu recensé, uniquement des indices prévisionnels départementaux | partiel : cartographie des peuplements de pins maritimes (essence) mais pas les feux réels | absent : uniquement des données météorologiques physiques sans mention des incendies | complet | exploiter directement |
| **Question 2** : Feux réels par couleur météo | partiel : date et heure précises de chaque feu (date_premiere_alerte, heure_alerte) mais sans l'indice météo | partiel : niveaux de danger de 1 à 4 (niveau_j1, niveau_j2) mais pas d'historique avant 2024 et grain départemental | absent : aucune donnée de météo ou de vigilance | absent : mesures physiques de base mais ne contient pas l'indice synthétique officiel | partiel | approximer |
| **Question 3** : Feux sous indice vert/jaune et vent | partiel : heure du premier appel au 18 (date_premiere_alerte, heure_alerte) mais pas de données météo | partiel : repérage des jours à indice 1 ou 2 (niveau_j1) mais sans vitesse du vent en km/h | absent : aucune donnée temporelle ou météorologique | partiel : mesures horaires de vent (FF) et rafales (FXY) mais anémomètre absent à la station de Belin-Béliet | partiel | approximer |
| **Question 4** : Comparaison Gironde vs Nouvelle-Aquitaine | partiel : historique de tous les départements (code_departement) mais sans la Météo des forêts | partiel : couvre tous les départements (num_dep) mais sur 3 saisons estivales seulement (2024 à 2026) | absent : analyse trop lourde pour une comparaison globale | absent : fichier limité au département de la Gironde (code 33) | partiel | renoncer |

### Détail des arbitrages et décisions

#### Question 1 : Communes et surfaces les plus touchées en Gironde
* Degré global retenu : complet
* Manque identifié : aucun manque bloquant, la table BDIFF répond directement à la localisation communale et au calcul des surfaces brûlées.
* Décision retenue : exploiter directement
* Justification métier et technique : la BDIFF constitue la vérité terrain officielle de l'État pour identifier les secteurs prioritaires où le SDIS 33 doit positionner ses moyens.
* Limite ou biais induit : les coordonnées GPS fines du point d'éclosion ne sont pas dans l'export tabulaire brut, ce qui oblige à travailler au centroïde communal sans géométrie exacte des pistes DFCI.

#### Question 2 : Proportion de feux réels par niveau d'indice de la Météo des forêts
* Degré global retenu : partiel
* Manque identifié : absence d'historique de la Météo des forêts pour les étés antérieurs à 2024, notamment l'année de crise 2022 (Landiras et La Teste-de-Buch).
* Décision retenue : approximer
* Justification métier et technique : nous ne pouvons pas inventer les bulletins officiels de 2022. En revanche, pour tester la pertinence du dispositif sur cette saison critique, nous utiliserons les variables de température et de vent des stations horaires comme proxy physique pour reconstituer le niveau de danger estimé.
* Limite ou biais induit : l'indice reconstitué restera une approximation calculée par notre pipeline et non la vigilance officielle reçue par le centre de secours cette année-là.

#### Question 3 : Feux sous vigilance verte ou jaune avec vent fort
* Degré global retenu : partiel
* Manque identifié : la station météorologique de Belin-Béliet, pourtant située en plein cœur du massif forestier sensible, ne dispose pas de capteur de vent opérationnel dans l'export officiel.
* Décision retenue : approximer
* Justification métier et technique : pour les incendies éclos dans le secteur de Belin-Béliet sous indice bas, nous appliquerons une règle d'imputation par proximité géographique en utilisant les mesures de vent de la station voisine de Cazats.
* Limite ou biais induit : une marge d'erreur locale sur la force réelle du vent au moment précis de l'éclosion en raison de l'éloignement de la station de remplacement (environ 15 km).

#### Question 4 : Comparaison de la performance de l'indice entre la Gironde et la région
* Degré global retenu : partiel
* Manque identifié : l'historique de la Météo des forêts est trop court (3 saisons d'archives de 2024 à 2026) pour mener une analyse statistique robuste sur 10 ou 15 ans.
* Décision retenue : renoncer
* Justification métier et technique : nous renonçons à une comparaison historique longue et nous reformulons la comparaison uniquement sur les saisons estivales disponibles (2024 et 2025) où les données existent pour tous les départements de Nouvelle-Aquitaine.
* Limite ou biais induit : perte de représentativité sur les étés caniculaires extrêmes plus anciens, limitant la portée de la comparaison aux conditions météo récentes.
