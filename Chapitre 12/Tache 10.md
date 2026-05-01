HC12T10 : Module d’opérations mathématiques
---
```haskell
-- 1. Définition des fonctions (plus besoin de la déclaration "module")
addition :: Double -> Double -> Double
addition a b = a + b

soustraction :: Double -> Double -> Double
soustraction a b = a - b

multiplication :: Double -> Double -> Double
multiplication a b = a * b

division :: Double -> Double -> Maybe Double
division _ 0 = Nothing
division a b = Just (a / b)

-- 2. Ta fonction Main
main :: IO ()
main = do
    let x = 15.0
    let y = 3.0
    putStrLn "--- Test des opérations ---"
    putStrLn $ "Addition : " ++ show (addition x y)
    putStr "Division : "
    print (division x y)
```

### 1. Définition des fonctions (La Logique)
Chaque fonction est un petit "outil" mathématique indépendant :

*   **`addition :: Double -> Double -> Double`** : Cette ligne est la "signature". Elle indique que la fonction prend deux nombres décimaux (`Double`) et produit un troisième `Double`.
*   **`division :: Double -> Double -> Maybe Double`** : C'est la partie la plus avancée. On utilise **`Maybe`** pour gérer les erreurs proprement.
    *   **`Nothing`** : Si le deuxième nombre est `0`, la fonction répond "Rien", ce qui empêche le programme de planter.
    *   **`Just (a / b)`** : Si le calcul est possible, elle répond "Juste le résultat".

### 2. Le point d'entrée : `main`
C'est ici que l'exécution commence réellement :

*   **`do`** : Ce mot-clé permet d'enchaîner des actions (afficher du texte, lire une entrée) de manière séquentielle.
*   **`let x = 15.0`** : On crée une variable locale pour stocker une valeur. Contrairement au C ou au Java, on n'a pas besoin de préciser le type si Haskell peut le deviner.
*   **`putStrLn`** : Cette fonction affiche une chaîne de caractères suivie d'un retour à la ligne.
*   **`show`** : C'est une fonction essentielle qui transforme un nombre en texte (String) pour qu'il puisse être affiché.
*   **`print`** : C'est un raccourci qui combine `show` et `putStrLn`. C'est très utile pour afficher des types complexes comme le `Maybe` (qui affichera `Just 5.0` ou `Nothing`).

