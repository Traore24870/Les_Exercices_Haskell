HC12T8 : Fusionner deux listes triées
---
### Code Source (Main.hs)

```haskell
-- Fonction qui fusionne deux listes déjà triées
mergeLists :: [Int] -> [Int] -> [Int]
mergeLists [] ys = ys                         -- Si la 1ère liste est vide, on retourne la 2ème
mergeLists xs [] = xs                         -- Si la 2ème liste est vide, on retourne la 1ère
mergeLists (x:xs) (y:ys)
    | x <= y    = x : mergeLists xs (y:ys)    -- Si x est plus petit, on le garde et on continue
    | otherwise = y : mergeLists (x:xs) ys    -- Sinon, on garde y et on continue

main :: IO ()
main = do
    -- Définition de deux listes triées pour le test
    let listeA = [1, 3, 5, 7]
    let listeB = [2, 4, 6, 8, 10]
    
    putStrLn "Liste A : [1, 3, 5, 7]"
    putStrLn "Liste B : [2, 4, 6, 8, 10]"
    
    let resultat = mergeLists listeA listeB
    
    putStrLn "Résultat de la fusion :"
    print resultat
```

---

### Explication détaillée

#### 1. Le filtrage de motifs (Pattern Matching)
Nous traitons trois scénarios possibles :
*   **Les cas d'arrêt** : Si l'une des deux listes est vide (`[]`), il suffit de retourner l'autre liste telle quelle, car elle est déjà triée.
*   **Le cas général `(x:xs)` et `(y:ys)`** : Ici, `x` et `y` représentent les premiers éléments respectifs des deux listes, tandis que `xs` et `ys` représentent le reste.

#### 2. L'utilisation des Gardes (`|`)
Nous comparons les "têtes" des listes :
*   Si `x <= y` : On place `x` en tête de la nouvelle liste (grâce à l'opérateur `:` appelé *cons*) et on appelle récursivement `mergeLists` avec le reste de la première liste (`xs`) et la deuxième liste entière.
*   Sinon (`otherwise`) : On fait l'inverse avec `y`.



#### 3. Efficacité
Cette méthode est très performante car elle ne parcourt chaque élément qu'une seule fois. Contrairement à une simple concaténation suivie d'un tri complet, `mergeLists` profite du fait que les listes d'entrée sont **déjà triées**.

---
