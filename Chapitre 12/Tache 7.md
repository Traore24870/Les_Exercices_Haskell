HC12T7 : Calculer l’aire d’un cercle
---
### Code Source (Main.hs)

```haskell
-- Fonction qui calcule l'aire d'un cercle : A = pi * r^2
calculateCircleArea :: Double -> Double
calculateCircleArea radius = pi * radius * radius

main :: IO ()
main = do
    putStrLn "--- Calcul de l'aire d'un cercle ---"
    putStrLn "Entrez le rayon du cercle :"
    
    -- Lecture et conversion de l'entrée en Double (nombre à virgule)
    input <- getLine
    let radius = read input :: Double
    
    -- Vérification si le rayon est positif
    if radius < 0
        then putStrLn "Erreur : Le rayon ne peut pas être négatif."
        else do
            let area = calculateCircleArea radius
            putStr "L'aire du cercle avec un rayon de "
            putStr (show radius)
            putStr " est : "
            print area
```

---

### Explication détaillée

#### 1. Le type `Double`
Contrairement aux exercices précédents qui utilisaient des `Int` (entiers), nous utilisons ici le type **`Double`**. C'est le type standard en Haskell pour représenter les nombres réels avec une grande précision décimale, indispensable pour des calculs géométriques.

#### 2. La constante `pi`
Haskell fournit nativement la valeur de $\pi$ au sein de la classe de types `Floating`. Vous n'avez pas besoin de définir `3.14159...` manuellement ; le langage utilise la précision maximale supportée par votre processeur.

#### 3. La logique de la fonction
La formule mathématique est $Area = \pi \times r^2$. En Haskell, l'expression `pi * radius * radius` est directe. Vous pourriez aussi écrire `pi * radius**2`, où `**` est l'opérateur de puissance pour les nombres flottants.

#### 4. Conversion et sécurité
*   **`read input :: Double`** : Cette commande tente d'interpréter la chaîne de caractères tapée par l'utilisateur comme un nombre décimal.
*   **La condition `if radius < 0`** : En programmation, il est toujours bon de vérifier la cohérence des données. Un rayon négatif n'ayant pas de sens physique, le programme affiche un message d'erreur.

---

