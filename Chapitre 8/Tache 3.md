HC8T3 : Types algébriques et fonctions
---

```haskell
-- 1. Définition du type Shape
-- Un cercle a un rayon (Float)
-- Un rectangle a une largeur et une hauteur (Float Float)
data Shape = Circle Float 
           | Rectangle Float Float
           deriving (Show)

-- 2. Fonction de calcul de l'aire avec filtrage par motif (pattern matching)
area :: Shape -> Float
area (Circle r)      = pi * r * r
area (Rectangle l h) = l * h

-- 3. Programme principal pour les calculs demandés
main :: IO ()
main = do
    let monCercle    = Circle 5.0
    let monRectangle = Rectangle 10.0 5.0
    
    putStrLn $ "Aire du cercle (r=5): " ++ show (area monCercle)
    putStrLn $ "Aire du rectangle (10x5): " ++ show (area monRectangle)

```

---

### Explication détaillée

#### Le type `Shape` (Somme de types)

Le symbole `|` se lit "**ou**". Une valeur de type `Shape` est soit un `Circle`, soit un `Rectangle`.

* `Circle` est un constructeur qui "emballe" un nombre flottant (le rayon).
* `Rectangle` est un constructeur qui "emballe" deux nombres flottants (longueur et largeur).

#### Le Pattern Matching dans `area`

C'est la force de Haskell. Au lieu d'utiliser des `if/else`, on définit la fonction `area` en ouvrant directement les "boîtes" :

* **Cas `Circle r` :** On extrait la valeur `r` et on applique la formule $\pi r^2$. Haskell fournit la constante `pi` par défaut.
* **Cas `Rectangle l h` :** On extrait les deux valeurs et on les multiplie.

#### Précision sur les calculs

* Pour le cercle de rayon 5 : $Area = \pi \times 5^2 \approx 78.54$
* Pour le rectangle 10x5 : $Area = 10 \times 5 = 50.0$

---
