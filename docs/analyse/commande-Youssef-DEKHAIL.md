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