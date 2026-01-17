
HC3T1 - Tâche 1 : Vérifier si un nombre est positif, négatif ou nul
---
## Code Complet (Haskell)

```haskell
import System.IO (hSetEncoding, stdout, utf8)

-- Définition de la fonction avec conditions imbriquées
checkNumber :: Int -> String
checkNumber n = 
    if n > 0 
    then "Positif" 
    else if n < 0 
         then "Négatif" 
         else "Zéro"

-- Fonction principale pour exécuter les tests
main :: IO ()
main = do
    -- Configuration pour supporter les accents (é) dans la console
    hSetEncoding stdout utf8 
    
    -- Affichage des résultats
    putStrLn ("Test avec 5 : " ++ checkNumber 5)
    putStrLn ("Test avec -3 : " ++ checkNumber (-3))
    putStrLn ("Test avec 0 : " ++ checkNumber 0)

```

---

## Points Clés à Retenir

### 1. Structure Logique

Puisqu'il y a trois issues possibles, nous utilisons une structure en cascade. Si la première condition () est fausse, le programme entre dans le `else` qui contient lui-même un test pour différencier les deux cas restants ( ou ).

### 2. Syntaxe Importante

* **Signature `Int -> String**` : Précise que la fonction transforme un nombre entier en texte.
* **Parenthèses `(-3)**` : Indispensables en Haskell lors du passage d'un nombre négatif en argument pour éviter que le compilateur ne confonde le signe moins avec une opération de soustraction.
* **Concaténation `++**` : Permet de coller le texte descriptif avec le résultat renvoyé par la fonction.

### 3. Gestion de l'affichage

* **`putStrLn`** : Utilisé à la place de `print` pour afficher proprement les caractères accentués sans les guillemets de débogage.
* **`hSetEncoding`** : Résout l'erreur `invalid argument` en forçant le terminal à reconnaître l'UTF-8.

---
