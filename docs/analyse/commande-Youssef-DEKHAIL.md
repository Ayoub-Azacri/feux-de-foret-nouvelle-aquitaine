# Analyse de la commande - Youssef DEKHAIL

## 1. Les questions

**La décision à éclairer :** où concentrer les moyens du SDIS 33 et à partir de quel niveau de la Météo des forêts déclencher le dispositif renforcé en 2027, sachant que le budget ne permet pas de renforcer partout tout l'été. Notre région d'étude est la Nouvelle-Aquitaine, avec la Gironde comme zone principale.

1. Quelles zones de la Nouvelle-Aquitaine (massifs, communes) ont le plus de départs de feu et de surfaces brûlées depuis 2012, et où se place la Gironde ?
2. À partir de quel niveau de la Météo des forêts les départs de feu deviennent-ils assez nombreux pour justifier le dispositif renforcé, sans le déclencher pour rien ?
3. Le bon niveau de déclenchement est-il le même partout en Gironde et pendant tout l'été, ou change-t-il selon le massif et le mois ?
4. L'indice se comporte-t-il en Gironde comme dans les autres départements de la Nouvelle-Aquitaine et comme dans le reste de la France ?

## 2. Les termes inconnus

Ces termes viennent tous du mail de la direction.

| Terme | Ce que je crois qu'il veut dire | Ce qu'il faudrait vérifier |
| :--- | :--- | :--- |
| Météo des forêts | Un indice qui indique le danger d'incendie du jour | Combien de niveaux il y a, qui le calcule, et pour quelle zone (département, massif ?) |
| Seuil actuel | Le niveau de l'indice à partir duquel le SDIS renforce le dispositif | Quel niveau exactement, et s'il est le même partout |
| Dispositif renforcé | Plus de patrouilles et de guet (le mail dit « patrouilles, guet, etc. ») | Ce que contient le « etc. » et combien ça coûte par jour |
| Danger élevé / indice au plus bas | Les niveaux hauts et bas de l'indice | Quels niveaux comptent comme « élevé » et comme « bas » |
| Départ de feu | Un début d'incendie en forêt | À partir de quelle taille on le compte comme un feu |
| Moyens | Les pompiers, le matériel et l'argent (« humains comme financiers ») | Le budget disponible et comment il est réparti |
| Autres départements de la région | Les départements de la Nouvelle-Aquitaine autour de la Gironde (région choisie par notre groupe) | Si le mail veut bien toute la région ou seulement les départements voisins |
| Reste du territoire national | La France entière, pour comparer | Si on compare avec toute la France ou seulement la métropole |
| Autant de feux que l'été 2026, voire davantage | Un été au moins aussi difficile que 2026 | Comment on mesure ça (nombre de feux, surface brûlée, météo ?) |

## 3. Les besoins

**Ce qui manque dans la commande pour y répondre :**

- Le **budget** et le **coût d'une journée** de dispositif renforcé, sinon on ne peut pas comparer deux seuils.
- Le **seuil actuel** précis et la zone où il s'applique.
- La **taille minimale** d'un feu qu'on veut prendre en compte.
- L'**accès aux données du SDIS** (date, heure et lieu des feux), parce que les bases nationales sont moins précises.
- Une **hypothèse à confirmer** : on regarde toute la Nouvelle-Aquitaine, avec la Gironde comme zone principale, et l'historique depuis 2012, avec 2022 et 2026 même si ce sont des étés exceptionnels.

## 4. Les données

| Question | Donnée idéale | Grain (une ligne = ?) | Période | Fraîcheur | Emprise géographique |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | Départs de feu avec lieu (GPS), surface brûlée, cause, massif | Un départ de feu | 2012-2026 | Temps réel | Nouvelle-Aquitaine (focus Gironde) |
| 2 | Niveau de la Météo des forêts jour par jour, croisé avec les départs de feu | Un jour × une zone | 2012-2026 | Deux fois par jour (prévision) | Gironde |
| 3 | Même donnée que la question 2, avec le massif et le mois | Un jour × un massif | 2012-2026 (surtout les étés) | Deux fois par jour (prévision) | Gironde, par massif |
| 4 | Niveau de la Météo des forêts et départs de feu pour tous les départements | Un jour × un département | 2012-2026 | Une fois par mois suffit pour comparer | Nouvelle-Aquitaine et France |

## 5. Confrontation des questions analytiques au catalogue de sources

### Tableau de couverture par question

| Question | BDIFF (Incendies) | Météo des forêts | BD Forêt V2 | Stations horaires | Couverture globale | Décision |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Question 1** : Zones de Nouvelle-Aquitaine les plus touchées depuis 2012 | complet : historique 2006-2024 avec colonnes code_insee, code_departement, surface_totale_brulee_ha, surface_foret_ha, date_premiere_alerte | absent : prévision départementale sans aucun relevé d'incendie réel | partiel : description des essences et du couvert végétal (code_tfv, essence) mais sans historique d'incendies | absent : relevés météorologiques physiques sans données d'incendies | complet | approximer |
| **Question 2** : Niveau de Météo des forêts justifiant le renfort sans fausse alerte | partiel : vérité terrain des départs de feu (date_premiere_alerte, code_departement = 33) sans indice de danger météo | partiel : niveaux de vigilance de 1 à 4 (niveau_j1, niveau_j2, num_dep = 33) mais limité aux saisons 2024-2026 sans historique 2022 | absent : géométrie statique de la végétation sans historique d'alerte | partiel : paramètres physiques (FF, T, U) utiles pour expliquer les départs mais sans l'indice officiel | partiel | approximer |
| **Question 3** : Variation spatiale par massif et temporelle par mois en Gironde | partiel : ventilation mensuelle possible par date_premiere_alerte et communale par code_insee, mais sans indice météo | partiel : ventilation mensuelle possible par date, mais grain départemental uniforme (num_dep = 33) masquant les massifs | partiel : cartographie fine de la part de pin maritime (essence = Pin maritime) par polygone geom pour délimiter les massifs | partiel : relevés micro-climatiques locaux (NUM_POSTE, T, FF) mais avec capteurs absents sur Belin-Béliet | partiel | approximer |
| **Question 4** : Comparaison du comportement de l'indice en Gironde, région et France | complet : ensemble des départements français couverts avec code_departement, date_premiere_alerte et surfaces brûlées | complet : 96 départements métropolitains couverts jour par jour (num_dep, date, niveau_j1, niveau_j2) de 2024 à 2026 | partiel : données nationales existantes mais millésimes hétérogènes et volume SIG trop lourd | partiel : stations réparties sur toute la France mais volume tabulaire massif (206 colonnes par département) | complet | approximer |

