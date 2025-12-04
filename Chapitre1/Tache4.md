## 🏆 HC1T4 - Tâche 4 : Composer une fonction pour traiter des données de joueurs

```haskell
import Data.List (sortBy)
import Data.Ord (comparing)

-- Définition du type synonyme pour la clarté
-- Un 'Joueur' est un tuple (Nom, Score)
type Joueur = (String, Int)

-- 1. extractPlayers : Extrait les noms des joueurs d'une liste de Joueur
-- Utilise la fonction map pour appliquer la fonction 'fst' (première composante du tuple)
extractPlayers :: [Joueur] -> [String]
extractPlayers = map fst

-- 2. sortByScore : Trie la liste des joueurs par score décroissant.
-- Nécessite l'importation de Data.List et Data.Ord.
sortByScore :: [Joueur] -> [Joueur]
sortByScore = sortBy (comparing (\(_, score) -> score) `flip` )
-- OU plus simplement pour un tri décroissant :
-- sortByScore = sortBy (\(_, scoreA) (_, scoreB) -> compare scoreB scoreA)
-- Nous utilisons 'flip comparing' pour inverser l'ordre par défaut (croissant) en décroissant.

-- 3. topThree : Retourne les trois premiers éléments d'une liste.
-- Utilise la fonction 'take'
topThree :: [a] -> [a]
topThree = take 3

-- Composition : getTopThreePlayers
-- Composition de fonctions pour appliquer les trois étapes dans l'ordre.
-- L'ordre des fonctions est de droite à gauche : sortByScore -> topThree -> extractPlayers
-- (Non, l'ordre DOIT être : sortByScore -> topThree, puis extractPlayers est appliqué au résultat)
-- L'ordre correct des étapes est : Trier -> Prendre les 3 -> Extraire les noms.
getTopThreePlayers :: [Joueur] -> [String]
getTopThreePlayers = extractPlayers . topThree . sortByScore

-- Bloc principal pour tester la fonction
main :: IO ()
main = do
    let listeDesJoueurs = 
          [ ("Alice", 150)
          , ("Bob", 200)
          , ("Charlie", 90)
          , ("David", 300)
          , ("Eve", 120)
          ] :: [Joueur]

    putStrLn "--- Composition des Fonctions de Classement ---"
    
    -- Test direct de la fonction composée
    let topTrois = getTopThreePlayers listeDesJoueurs
    putStrLn "Liste des joueurs par score (David: 300, Bob: 200, Alice: 150, ...)"
    putStrLn $ "\nLes 3 meilleurs joueurs sont : " ++ show topTrois
    -- Résultat attendu : ["David", "Bob", "Alice"]
```

-----

## 🧐 Explication de la Composition

La composition finale est :

```haskell
getTopThreePlayers = extractPlayers . topThree . sortByScore
```

Comme vous l'avez appris, l'opérateur de composition **`.`** applique les fonctions de **droite à gauche**.

Pour un appel de la fonction comme `getTopThreePlayers listeDesJoueurs`, voici les étapes d'exécution :

1.  **`sortByScore` (la plus à droite) :**

      * **Action :** Reçoit la liste complète des joueurs `[("Alice", 150), ..., ("Eve", 120)]`.
      * **Résultat :** Elle trie la liste par score décroissant.
      * **Sortie :** `[("David", 300), ("Bob", 200), ("Alice", 150), ("Eve", 120), ("Charlie", 90)]`

2.  **`topThree` (au milieu) :**

      * **Action :** Reçoit la liste triée.
      * **Résultat :** Elle prend les 3 premiers éléments de cette liste.
      * **Sortie :** `[("David", 300), ("Bob", 200), ("Alice", 150)]`

3.  **`extractPlayers` (la plus à gauche) :**

      * **Action :** Reçoit la liste des 3 meilleurs joueurs (tuples).
      * **Résultat :** Elle utilise `map fst` pour extraire uniquement la première composante de chaque tuple (le nom).
      * **Sortie :** `["David", "Bob", "Alice"]`

Cette composition crée un pipeline de données très lisible et efficace, où la sortie d'une fonction devient l'entrée de la fonction suivante.
