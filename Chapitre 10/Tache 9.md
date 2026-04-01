HC10T9 : Classe de type MinMax
---
---

## Code Source (Haskell)

```haskell
-- 1. Définition de la classe de type MinMax
-- Cette classe définit deux valeurs "témoins" que chaque type doit posséder.
class MinMax a where
    minValue :: a
    maxValue :: a

-- 2. Implémentation de l'instance pour le type Int
-- Nous utilisons ici les constantes prédéfinies de Haskell pour les entiers.
instance MinMax Int where
    minValue = minBound  -- La plus petite valeur possible pour un Int
    maxValue = maxBound  -- La plus grande valeur possible pour un Int

-- 3. Fonction principale pour tester l'implémentation
main :: IO ()
main = do
    putStrLn "--- Test de la classe MinMax pour Int ---"
    
    putStr "Valeur minimale (minValue) : "
    print (minValue :: Int)
    
    putStr "Valeur maximale (maxValue) : "
    print (maxValue :: Int)
```

---

## Explication Détaillée

### 1. Des Méthodes sans Arguments
Remarquez la signature : `minValue :: a`. 
Contrairement à `showSimple :: a -> String`, il n'y a pas d'argument avant la flèche. En Haskell, cela signifie que `minValue` est une valeur fixe pour un type donné. C'est ce qu'on appelle souvent des **valeurs polymorphes**.

### 2. L'Instance `Int` et `Bounded`
Pour implémenter `MinMax` pour `Int`, nous nous appuyons sur la classe native `Bounded` de Haskell :
* **`minBound`** : Sur une architecture 64-bit, cela correspond généralement à $-2^{63}$.
* **`maxBound`** : Correspond à $2^{63} - 1$.
En liant nos méthodes `minValue` et `maxValue` à ces constantes, nous rendons notre classe compatible avec les limites matérielles du processeur.



### 3. L'importance de l'annotation de type
Dans le `main`, vous remarquerez l'écriture `(minValue :: Int)`. 
Comme `minValue` est polymorphe (elle peut être un `Int`, un `Char`, etc., si les instances existent), le compilateur a besoin de savoir laquelle vous souhaitez afficher. Sans cette précision, Haskell ne saurait pas s'il doit aller chercher le minimum d'un entier ou d'un autre type.

---

## Pourquoi est-ce utile ?
La classe `MinMax` est extrêmement utile pour l'écriture d'algorithmes génériques. Par exemple, si vous écrivez une fonction de recherche du plus petit élément dans une liste, vous pouvez initialiser votre variable de comparaison à `maxValue`. 

```haskell
-- Exemple d'usage théorique
trouverMinimum :: (MinMax a, Ord a) => [a] -> a
trouverMinimum [] = maxValue -- Si la liste est vide, on renvoie le plafond
trouverMinimum xs = minimum xs
```

Cela garantit que n'importe quelle valeur réelle de la liste sera inférieure ou égale à votre point de départ.
```
