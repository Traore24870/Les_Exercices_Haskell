## ✅ HC1T3 - Tâche 3 : Vérifier si un nombre est supérieur à 18

```haskell
-- Définition de la fonction 'greaterThan18'.
-- Elle prend un type a (qui doit être une instance de Ord pour la comparaison)
-- et retourne un Bool (True ou False).
greaterThan18 :: (Ord a, Num a) => a -> Bool
greaterThan18 n = n > 18

-- Bloc main pour tester la fonction
main :: IO ()
main = do
    let age1 = 25
    let age2 = 18
    let age3 = 15
    
    putStrLn "--- Vérification de la Majorité (Supérieur à 18) ---"
    
    putStrLn $ "greaterThan18(" ++ show age1 ++ ") = " ++ show (greaterThan18 age1) -- True
    putStrLn $ "greaterThan18(" ++ show age2 ++ ") = " ++ show (greaterThan18 age2) -- False (car 18 n'est PAS supérieur à 18)
    putStrLn $ "greaterThan18(" ++ show age3 ++ ") = " ++ show (greaterThan18 age3) -- False
```

-----

## 🔎 Explication

1.  **Signature de Type** : `greaterThan18 :: (Ord a, Num a) => a -> Bool`

      * **`(Ord a, Num a)`** : Cette contrainte de type est importante. Elle indique que l'argument `a` doit être un type qui peut être **ordonné** (`Ord`, pour utiliser l'opérateur `>`) et un type **numérique** (`Num`, pour pouvoir utiliser le nombre `18` dans l'expression).
      * **`a -> Bool`** : La fonction prend un argument de type `a` et retourne une valeur **booléenne** (`Bool`), c'est-à-dire soit `True`, soit `False`.

2.  **Définition de la Fonction** : `greaterThan18 n = n > 18`

      * L'opérateur de comparaison **`>`** (strictement supérieur à) évalue si la valeur de l'argument `n` est strictement plus grande que la constante `18`.
      * C'est une **fonction pure**, car le résultat dépend uniquement de son entrée (`n`) et ne produit aucun effet secondaire.
