# Journal des décisions d'architecture et de modélisation

* Projet : Préparation opérationnelle de la saison feux 2027 (SDIS 33)
* Dépôt : `feux-de-foret-nouvelle-aquitaine`
* Cadre méthodologique : Titre RNCP Niveau 7 / UE01.A Modélisation et pipelines de données
* Responsable de la tenue du journal : Ayoub AZACRI (Chef de projet)
* Validation : Omar HAKIK (Responsable sources), Youssef EL HAJJI (Qualité), Youssef DEKHAIL (Pipeline)

---

## DEC-001 : Approximation du risque spatial par le taux communal d'enrésinement

* **Date :** 18 novembre 2026
* **Auteurs :** Ayoub AZACRI, Youssef DEKHAIL, Omar HAKIK, Youssef EL HAJJI
* **Question rattachée :** Q1 (Concentration spatiale des éclosions et massifs vulnérables)
* **Manque identifié :** la BDIFF en export tabulaire brut ne contient pas les coordonnées GPS précises au sein de la commune, et ne qualifie pas l'interface forêt-habitat (WUI). La BD Forêt V2 vectorielle complète (> 200 Mo) est trop lourde pour un pipeline décisionnel classique.
* **Décision retenue :** `approximer`.
* **Raison métier et technique :** nous renonçons au calcul géométrique lourd d'intersection de polygones vectoriels. Nous créons une table de référence communale Insee enrichie du pourcentage de couverture en pin maritime issu de la BD Forêt V2. Ce taux est croisé avec l'historique des feux BDIFF et les relevés de vent sec d'est (`DD` entre 60° et 120°) des stations Météo-France les plus proches.
* **Ce que la décision coûte (biais et limites) :** l'analyse est agrégée au niveau de la commune et non de la parcelle cadastrale exacte. Cela masque l'hétérogénéité interne des très vastes communes forestières girondines (ex. La Teste-de-Buch ou Belin-Béliet), mais réduit le temps de traitement de plusieurs heures à quelques secondes.
* **Statut :** validée.

---

## DEC-002 : Reconstitution d'un seuil proxy physique pour la saison de crise 2022

* **Date :** 18 novembre 2026
* **Auteurs :** Ayoub AZACRI, Omar HAKIK, Youssef EL HAJJI, Youssef DEKHAIL
* **Question rattachée :** Q2 (Fiabilité du seuil Météo des forêts et matrice de confusion)
* **Manque identifié :** le dispositif d'alerte de la Météo des forêts a été inauguré en 2023. Les archives publiques ne couvrent que les saisons 2024 à 2026. L'été historique de 2022 (plus de 30 000 hectares détruits à Landiras et La Teste-de-Buch) est totalement absent de l'historique de vigilance Open Data.
* **Décision retenue :** `approximer`.
* **Raison métier et technique :** nous scindons l'évaluation en deux étapes. Sur 2024-2026, calcul direct de la matrice de confusion officielle (taux de fausses alertes Orange/Rouge et feux sous vigilance faible). Pour 2022, nous construisons une règle seuil physique calibrée sur les stations météo horaires : un jour est considéré comme équivalent à un risque élevé si la température maximale dépasse 35 °C, la vitesse moyenne du vent excède 30 km/h et l'hygrométrie relative descend sous 30%.
* **Ce que la décision coûte (biais et limites) :** le seuil physique 2022 est un proxy indicatif qui ne reproduit pas l'intégralité du calcul multicouche de l'Indice Forêt Météo (IFM) officiel de Météo-France. Il permet néanmoins d'intégrer l'été 2022 dans le benchmark sans fausser l'historique.
* **Statut :** validée.

---

## DEC-003 : Substitution de la station Cazats pour pallier l'anémomètre manquant de Belin-Béliet

