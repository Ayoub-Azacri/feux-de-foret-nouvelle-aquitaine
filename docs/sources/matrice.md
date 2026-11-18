# Matrice collective d'équipe : questions décisionnelles x sources de données

* Document consolidé par : Ayoub AZACRI (Chef de projet)
* Relecture officielle : Omar HAKIK (Responsable sources)
* Co-auteurs : Youssef EL HAJJI (Responsable qualité), Youssef DEKHAIL (Responsable pipeline)
* Date : 18 novembre 2026
* Contexte : SDIS 33, préparation opérationnelle de la saison feux 2027
* Référence projet : Ticket #21, branche `feature/matrice-decisions`

---

## 1. Tableau croisé d'équipe : questions consolidées x sources réelles

Ce tableau synthétise la confrontation collective des 6 questions décisionnelles de l'équipe face aux 4 sources du catalogue Open Data et aux données internes du commanditaire.

| N° | Question analytique consolidée | BDIFF (Incendies IGN) | Météo des forêts (Météo-France) | BD Forêt V2 (IGN) | Stations horaires (Météo-France) | Couverture globale | Décision retenue | Renvoi Journal |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Q1** | **Concentration spatiale des éclosions et massifs vulnérables** (Auteurs : Ayoub, Omar, Youssef EL H., Youssef D.) | Partiel : date, heure et code Insee (`date_premiere_alerte`, `heure_alerte`, `code_insee`, `id_incendie`), mais pas de GPS fin ni de WUI dans le CSV brut. | Absent : prévision départementale sans coordonnées ni direction locale du vent (`num_dep`, `nom_dep`). | Partiel : cartographie fine des peuplements inflammables (`code_tfv`, `essence = Pin maritime`), mais millésime ancien (2012-2015) sans feux. | Partiel : direction du vent sec (`DD`), vitesse (`FF`), rafales (`FXY`), température (`T`), humidité (`U`) sur 31 stations ponctuelles. | Partiel | Approximer : jointure communale Insee x taux d'enrésinement pin x vent d'est, sans calcul SIG vectoriel lourd. | DEC-001 |
| **Q2** | **Fiabilité du seuil Météo des forêts et matrice de confusion** (Auteurs : Ayoub, Omar, Youssef EL H., Youssef D.) | Complet : vérité terrain exhaustive des feux réels (`date_premiere_alerte`, `code_departement = 33`, `surface_totale_brulee_ha`). | Partiel : niveaux de vigilance quotidiens (`niveau_j1`, `niveau_j2`), mais historique court limité à 2024-2026 (absence de la saison 2022). | Absent : information statique de végétation sans historique d'alerte météo. | Partiel : historique continu 2020-2024 des paramètres physiques (`T`, `FF`, `U`), mais sans la classification officielle en 4 couleurs. | Partiel | Approximer : matrice de confusion directe sur 2024-2026 et reconstitution d'un seuil proxy physique pour l'été 2022. | DEC-002 |
| **Q3** | **Modulation spatiale (massifs) et temporelle (mois) du seuil d'alerte** (Auteurs : Youssef D., Ayoub) | Partiel : ventilation mensuelle (`date_premiere_alerte`) et communale (`code_insee`), mais sans indice de risque météo associé. | Partiel : ventilation mensuelle possible par date, mais grain départemental uniforme (`num_dep = 33`) masquant les massifs locaux. | Partiel : cartographie fine de la part de pin maritime par polygone pour délimiter la sensibilité des massifs (Landes, littoral, vignoble). | Partiel : paramètres physiques locaux (`NUM_POSTE`, `T`, `FF`), mais avec capteur de vent absent sur la station forestière de Belin-Béliet. | Partiel | Approximer : modélisation communale croisée (Insee x pin maritime) et substitution de la station Cazats pour le vent de Belin-Béliet. | DEC-003 |
| **Q4** | **Départs de feu non anticipés sous vigilance faible ou modérée (Vert / Jaune)** (Auteurs : Omar, Youssef EL H.) | Complet : inventaire complet des feux déclarés les jours classés en Vert ou Jaune (`date_premiere_alerte`, `id_incendie`). | Partiel : identifie les jours de vigilance 1 (Vert) et 2 (Jaune), mais ne donne aucune explication physique locale sur l'éclosion. | Absent : géométrie statique sans horodatage des conditions de propagation. | Partiel : relevés horaires permettant d'identifier des effets de brise marine, des rafales locales (`FXY`) ou une chute locale d'hygrométrie (`U`). | Partiel | Approximer : jointure BDIFF x Météo des forêts (jours Vert/Jaune avec feux) x stations horaires locales pour isoler les anomalies micro-climatiques. | DEC-004 |
| **Q5** | **Comparaison interdépartementale et régionale du risque incendie** (Auteurs : Ayoub, Omar, Youssef EL H., Youssef D.) | Partiel : couverture nationale complète de 2006 à 2024 (`code_departement`, `surface_totale_brulee_ha`), mais sans heure de maîtrise du feu. | Partiel : 96 départements couverts de 2024 à 2026 (`num_dep`, `date`), mais grain départemental uniforme sans historique 2022. | Absent : données vectorielles nationales hétérogènes et inexploitables dans le temps du projet. | Partiel : réseau de stations dense sur toute la France mais volume tabulaire massif (206 colonnes par département). | Partiel | Renoncer : abandon de la mesure de cinétique horaire fine (ha/h) et reformulation sur la surface moyenne brûlée par feu. | DEC-005 |
| **Q6** | **Répartition horaire et hebdomadaire pour les astreintes pompiers** (Auteur : Ayoub) | Complet : horodatage précis à la minute du premier appel (`date_premiere_alerte`, `heure_alerte`) sur 18 ans d'historique en Gironde. | Absent : calendrier journalier sans détail horaire (`date`). | Absent : donnée spatiale statique sans dimension temporelle. | Absent : confirme les pointes thermiques de l'après-midi mais ne recense pas les sollicitations opérationnelles des pompiers. | Complet | Réponse directe : pas d'arbitrage de renoncement, exploitation directe de la BDIFF croisée avec le calendrier estival. | DEC-006 |

