import Data.List (sortBy)
import Data.Ord (comparing)

type Player = (String, Int)
extractPlayers :: [Player] -> [Player]
extractPlayers = id 

sortByScore :: [Player] -> [Player]
sortByScore = sortBy (flip (comparing snd))
topTrois :: [Player] -> [Player]
topTrois = take 3
getTopThreePlayers :: [Player] -> [Player]
getTopThreePlayers = topTrois . sortByScore . extractPlayers

-- --- Exemples d'utilisation ---

-- Liste de données de joueurs brutes
playersData :: [Player]
playersData = [("Alice", 85), ("Bob", 92), ("Charlie", 78), ("David", 95), ("Eve", 88)]

-- Appel de la fonction composée
main :: IO ()
main = do
    putStrLn "Liste complète des joueurs :"
    print playersData
    putStrLn "\nLes trois meilleurs joueurs (triés par score décroissant) :"
    print (getTopThreePlayers playersData)


Explication du code

extractPlayers :: [Player] -> [Player],La signature de type indique qu'elle prend une liste de Player et retourne une liste de Player.

extractPlayers = id,"L'implémentation utilise la fonction identité (id). Cela signifie que, dans ce cas précis, la fonction ne fait que retourner

la liste d'entrée telle quelle. Cela est fait pour s'adapter à l'énoncé de la tâche, où elle aurait normalement transformé des données brutes (non-Player) en format Player."

sortByScore :: [Player] -> [Player],Prend une liste de Player et retourne une liste de Player (triée).

sortByScore = sortBy (flip (comparing snd)),"C'est l'étape de tri. Elle utilise des fonctions de la bibliothèque Data.List : * sortBy : La fonction principale de tri. * comparing snd : Crée une fonction de comparaison qui se concentre uniquement sur le deuxième élément du tuple (le score). * flip : Inverse l'ordre de la fonction de comparaison, ce qui permet d'obtenir un tri décroissant (du score le plus élevé au plus faible)."

topTrois :: [Player] -> [Player],Prend une liste de Player et retourne une liste de Player (contenant au maximum 3 joueurs).

topTrois = take 3,Utilise la fonction standard take pour sélectionner les 3 premiers éléments de la liste triée.

getTopThreePlayers :: [Player] -> [Player],"La fonction principale, elle prend la liste initiale et retourne le top 3."

getTopThreePlayers = topTrois . sortByScore . extractPlayers,C'est le cœur de la solution : la composition de fonctions. L'opérateur point (.) enchaîne les fonctions. L'exécution se fait de droite à gauche (comme f(g(x))). 1. extractPlayers est appliquée aux données brutes. 2. Le résultat est passé à sortByScore (Tri). 3. Le résultat est passé à topTrois (Sélection des 3 premiers).
