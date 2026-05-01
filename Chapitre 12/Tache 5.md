HC12T5 : Vérification de palindrome
---
### Code Source (Main.hs)

```haskell
-- Fonction qui vérifie si une chaîne est un palindrome
isPalindrome :: String -> Bool
isPalindrome str = str == reverse str

main :: IO ()
main = do
    putStrLn "Entrez un mot pour vérifier s'il est un palindrome :"
    -- Lecture de l'entrée utilisateur
    input <- getLine
    
    -- Vérification et affichage du résultat
    if isPalindrome input
        then putStrLn "Oui, c'est un palindrome !"
        else putStrLn "Non, ce n'est pas un palindrome."
```

---

### Explication détaillée

#### 1. La fonction `isPalindrome`
*   **Signature (`String -> Bool`)** : Elle prend une chaîne en entrée et retourne un Booléen (`True` ou `False`).
*   **`reverse`** : C'est une fonction intégrée à Haskell qui inverse l'ordre des éléments d'une liste (et donc d'une chaîne).
*   **L'opérateur `==`** : Il compare la chaîne originale avec sa version inversée. Si elles sont identiques, c'est un palindrome.

#### 2. L'action `getLine`
C'est la fonction standard pour lire du texte depuis le terminal.
*   **L'opérateur `<-`** : Contrairement au `let`, on utilise `<-` pour extraire la valeur d'une action d'entrée/sortie (`IO String`). Cela permet de récupérer ce que l'utilisateur a tapé pour le stocker dans la variable `input`.

#### 3. La structure `if ... then ... else`
En Haskell, le `else` est **obligatoire**. Comme Haskell est un langage d'expressions, chaque `if` doit obligatoirement retourner une valeur ou une action, peu importe le résultat du test.

---

### Amélioration : Gérer la casse et les espaces
Si vous tapez "Radar", le programme dira que ce n'est pas un palindrome car 'R' est différent de 'r'. Pour rendre le programme plus "intelligent", on peut normaliser l'entrée avec les fonctions du module `Data.Char` :

```haskell
import Data.Char (toLower, isAlphaNum)

isPalindromeSmart :: String -> Bool
isPalindromeSmart str = 
    let cleanStr = map toLower (filter isAlphaNum str)
    in cleanStr == reverse cleanStr
```
*   **`filter isAlphaNum`** : Enlève les espaces et la ponctuation.
*   **`map toLower`** : Met tout en minuscules.

