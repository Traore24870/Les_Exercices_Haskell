HC3T3 - Tâche 3 : Convertir une couleur RGB en chaîne hexadécimale avec let
---
Pour cette tâche, nous allons utiliser le bloc **`let ... in ...`**. Il permet de définir des variables locales (des noms) pour stocker les résultats intermédiaires avant de les combiner.
Pour convertir un nombre en hexadécimal en Haskell, nous utilisons la fonction `showHex` du module `Numeric`.

---

## Code Source (Main.hs)

```haskell
import Numeric (showHex)
import Data.Char (toUpper)
import System.IO (hSetEncoding, stdout, utf8)

-- Fonction pour formater un seul nombre en 2 caractères hexa
formatHex :: Int -> String
formatHex n = 
    let s = showHex n ""
    in map toUpper (if length s == 1 then "0" ++ s else s)

-- Tâche 3 : Conversion RGB vers Hexadécimal
rgbToHex :: (Int, Int, Int) -> String
rgbToHex (r, g, b) = 
    let hexR = formatHex r
        hexG = formatHex g
        hexB = formatHex b
    in "#" ++ hexR ++ hexG ++ hexB

main :: IO ()
main = do
    hSetEncoding stdout utf8
    putStrLn $ "RGB (255, 0, 127) -> " ++ rgbToHex (255, 0, 127)
    putStrLn $ "RGB (0, 255, 64)  -> " ++ rgbToHex (0, 255, 64)

```

---

## Explications du code

### 1. L'utilisation de `let ... in`

Le bloc `let` définit les liaisons `hexR`, `hexG` et `hexB`. Le bloc `in` est l'endroit où ces variables sont utilisées pour produire le résultat final. C'est idéal pour décomposer un calcul complexe en étapes lisibles.

### 2. La fonction `formatHex`

* **`showHex`** : Convertit un nombre en base 16 (mais renvoie "f" au lieu de "0f").
* **Le `if` local** : Si la chaîne ne fait qu'un seul caractère (ex: "A"), on ajoute un "0" devant pour respecter le format standard des couleurs (ex: "0A").
* **`map toUpper`** : Convertit les lettres en majuscules (ex: "ff" devient "FF").

### 3. Le tuple `(Int, Int, Int)`

La fonction prend un seul argument qui est un **tuple** de trois entiers. C'est pourquoi on écrit `rgbToHex (r, g, b)` avec des parenthèses dans la définition de la fonction.

---

### Résultat attendu

```text
RGB (255, 0, 127) -> #FF007F
RGB (0, 255, 64)  -> #00FF40

```
