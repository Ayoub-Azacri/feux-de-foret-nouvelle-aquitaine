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