### Détail des arbitrages et décisions

#### Question 1 : Zones de la Nouvelle-Aquitaine ayant le plus de départs de feu et de surfaces brûlées
* Degré global retenu : complet
* Manque identifié : la BDIFF s'arrête à la saison 2024 dans l'export consolidé disponible (les années 2025 et 2026 ne sont pas consolidées) et ne comporte pas de colonne explicite pour le nom du massif forestier.
* Décision retenue : approximer
* Justification métier et technique : la BDIFF fournit une couverture exhaustive de 2012 à 2024 sur l'ensemble de la région Nouvelle-Aquitaine et de la France. Le pipeline regroupera les communes par massif forestier DFCI via une table de correspondance géographique sur le code Insee, permettant de classer rigoureusement la Gironde par rapport aux autres départements néo-aquitains.
* Limite ou biais induit : l'absence des bilans 2025 et 2026 empêche de mesurer les départs les plus récents, mais la période 2012-2024 inclut l'été historique de 2022, ce qui garantit la représentativité statistique du modèle.

#### Question 2 : Niveau de la Météo des forêts justifiant le renforcement sans fausses alertes
* Degré global retenu : partiel
* Manque identifié : l'archive ouverte de la Météo des forêts ne couvre que les saisons estivales 2024, 2025 et 2026. La saison de crise majeure de 2022 n'y figure pas car le dispositif n'existait pas encore en Open Data. De plus, les données de coûts financiers d'une journée de mobilisation renforcée sont absentes des sources publiques.
* Décision retenue : approximer
* Justification métier et technique : le pipeline réalisera une jointure interne entre la BDIFF et les archives de la Météo des forêts sur la clé composite (date, num_dep) pour les saisons 2024 à 2026 afin de mesurer le taux de fausses alertes (jours Orange ou Rouge sans incendie significatif) et d'éclosions non anticipées (feux sous indice Vert ou Jaune). Pour 2022, un proxy de risque météorologique sera reconstitué via les paramètres physiques des stations horaires (température T supérieure à 35 °C et vent FF soutenu).
* Limite ou biais induit : l'analyse du seuil optimal s'appuie sur un historique d'indice officiel court (trois saisons estivales), et l'évaluation budgétaire devra reposer sur une estimation paramétrable du coût d'une garde postée transmise par le SDIS 33.

#### Question 3 : Variation du bon niveau de déclenchement selon le massif et le mois
* Degré global retenu : partiel
* Manque identifié : l'indice de la Météo des forêts est calculé à la maille uniforme du département (une seule valeur par jour pour tout le 33), ce qui empêche de mesurer directement des seuils différenciés par massif. De plus, la station météo forestière de Belin-Béliet ne mesure pas le vent dans l'export brut.
* Décision retenue : approximer
* Justification métier et technique : le pipeline modélisera la sensibilité territoriale en croisant la vigilance départementale avec une dimension communale enrichie par la BD Forêt V2 (taux d'enrésinement en pin maritime par code Insee). Les disparités temporelles seront capturées en ventilant les ratios d'éclosion par mois (juin, juillet, août, septembre). Pour le vent en Sud-Gironde, les relevés de la station de Cazats seront utilisés en substitution de Belin-Béliet.
* Limite ou biais induit : l'indice Météo des forêts reste uniforme sur le département dans les données sources ; la modulation par massif sera le résultat de notre modèle décisionnel croisé et non d'une prévision officielle distincte fournie par Météo-France.

#### Question 4 : Comparaison du comportement de l'indice en Gironde, région et France
* Degré global retenu : complet
* Manque identifié : le volume des données à l'échelle nationale (96 départements sur plusieurs années) risque d'alourdir les temps de traitement si l'on intègre des données horaires locales.
* Décision retenue : approximer
* Justification métier et technique : la comparaison s'appuiera strictement sur les deux tables au grain départemental journalier : la BDIFF agrégée par jour et département, et la Météo des forêts (num_dep, date, niveau_j1, niveau_j2). Le périmètre sera restreint aux 12 départements de Nouvelle-Aquitaine complétés par un échantillon national représentatif (départements méditerranéens des Bouches-du-Rhône, du Var et de l'Hérault).
* Limite ou biais induit : la comparaison nationale portera sur les saisons 2024 à 2026 uniquement, ce qui suffit pour comparer la calibration de l'indice entre territoires mais ne capture pas le comportement comparé lors des sécheresses extrêmes antérieures à 2024.
