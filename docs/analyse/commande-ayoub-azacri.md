# Analyse de la commande SDIS 33 (saison feux 2027)

Auteur : Ayoub AZACRI (Chef de projet)
Date : 16 novembre 2026
Contexte : Préparation opérationnelle de la saison estivale 2027 en Gironde (région Nouvelle-Aquitaine)
Commanditaire : Direction du Service Départemental d'Incendie et de Secours de la Gironde (SDIS 33)

## 1. Questions analytiques décisionnelles

### Question 1 : concentration spatiale des départs
> Quels massifs forestiers et zones d'interface forêt-habitat concentrent historiquement la plus forte fréquence de départs de feu simultanés lors des épisodes de canicule et de vent sec d'est ?

### Question 2 : fiabilité du seuil d'alerte météo
> Quel est le taux historique de fausses alertes (jours d'indice élevé sans éclosion) et de feux non anticipés pour chaque niveau de l'indice de la Météo des forêts en Gironde ?

### Question 3 : comparaison de la vitesse de propagation
> La cinétique de propagation des feux en Gironde est-elle significativement plus rapide que celle des départements voisins pour un niveau de danger météorologique équivalent ?

### Question 4 : répartition temporelle des moyens et des astreintes
> Quels jours de la semaine et créneaux horaires concentrent historiquement le plus grand nombre d'éclosions lors des pics de fréquentation touristique estivale ?

## 2. Glossaire des termes inconnus

Termes découverts dans la commande du SDIS 33 à verser au glossaire du groupe :

* SDIS (Service Départemental d'Incendie et de Secours) : structure publique chargée des sapeurs-pompiers et des secours à l'échelle du département.
* Météo des forêts : carte d'alerte quotidienne publiée par Météo-France avec 4 niveaux de danger (vert, jaune, orange, rouge) pour le lendemain et le surlendemain.
* Indice de danger / seuil : indicateur calculé à partir de la chaleur, du vent, de la sécheresse et de l'humidité pour estimer le risque qu'un feu se déclare et se propage.
* Dispositif renforcé : mobilisation accrue des pompiers l'été (gardes payées en plus, camions prépositionnés et patrouilles régulières) dès que le risque grimpe.
* Patrouilles : rondes de surveillance assurées par des véhicules légers sur les pistes forestières pour repérer les fumées au plus vite.
* Guet (ou guet armé) : camions de pompiers postés directement en forêt sur des points hauts pour attaquer un départ de feu en moins de 10 minutes.
* Départs de feu : le moment où le feu s'allume. Il faut les distinguer des hectares brûlés, car un grand nombre de départs traduit surtout des imprudences humaines.
* Chefs de centre : officiers qui dirigent les casernes locales sur le terrain et qui constatent l'écart entre les alertes météo et les feux réels.

## 3. Besoins informationnels de la direction

Ce que la direction du SDIS 33 doit avoir sous les yeux pour trancher ses décisions :

* Coût financier réel d'une journée d'alerte renforcée (heures supplémentaires, carburant) mis en regard du nombre de feux stoppés rapidement.
* Tableau croisé entre les niveaux de vigilance météo et les feux réels sur 10 ans pour mesurer le pourcentage exact de fausses alertes et de feux manqués.
* Carte des délais d'accès réels des pompiers sur les différents massifs du département après un appel au 18 ou au 112.
* Comparatif des surfaces brûlées par rapport à la taille de la forêt entre la Gironde, les Landes voisines et le pourtour méditerranéen.
* Répartition journalière et horaire des départs de feu en saison estivale pour ajuster le calendrier des astreintes rémunérées.

## 4. Spécification de la donnée idéale

| Question analytique | Grain spatial | Grain temporel | Période | Fraîcheur | Emprise |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Question 1 : concentration spatiale des moyens | Coordonnées GPS exactes du départ de feu (au minimum commune et parcelle forestière) | Heure et minute du départ de feu et de son extinction | 2012 à 2026 (15 étés complets pour inclure les crises de 2022 et 2026) | Hebdomadaire pour l'analyse, quotidienne en saison | Département de la Gironde (33) |
| Question 2 : fiabilité du seuil Météo des forêts | Grille météo fine (1 à 2 km) et position des stations météo réelles | Données météo heure par heure et indice de danger calculé chaque midi | 2017 à 2026 (10 ans pour couvrir l'historique de l'indice Météo-France) | Actualisation deux fois par jour (matin pour le jour même, soir pour J+1 et J+2) | Département de la Gironde (33) |
| Question 3 : comparaison de la vitesse de propagation | Maille départementale et découpage par grand massif forestier | Bilan journalier et mensuel des départs et des hectares brûlés | 2010 à 2026 (17 ans pour lisser les étés très pluvieux ou très secs) | Mensuelle hors saison, quotidienne en période estivale | Région Nouvelle-Aquitaine et France entière |
| Question 4 : répartition temporelle des moyens | Commune ou secteur de premier appel | Heure et minute de réception de l'alerte, avec jour de la semaine | 2017 à 2026 (10 étés pour capter les habitudes touristiques récentes) | Quotidienne pendant la saison estivale | Département de la Gironde (33) |


## 5. Confrontation des questions analytiques au catalogue de sources

### Tableau de couverture par question

| Question analytique | BDIFF (Incendies) | Météo des forêts | BD Forêt V2 | Stations horaires | Couverture globale | Décision retenue |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Question 1 : concentration spatiale des départs | Partiel : date, heure et code Insee (date_premiere_alerte, heure_alerte, code_insee, id_incendie), mais pas de GPS fin ni de mention d interface dans l export tabulaire. | Absent : aucune donnée de localisation fine ni de direction du vent (num_dep, nom_dep). | Partiel : cartographie fine des peuplements inflammables de pin maritime, mais millésime ancien (2012-2015) sans feux. | Partiel : direction du vent sec (DD), vitesse (FF), rafales (FXY), température (T) et humidité (U), mais limité à 31 stations ponctuelles. | Partiel | Approximer : croisement communal Insee x stations x taux de pin maritime sans SIG lourd. |
| Question 2 : fiabilité du seuil d alerte météo | Complet : recensement exhaustif des feux réels (date_premiere_alerte, code_departement = 33). | Partiel : niveaux de vigilance quotidiens (niveau_j1, niveau_j2), mais historique court limité à 2024-2026 (pas de 2022). | Absent : pas d indice météo ni d historique de feux. | Partiel : historique complet 2020-2024 des variables physiques de canicule (T, FF, U), mais sans la classe officielle en 4 couleurs. | Partiel | Approximer : matrice de confusion sur 2024-2026 et calcul d un proxy seuil sur stations pour 2022. |
| Question 3 : comparaison de la vitesse de propagation | Partiel : surfaces brûlées finales (surface_totale_brulee_ha) sur toute la France (code_departement), mais sans heure de maîtrise ni cinétique horaire. | Partiel : comparaison interdépartementale possible (num_dep), mais grain départemental uniforme sans historique 2022. | Absent : aucune donnée dynamique de cinétique d incendie. | Partiel : vent et rafales comparables entre départements voisins, mais sans surface de feu associée. | Partiel | Renoncer : abandon de la vitesse horaire fine et reformulation sur la surface moyenne par feu. |
| Question 4 : répartition temporelle des moyens et astreintes | Complet : date d alerte (date_premiere_alerte) et heure à la minute (heure_alerte) sur 2006-2024 permettant d isoler les jours de semaine et créneaux. | Absent : calendrier journalier sans détail horaire (date). | Absent : donnée spatiale statique sans horodatage. | Absent : valide les pics thermiques de l après-midi mais ne recense pas les appels de secours. | Complet | Réponse directe : pas d arbitrage de renoncement, exploitation directe de la BDIFF. |

### Détail des arbitrages et décisions

#### Question 1 : concentration spatiale des départs
* Degré global retenu : partiel.
* Manque identifié : l export tabulaire brut de la BDIFF ne fournit pas les coordonnées géographiques précises (X, Y) au sein de la commune, et ne qualifie pas directement l interface forêt-habitat (WUI). De plus, la BD Forêt V2 de référence date de 2012-2015 et n intègre pas les parcelles rasées lors des incendies de 2022.
* Décision retenue : approximer.
* Justification métier et technique : nous renonçons au calcul vectoriel lourd d intersection géospatiale polygone par polygone. Nous approximons le risque spatial en reliant la BDIFF à la BD Forêt V2 via le code Insee communal (code_insee) enrichi d un indicateur de densité de pin maritime et de bâti diffus, croisé avec les données de vent d est (DD entre 60° et 120°) des stations Météo-France les plus proches.
* Limite ou biais induit : l analyse est agrégée à l échelle de la commune et non de la parcelle cadastrale exacte, ce qui masque l hétérogénéité interne des très grandes communes forestières girondines (ex. La Teste-de-Buch ou Belin-Béliet).

#### Question 2 : fiabilité du seuil d alerte météo
* Degré global retenu : partiel.
* Manque identifié : les archives publiques de la Météo des forêts ne démarrent qu en 2024. Il n existe aucun historique officiel en Open Data pour l été de crise 2022, qui constitue pourtant l étalon de référence décisionnel du SDIS 33.
* Décision retenue : approximer.
* Justification métier et technique : nous scindons l analyse en deux volets. Sur la période 2024-2026, nous mesurons directement la matrice de confusion (vrais positifs, fausses alertes Orange/Rouge sans feu, feux en vigilance Verte/Jaune). Pour l été 2022, nous approximons le niveau de risque en construisant une règle seuil simplifiée sur les données physiques des stations horaires (T max > 35°C, FF > 30 km/h et U < 30%).
* Limite ou biais induit : ce seuil physique approché pour 2022 est un proxy indicatif qui ne reproduit pas l intégralité du calcul multicouche de l Indice Forêt Météo (IFM) officiel de Météo-France.

#### Question 3 : comparaison de la vitesse de propagation
* Degré global retenu : partiel.
* Manque identifié : aucune source publique ne renseigne la chronologie d extension du front de flamme (heure de maîtrise, surface heure par heure). Seules l heure du premier appel et la surface finale totale sont consignées dans la BDIFF.
* Décision retenue : renoncer (avec reformulation).
* Justification métier et technique : mesurer une véritable cinétique d extension (en hectares par heure ou mètres par minute) nécessiterait les comptes-rendus d intervention opérationnels du CTA-CODIS, inaccessibles en Open Data. Nous renonçons à cette mesure horaire impossible et nous reformulons la question sur un indicateur macroscopique disponible : la surface moyenne finale détruite par feu (surface_totale_brulee_ha / nb_feux) comparée entre la Gironde et les départements voisins (Landes, Lot-et-Garonne, Dordogne) lors de journées de vent soutenu.
* Limite ou biais induit : la surface finale dépend non seulement de la vitesse de propagation naturelle de la végétation, mais aussi du délai d engagement et de la puissance des moyens de lutte déployés par les pompiers.

#### Question 4 : répartition temporelle des moyens et des astreintes
* Degré global retenu : complet.
* Manque identifié : aucun manque bloquant dans les données sources. La BDIFF fournit un historique continu sur 18 ans avec la date exacte et l heure à la minute.
* Décision retenue : réponse directe (aucun arbitrage de renoncement nécessaire).
* Justification métier et technique : la BDIFF contient les champs date_premiere_alerte et heure_alerte. L extraction du jour de la semaine (lundi au dimanche) et la discrétisation en tranches de 2 heures (créneaux 12h-14h, 14h-16h, 16h-18h, 18h-20h) permettent de croiser directement les éclosions avec les périodes de vacances scolaires et de week-ends estivaux pour dimensionner les gardes du SDIS 33.
* Limite ou biais induit : l heure enregistrée est celle du premier appel au 18/112, qui peut accuser un léger décalage (quelques minutes à une demi-heure) par rapport à l éclosion physique réelle en forêt isolée.
