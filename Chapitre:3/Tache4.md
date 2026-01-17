HC3T4 - Tâche 4 : Calculer l'aire d'un triangle avec la formule de Héron
---
Pour cette tâche, nous utilisons la **formule de Héron**, qui est idéale pour calculer l'aire d'un triangle dont on connaît la longueur des trois côtés (,  et ). Le bloc `let` est ici parfait pour calculer d'abord le demi-périmètre (), puis l'utiliser dans la formule finale.

---

## Code Source (Main.hs)

```haskell
import System.IO (hSetEncoding, stdout, utf8)

-- Tâche 4 : Calcul de l'aire avec la formule de Héron
triangleArea :: Float -> Float -> Float -> Float
triangleArea a b c =
    let s = (a + b + c) / 2
    in sqrt (s * (s - a) * (s - b) * (s - c))

main :: IO ()
main = do
    hSetEncoding stdout utf8
    -- Affichage des résultats avec 2 décimales
    putStrLn $ "Aire triangle (3, 4, 5) : " ++ show (triangleArea 3 4 5)
    putStrLn $ "Aire triangle (7, 8, 9) : " ++ show (triangleArea 7 8 9)

```

---

## Explications Techniques

### 1. La Formule de Héron

La formule se décompose en deux étapes :

1. **Le demi-périmètre ()** : 
2. **L'aire ()** : 

### 2. L'usage de `let ... in`

En Haskell, `let` permet de créer une variable locale `s`. Cela évite de devoir réécrire `(a + b + c) / 2` quatre fois à l'intérieur de la fonction `sqrt`. Cela rend le code plus propre et plus performant.

### 3. Le type `Float`

Contrairement aux tâches précédentes qui utilisaient des `Int`, nous utilisons ici `Float` car le calcul d'une racine carrée (`sqrt`) et d'une division par 2 produit presque toujours des nombres à virgule.

---

### Résultat attendu

```text
Aire triangle (3, 4, 5) : 6.0
Aire triangle (7, 8, 9) : 26.832815

```

 **Note :** Pour le triangle (3, 4, 5), le résultat est exactement 6 car il s'agit d'un triangle rectangle ().
