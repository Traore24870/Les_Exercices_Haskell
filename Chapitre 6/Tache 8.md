HC6T8 : Filtrer les nombres pairs
---
### Code Source Complet

Voici le code incluant la fonction de filtrage, sa signature de type et un programme de test.

```haskell
-- Signature : prend une liste d'entiers et retourne une liste d'entiers
filterPairs :: [Int] -> [Int]

-- Cas de base : une liste vide retourne une liste vide
filterPairs [] = []

-- Cas récursif avec gardes
filterPairs (x:xs)
    | x `mod` 2 == 0 = x : filterPairs xs  -- Si pair, on garde x et on continue
    | otherwise      = filterPairs xs      -- Sinon, on passe au suivant
    
main :: IO ()
main = do
    let maListe = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    putStr "Liste originale : "
    print maListe
    putStr "Nombres pairs uniquement : "
    print (filterPairs maListe)

```

---

### Explication Technique

#### 1. L'opérateur `mod`

L'expression `x mod 2 == 0` vérifie si le reste de la division entière de `x` par 2 est nul. C'est le test mathématique standard pour déterminer la parité.

#### 2. Les Gardes (`|`)

Les gardes permettent de tester plusieurs conditions sur un même motif :

* **Première garde :** Si la condition est vraie, on utilise l'opérateur de construction `:` pour ajouter `x` au résultat de l'appel récursif sur le reste de la liste (`xs`).
* **`otherwise` :** Si la condition est fausse (nombre impair), on ignore simplement `x` et on renvoie le résultat de l'appel récursif sur `xs`.

#### 3. Approche avec la fonction `filter`

Dans un projet réel, au lieu de réécrire la récursion, on utiliserait la fonction d'ordre supérieur `filter` déjà intégrée à Haskell :

```haskell
filterPairsDirect :: [Int] -> [Int]
filterPairsDirect = filter even

```
