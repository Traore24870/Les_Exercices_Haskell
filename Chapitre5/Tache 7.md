HC5T7 : L’opérateur $
---
### Code Source Complet

```haskell
-- Définition du résultat avec sa signature de type
-- On utilise Integer pour éviter tout débordement, bien qu'Int suffise ici.
result :: Integer
result = sum $ map (*2) $ filter (>3) [1..10]

-- Fonction principale pour exécuter le programme
main :: IO ()
main = do
    putStrLn "Le résultat du calcul (sum $ map (*2) $ filter (>3) [1..10]) est :"
    print result

```

---

### Analyse des composants

#### 1. La Signature de Type (`result :: Integer`)

En Haskell, il est de bonne pratique de déclarer explicitement le type. Ici, `Integer` indique que `result` est un nombre entier de précision arbitraire. Le double deux-points `::` se lit "est de type".

#### 2. L'Opérateur `$` (Application de fonction)

Comme expliqué précédemment, l'opérateur `$` remplace les parenthèses. Sans lui, le code ressemblerait à ceci :
`result = sum (map (*2) (filter (>3) [1..10]))`

L'image ci-dessous illustre comment les fonctions s'emboîtent ou s'enchaînent dans ce type d'expression :

#### 3. La fonction `main`

* **`main :: IO ()`** : C'est le point d'entrée de tout programme Haskell exécutable. Le type `IO ()` indique que la fonction effectue des opérations d'entrée/sortie (comme afficher du texte).
* **`putStrLn`** : Affiche une chaîne de caractères suivie d'un retour à la ligne.
* **`print`** : Convertit une valeur (ici notre `Integer`) en chaîne de caractères et l'affiche. C'est un raccourci pour `putStrLn (show result)`.


