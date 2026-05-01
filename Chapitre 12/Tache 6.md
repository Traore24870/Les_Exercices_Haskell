HC12T6 : Trier une liste d’entiers
---
### Code Source (Main.hs)

```haskell
-- Algorithme de tri rapide (QuickSort)
quickSort :: [Int] -> [Int]
quickSort [] = [] -- Une liste vide est déjà triée
quickSort (pivot:reste) = 
    let petits = [x | x <- reste, x <= pivot]
        grands = [x | x <- reste, x > pivot]
    in quickSort petits ++ [pivot] ++ quickSort grands

main :: IO ()
main = do
    putStrLn "Entrez une liste de nombres séparés par des espaces (ex: 5 2 9 1) :"
    input <- getLine
    
    -- Conversion de la chaîne de caractères en liste d'entiers
    let nombres = map read (words input) :: [Int]
    
    let nombresTries = quickSort nombres
    putStrLn "Voici la liste triée dans l'ordre croissant :"
    print nombresTries
```

---

### Explication détaillée

#### 1. L'algorithme `quickSort`
La logique repose sur la stratégie "diviser pour régner" :
*   **Le Pivot** : On prend le premier élément de la liste (`pivot`).
*   **Les partitions** : 
    *   On crée une liste `petits` contenant tous les éléments inférieurs ou égaux au pivot.
    *   On crée une liste `grands` contenant tous les éléments strictement supérieurs au pivot.
*   **La Récursion** : On trie à nouveau ces deux listes et on les assemble autour du pivot avec l'opérateur de concaténation `++`.

#### 2. La conversion des données (`map read (words input)`)
C'est une ligne très courante en Haskell pour traiter les entrées utilisateur :
*   **`words input`** : Découpe la chaîne de caractères au niveau des espaces pour créer une liste de mots (ex: `"5 2 9"` devient `["5", "2", "9"]`).
*   **`read`** : Transforme une chaîne de caractère en une valeur (ici en entier).
*   **`map`** : Applique la fonction `read` à chaque élément de la liste de mots.
*   **`:: [Int]`** : C'est une annotation de type nécessaire pour dire à Haskell : "Je veux que tu lises ces mots comme des entiers".

#### 3. Pourquoi c'est efficace en Haskell ?
Haskell excelle ici car la syntaxe des listes par compréhension (`[x | x <- reste, x <= pivot]`) ressemble presque mot pour mot à la définition mathématique d'un ensemble, ce qui rend le code extrêmement lisible comparé à une boucle `for` imbriquée.

---
