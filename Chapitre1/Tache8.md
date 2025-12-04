La fonction `applyTwice` prend une fonction ($f$) et une valeur ($x$), et calcule $f(f(x))$.

## 🔄 Fonction `applyTwice`

```haskell
-- Définition de la fonction 'applyTwice'.
-- Signature : Elle prend une fonction (f) qui mappe a -> a, et une valeur (x) de type a.
-- Elle retourne la valeur résultante, qui est aussi de type a.
applyTwice :: (a -> a) -> a -> a
applyTwice f x = f (f x)

-- Bloc principal pour tester la fonction
main :: IO ()
main = do
    -- 1. Définition des fonctions de test
    let increment :: Int -> Int
        increment n = n + 1
        
    let double :: Int -> Int
        double n = n * 2
        
    let initialValue = 5
    
    putStrLn "--- Application d'une Fonction Deux Fois (applyTwice) ---"
    
    -- Test 1 : Appliquer 'increment' deux fois (5 -> 6 -> 7)
    let result1 = applyTwice increment initialValue
    putStrLn $ "Appliquer 'increment' deux fois à " ++ show initialValue ++ " : " ++ show result1
    -- Résultat attendu : 7 (5 + 1 + 1)
    
    -- Test 2 : Appliquer 'double' deux fois (5 -> 10 -> 20)
    let result2 = applyTwice double initialValue
    putStrLn $ "Appliquer 'double' deux fois à " ++ show initialValue ++ " : " ++ show result2
    -- Résultat attendu : 20 (5 * 2 * 2)
    
    -- Test 3 : Utilisation directe d'une lambda expression
    -- (Ajouter 10 deux fois : 100 -> 110 -> 120)
    let result3 = applyTwice (\n -> n + 10) 100
    putStrLn $ "Appliquer '(+10)' deux fois à 100 : " ++ show result3
    -- Résultat attendu : 120
```

-----

## 💡 Explication Détaillée

### 1\. Fonction d'Ordre Supérieur

`applyTwice` est une **fonction d'ordre supérieur** (Higher-Order Function) car elle prend une autre fonction (`f`) comme argument.

### 2\. Signature de Type

```haskell
applyTwice :: (a -> a) -> a -> a
```

  * **`(a -> a)`** : Le premier argument est une fonction qui prend une valeur de type `a` et retourne une valeur du même type `a`. C'est crucial, car la sortie de la première application de $f$ doit être compatible avec l'entrée de la deuxième application.
  * **`-> a`** : Le deuxième argument est la valeur d'entrée ($x$), de type `a`.
  * **`-> a`** : La fonction retourne la valeur finale, de type `a`.

### 3\. Définition

```haskell
applyTwice f x = f (f x)
```

La définition est extrêmement simple et exprime directement l'intention :

1.  L'expression **la plus à l'intérieur**, `f x`, est évaluée en premier.
2.  Le résultat de `f x` est ensuite passé comme argument à l'appel de fonction **extérieur**, `f (...)`.

Cette définition est l'équivalent direct de la composition de fonction $f \circ f$ appliquée à $x$, soit $(f . f) x$.
