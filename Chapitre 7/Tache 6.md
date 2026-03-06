HC7T6 : Utiliser Integral et Floating
---
```haskell
-- 1. Fonction de calcul de circonférence
-- Elle accepte n'importe quel type 'a' qui est Numeric
-- Mais elle doit convertir 'a' en un type flottant pour utiliser 'pi'
circleCircumference :: (Real a) => a -> Double
circleCircumference radius = 2 * pi * realToFrac radius

-- 2. Fonction principale pour tester avec Integral et Floating
main :: IO ()
main = do
    putStrLn "--- Test de la fonction circleCircumference ---"

    -- Test avec un type Floating (Double)
    let radiusFloat = 5.5 :: Double
    putStr "Rayon flottant (5.5) -> Circonférence : "
    print (circleCircumference radiusFloat)

    -- Test avec un type Integral (Int)
    let radiusInt = 10 :: Int
    putStr "Rayon entier (10) -> Circonférence : "
    print (circleCircumference radiusInt)

    -- Test avec un type Integer (Grand entier)
    let radiusBig = 100 :: Integer
    putStr "Rayon Integer (100) -> Circonférence : "
    print (circleCircumference radiusBig)

```

---

### Explication Détaillée

#### 1. La contrainte `Real a`

Plutôt que de lister `(Integral a, Floating a)`, ce qui est impossible car un type ne peut pas être les deux à la fois, on utilise la contrainte **`Real a`**.

* La classe `Real` est la "classe parente" qui englobe à la fois les entiers (`Int`, `Integer`) et les nombres décimaux (`Double`, `Float`).
* Cela permet à notre fonction d'accepter n'importe quel nombre réel en entrée.

#### 2. La conversion avec `realToFrac`

C'est la pièce maîtresse du code. En Haskell, vous ne pouvez pas multiplier un `Int` par un `Double` (comme `pi`) directement.

* **`pi`** appartient à la classe `Floating`.
* **`realToFrac`** est une fonction très flexible qui convertit n'importe quel type `Real` vers n'importe quel type `Fractional` (comme `Double`).
* Sans cette conversion, le compilateur renverrait une erreur de type car il refuserait de mélanger des "pommes" (entiers) et des "oranges" (flottants).
  

### Résumé des classes numériques utilisées

| Classe | Types inclus | Usage ici |
| --- | --- | --- |
| **`Real`** | `Int`, `Double`, `Integer` | Le type du rayon en entrée. |
| **`Floating`** | `Double`, `Float` | Requis pour utiliser la constante `pi`. |
| **`realToFrac`** | N/A (Fonction) | Le "pont" pour transformer l'entrée en nombre décimal. |

