
La formule est : $$C = (F - 32) \times \frac{5}{9}$$

## 🌡️ HC1T7 - Tâche 7 : Conversion Fahrenheit/Celsius

```haskell
-- Définition de la fonction 'fToC'.
-- Elle prend un type a qui doit être 'Floating' (pour la division et les décimales)
-- et retourne le résultat en Celsius du même type.
fToC :: Floating a => a -> a
fToC fahrenheit = (fahrenheit - 32.0) * (5.0 / 9.0)

-- Bloc principal pour tester la fonction
main :: IO ()
main = do
    let tempF1 = 32.0   -- Point de congélation de l'eau
    let tempF2 = 212.0  -- Point d'ébullition de l'eau
    let tempF3 = 68.0   -- Température ambiante
    let tempF4 = 0.0    -- Zéro Fahrenheit
    
    putStrLn "--- Conversion Fahrenheit (F) vers Celsius (C) ---"
    
    putStrLn $ show tempF1 ++ "°F = " ++ show (fToC tempF1) ++ "°C (Point de congélation : 0°C)"
    putStrLn $ show tempF2 ++ "°F = " ++ show (fToC tempF2) ++ "°C (Point d'ébullition : 100°C)"
    putStrLn $ show tempF3 ++ "°F = " ++ show (fToC tempF3) ++ "°C"
    putStrLn $ show tempF4 ++ "°F = " ++ show (fToC tempF4) ++ "°C"
```

-----

## 🔬 Explication

1.  **Signature de Type** : `fToC :: Floating a => a -> a`

      * Nous utilisons la classe de types **`Floating a`** pour garantir que la fonction peut gérer les nombres à virgule flottante (`Float` ou `Double`). La conversion de température implique une **division par 9**, ce qui produit généralement des valeurs décimales.

2.  **La Formule en Haskell** : `(fahrenheit - 32.0) * (5.0 / 9.0)`

      * **Soustraction** : Nous soustrayons d'abord `32.0` de la température en Fahrenheit. Il est important d'utiliser des **littéraux flottants** (`32.0`, `5.0`, `9.0`) pour forcer l'arithmétique en virgule flottante. Si nous avions utilisé `32`, `5`, et `9` (qui sont des entiers), Haskell aurait pu effectuer une division entière, produisant un résultat incorrect.
      * **Multiplication** : Le résultat de la soustraction est ensuite multiplié par le facteur de conversion $(\frac{5}{9})$.

Cette fonction est une **fonction pure**, car elle ne dépend que de son argument d'entrée et ne provoque aucun effet secondaire.
