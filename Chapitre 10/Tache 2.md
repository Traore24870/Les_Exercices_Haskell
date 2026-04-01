HC10T2 : Classe de type Summable
---

### Code Source (Haskell)

```haskell
-- 1. Définition de la classe de type Summable
class Summable a where
    sumUp :: [a] -> a

-- 2. Implémentation de l'instance pour le type Int
instance Summable Int where
    sumUp []     = 0           -- Cas de base : la somme d'une liste vide est 0
    sumUp (x:xs) = x + sumUp xs -- Cas récursif : tête + somme du reste

-- 3. Fonction principale pour tester l'implémentation
main :: IO ()
main = do
    let nombres = [1, 2, 3, 4, 5] :: [Int]
    let resultat = sumUp nombres
    
    putStrLn "--- Test de la classe Summable ---"
    putStr "La somme de la liste [1, 2, 3, 4, 5] est : "
    print resultat
```

---

### Explication Détaillée

#### 1. La Classe de Type (`class Summable a`)
Une classe de type en Haskell est une sorte d'interface qui définit un ensemble de fonctions que les types membres doivent implémenter.
* **`a`** est une variable de type représentant n'importe quel type futur (Int, Float, etc.).
* **`sumUp :: [a] -> a`** : Cette signature impose que la fonction prenne une liste d'éléments de type `a` et renvoie une valeur unique de ce même type `a`.


#### 2. L'Instance pour `Int` (`instance Summable Int`)
C'est ici que nous définissons concrètement comment additionner des entiers.
* **Le cas de base (`sumUp [] = 0`)** : Il est crucial de définir ce qui se passe avec une liste vide pour arrêter la récursion. Pour l'addition, l'élément neutre est `0`.
* **Le cas récursif (`sumUp (x:xs) = x + sumUp xs`)** :
    * `(x:xs)` utilise le "pattern matching" pour séparer le premier élément (`x`) du reste de la liste (`xs`).
    * On additionne `x` au résultat de l'appel récursif sur `xs`.

#### 3. Fonctionnement du `main`
* Nous déclarons explicitement `[Int]` pour que le compilateur sache quelle instance de `Summable` utiliser.
* `print` est utilisé à la place de `putStrLn` car le résultat est un entier (`Int`) et non une chaîne de caractères (`String`).

### Remarque sur l'optimisation
Dans une application réelle, on utiliserait souvent une fonction d'ordre supérieur comme `foldl` ou `foldr` pour implémenter cette logique de manière plus concise :
```haskell
instance Summable Int where
    sumUp = foldl (+) 0
```
Cela produit exactement le même résultat que la version récursive détaillée ci-dessus.
