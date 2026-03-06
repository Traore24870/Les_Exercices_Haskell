HC7T8 : Parser une valeur avec Read
---
### Le Code Source (Haskell)

```haskell
-- 1. Définition du type Shape (avec deriving Show pour l'affichage)
data Shape = Circle Double | Rectangle Double Double
    deriving (Show, Eq)

-- 2. Implémentation manuelle de Read pour supporter un format spécifique
instance Read Shape where
    readsPrec _ input =
        case words input of
            ("Circle":r:rest) -> [(Circle (read r), unwords rest)]
            ("Rectangle":l:h:rest) -> [(Rectangle (read l) (read h), unwords rest)]
            _ -> [] -- Retourne une liste vide si le format est incorrect

-- 3. Fonction parseShape
-- Elle utilise la fonction standard 'read' pour convertir le String
parseShape :: String -> Shape
parseShape str = read str

-- 4. Point d'entrée pour les tests
main :: IO ()
main = do
    putStrLn "--- Test de la fonction parseShape ---"

    -- Test 1 : Parser un cercle
    let s1 = parseShape "Circle 15.0"
    putStr "Input 'Circle 15.0' -> Resultat : "
    print s1

    -- Test 2 : Parser un rectangle
    let s2 = parseShape "Rectangle 10.0 20.0"
    putStr "Input 'Rectangle 10.0 20.0' -> Resultat : "
    print s2

```

---

### Explication Détaillée

#### 1. Le rôle de `Read`

La classe `Read` est l'inverse de `Show`. Alors que `Show` transforme un objet en texte, `Read` tente de reconstruire l'objet à partir du texte. Dans notre instance personnalisée :

* **`words input`** : Découpe la chaîne en une liste de mots (ex: `"Circle 15.0"` devient `["Circle", "15.0"]`).
* **Pattern Matching** : On vérifie si le premier mot est "Circle" ou "Rectangle".
* **`read r`** : On délègue la lecture des nombres au parseur de `Double` déjà existant dans Haskell.

#### 2. La fonction `parseShape`

La fonction `parseShape` est une simple **enveloppe** (wrapper) autour de la fonction `read`.

* En Haskell, `read` est une fonction "poly-morphe de retour". Cela signifie qu'elle ne sait pas ce qu'elle doit retourner tant qu'on ne lui précise pas le type.
* Ici, comme la signature de `parseShape` indique qu'elle retourne un `Shape`, le compilateur comprend automatiquement qu'il doit utiliser l'instance `Read` de `Shape`.

#### 3. Attention aux erreurs (Runtime)

La fonction `read` est dite "partielle" : si vous lui passez une chaîne de caractères mal formée (ex: `"Triangle 5"`), le programme plantera avec une erreur.