* **Date :** 18 novembre 2026
* **Auteurs :** Youssef DEKHAIL, Youssef EL HAJJI, Ayoub AZACRI, Omar HAKIK
* **Question rattachée :** Q3 (Modulation spatiale et temporelle du seuil d'alerte)
* **Manque identifié :** la station météorologique historique de Belin-Béliet (poste 33042001), située au cœur du massif forestier des Landes de Gascogne, ne dispose pas d'anémomètre ni d'hygromètre opérationnel dans l'export Open Data (valeurs de vent et d'humidité nulles pour toutes les lignes observées).
* **Décision retenue :** `approximer`.
* **Raison métier et technique :** pour évaluer le vent et la sécheresse de l'air dans ce secteur hautement inflammable, le pipeline substitue automatiquement les mesures de la station voisine de Cazats (poste 33116001), située à moins de 25 km dans les mêmes conditions d'exposition forestière continentale.
* **Ce que la décision coûte (biais et limites) :** une légère imprécision micro-climatique locale (quelques km/h d'écart sur les rafales ponctuelles), mais qui évite le rejet pur et simple des départs de feux survenus dans le secteur de Belin-Béliet.
* **Statut :** validée.

---

## DEC-004 : Qualification des feux sous indice faible par les anomalies physiques locales

* **Date :** 18 novembre 2026
* **Auteurs :** Omar HAKIK, Youssef EL HAJJI, Ayoub AZACRI
* **Question rattachée :** Q4 (Départs de feu non anticipés sous vigilance Verte ou Jaune)
* **Manque identifié :** la Météo des forêts diffuse un indice uniforme pour tout le département de la Gironde, ce qui masque les phénomènes locaux (effet de brise thermique sur le littoral atlantique, sécheresse de l'humus sur le massif dunaire).
* **Décision retenue :** `approximer`.
* **Raison métier et technique :** le pipeline isole l'ensemble des feux déclarés lors des journées classées Vert ou Jaune dans la BDIFF. Il effectue une jointure spatio-temporelle avec les stations horaires environnantes pour identifier si une anomalie locale non captée par la prévision globale (rafales soudaines `FXY`, chute brutale de l'humidité relative `U` en milieu d'après-midi) explique l'éclosion.
* **Ce que la décision coûte (biais et limites) :** l'analyse n'explique que les facteurs atmosphériques ; elle ne permet pas de tracer les causes humaines imprévisibles (jets de mégots, feux de camp illégaux, travaux agricoles).
* **Statut :** validée.

---

## DEC-005 : Renoncement à la cinétique horaire fine au profit de la surface moyenne par feu

* **Date :** 18 novembre 2026
* **Auteurs :** Ayoub AZACRI, Omar HAKIK, Youssef DEKHAIL, Youssef EL HAJJI
* **Question rattachée :** Q5 (Comparaison interdépartementale et régionale du risque)
* **Manque identifié :** la BDIFF ne consigne que l'heure de la première alerte et la surface totale finale calcinée. L'heure de maîtrise, l'heure d'extinction définitive et le taux d'expansion horaire du feu (en ha/h) ne figurent dans aucun fichier Open Data.
* **Décision retenue :** `renoncer` (avec reformulation méthodologique).
* **Raison métier et technique :** reconstituer la cinétique horaire nécessiterait les mains courantes d'intervention confidentielles du CTA-CODIS (déploiement minute par minute des groupes d'attaque feux de forêt). Nous renonçons formellement à calculer la vitesse d'avancée du front de flamme. Nous reformulons la question sur un indicateur macroscopique disponible : la surface moyenne finale détruite par feu (`surface_totale_brulee_ha / nb_feux`), comparée entre la Gironde, les Landes (40), le Lot-et-Garonne (47) et un panel méditerranéen de référence (13, 83, 34).
* **Ce que la décision coûte (biais et limites) :** la surface finale ne mesure pas uniquement la vitesse brute de propagation du combustible, mais dépend également du délai de présentation et de la puissance des moyens de secours engagés sur les lieux.
* **Statut :** validée.

---

## DEC-006 : Exploitation directe des timestamps BDIFF et paramétrage du coût SDIS

* **Date :** 18 novembre 2026
* **Auteurs :** Ayoub AZACRI, Youssef EL HAJJI
* **Question rattachée :** Q6 (Répartition horaire et hebdomadaire pour les astreintes pompiers)
* **Manque identifié :** les coûts financiers internes du SDIS 33 (indemnités des gardes postées, carburant des véhicules de surveillance) sont absents des données publiques.
* **Décision retenue :** `complet` sur les données d'éclosion, `approximer` sur la dimension financière.
* **Raison métier et technique :** la BDIFF fournit une complétude totale sur l'horodatage (`date_premiere_alerte`, `heure_alerte`). L'extraction directe du jour de la semaine et des créneaux de 2 heures permet de répondre à 100% au dimensionnement opérationnel des vacations. Pour la valorisation budgétaire, le modèle intègre une variable paramétrable (coût moyen estimé d'une journée de mobilisation renforcée, renseigné par le contrôleur de gestion du SDIS 33).
* **Ce que la décision coûte (biais et limites) :** l'heure d'alerte enregistrée est celle du premier appel au 18/112, avec une latence potentielle de quelques minutes par rapport au départ de feu réel. Le chiffrage budgétaire est un modèle de simulation et non une comptabilité analytique réelle.
* **Statut :** validée.
