-- La formule est C = (F - 32) * 5/9.
fToC :: Double -> Double
fToC fahrenheit = (fahrenheit - 32.0) * (5.0 / 9.0)

-- | Fonction main pour tester fToC.
main :: IO ()
main = do
    putStrLn "--- Tâche 7 : Fahrenheit -> Celsius ---"
    -- Test 1 : Point de congélation (32°F = 0°C)
    let f1 = 32.0
        c1 = fToC f1
    putStrLn $ show f1 ++ " °F est égal à " ++ show c1 ++ " °C."

    -- Test 2 : Température ambiante (68°F = 20°C)
    let f2 = 68.0
        c2 = fToC f2
    putStrLn $ show f2 ++ " °F est égal à " ++ show c2 ++ " °C."

    -- Test 3 : Point d'ébullition (212°F = 100°C)
    let f3 = 212.0
        c3 = fToC f3
    putStrLn $ show f3 ++ " °F est égal à " ++ show c3 ++ " °C."

========Explication du code=======

    fToC :: Double -> Double Signature de Type Indique que la fonction fToC prend un nombre à virgule (Double) comme température en Fahrenheit et retourne un nombre à virgule (Double) comme température en Celsius.
    
 fToC fahrenheit = ... Définition Définit le corps de la fonction. Le terme fahrenheit est le nom de la variable (l'argument) qui reçoit la valeur d'entrée.
 
 (fahrenheit - 32.0) Étape 1 du Calcul Soustrait 32 (le décalage entre les deux échelles) de la température en Fahrenheit. Le .0 assure que le calcul reste en nombre décimal (Double).
 
  (5.0 / 9.0) Étape 2 du Calcul Multiplie le résultat de l'étape 1 par la fraction de conversion \frac{5}{9}. Les .0 sur 5.0 et 9.0 garantissent que la division et la multiplication sont effectuées en virgule flottante pour obtenir un résultat précis.

  