---

## 2. Lecture horizontale : bilan des manques et arbitrages décisionnels

Conformément à la consigne de Marine PROST, la lecture horizontale identifie ce que les données actuelles ne permettent pas d'affirmer directement :

### L'absence totale de données budgétaires et financières du SDIS 33
Aucune source de l'inventaire Open Data ne contient le coût financier réel d'une journée de mobilisation renforcée (rémunération des gardes postées, carburant des patrouilles, maintenance des véhicules).  
*Impact sur le projet :* le modèle décisionnel ne pourra pas calculer un coût en euros absolus. L'équipe formule une variable de coût paramétrable (forfait journalier estimatif renseigné par le SDIS 33) pour chiffrer les économies potentielles lors de la réduction des fausses alertes.

### La rupture historique de la Météo des forêts (2022 non disponible)
L'indice officiel n'étant publié en Open Data que depuis 2024, la saison de référence 2022 (marquée par les incendies historiques de Landiras et La Teste-de-Buch avec plus de 30 000 hectares détruits) ne possède aucun historique de vigilance préfectorale.  
*Arbitrage :* nous refusons de renoncer à l'année 2022. Nous construisons une règle proxy basée sur les relevés physiques des stations météo horaires (température > 35 °C, vent > 30 km/h, humidité relative < 30%) pour simuler le comportement du risque lors de cette crise.

### L'absence de géométrie fine et de cinétique horaire dans la BDIFF
La BDIFF ne contient ni les coordonnées GPS ponctuelles de la parcelle forestière (dans son export tabulaire brut), ni l'heure de maîtrise ou d'extinction du feu.  
*Arbitrage :* nous renonçons au calcul de vitesse de propagation en hectares par heure (qui relève des mains courantes internes du CODIS), et nous reformulons l'analyse comparative sur la surface moyenne finale détruite par événement (`surface_totale_brulee_ha / nb_feux`).

---

## 3. Lecture verticale : application stricte du principe de minimisation

La lecture verticale détermine les données à écarter d'office du pipeline pour éviter tout stockage inutile, tout calcul superflu et toute infraction au principe de proportionnalité :

### Écartement des géométries vectorielles lourdes de la BD Forêt V2
La BD Forêt V2 représente plus de 200 Mo de polygones Shapefile ou GeoPackage pour la seule Gironde, avec plusieurs dizaines de milliers d'entités géométriques complexes. Effectuer des jointures spatiales géométriques (intersections de polygones) à chaque requête saturerait la mémoire du pipeline sans apporter de gain décisionnel par rapport au besoin du SDIS 33.  
*Règle de minimisation retenue :* le pipeline écarte totalement les fichiers vectoriels géométriques. Une extraction tabulaire préalable agrège le taux de couverture en pin maritime par code commune Insee (`code_insee`), stockée sous forme d'une dimension géographique légère de quelques dizaines de kilo-octets.

### Projection stricte sur les variables utiles des stations météo horaires
Le fichier d'archives des stations horaires de Météo-France comporte 206 colonnes (861 911 lignes pour la Gironde sur 5 ans), comprenant des grandeurs sans rapport avec le risque incendie en plaine (hauteur de neige, état du sol, rayonnement spécifique).  
*Règle de minimisation retenue :* le script d'ingestion applique une projection SQL/Pandas immédiate dès la lecture pour ne retenir que les 8 attributs requis pour les calculs du SDIS 33 : `NUM_POSTE`, `AAAAMMJJHH`, `T`, `FF`, `FXY`, `DD`, `U`, `RR1`, accompagnés de leurs drapeaux de qualité (`QT`, `QFF`, `QU`). Les 198 colonnes restantes sont ignorées dès le chargement brut.

### Exclusion des données nominatives et conformité RGPD
Aucune donnée personnelle n'est ingérée. Les fiches BDIFF sont strictement anonymisées à l'échelle communale et matérielle. Le pipeline applique une règle d'exclusion systématique de tout champ de texte libre non structuré susceptible de contenir des noms d'exploitants forestiers ou de témoins.

---

## 4. Synthèse des correspondances et clés de jointure

Pour relier les 4 sources dans l'entrepôt consolidé, le groupe valide le modèle de clés suivant :

* **Clé spatiale de référence :** le code commune Insee (`code_insee` sur 5 caractères, ex. 33042 pour Belin-Béliet). Utilisé pour joindre la BDIFF et la dimension d'occupation du sol issue de la BD Forêt V2.
* **Clé temporelle de référence :** la date calendaire (`date` au format AAAA-MM-JJ). Utilisée pour joindre la BDIFF avec les archives départementales de la Météo des forêts (`num_dep = 33` et `date`).
* **Clé spatio-temporelle fine :** le couple (`NUM_POSTE`, `AAAAMMJJHH`). Utilisé pour rattacher chaque éclosion de feu de la BDIFF aux relevés horaires de la station Météo-France la plus proche lors de la tranche horaire du sinistre.
