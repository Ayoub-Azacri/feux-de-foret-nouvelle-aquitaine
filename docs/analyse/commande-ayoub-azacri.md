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
