HC7T4 : Type personnalisé avec Show et Read
---
### Le Code Source (Haskell)

```haskell
-- 1. Définition du type de données Shape
-- Circle prend un rayon (Double)
-- Rectangle prend une largeur et une hauteur (Double, Double)
data Shape = Circle Double | Rectangle Double Double
    deriving (Eq) -- Utile pour comparer les résultats lors des tests

-- 2. Implémentation de l'instance Show
-- Définit comment transformer une forme en chaîne de caractères (String)
instance Show Shape where
    show (Circle r)      = "Circle with radius " ++ show r
    show (Rectangle l h) = "Rectangle " ++ show l ++ "x" ++ show h

-- 3. Implémentation de l'instance Read
-- Définit comment recréer une forme à partir d'un String
instance Read Shape where
    readsPrec _ input =
        case words input of
            ("Circle":"with":"radius":r:rest) ->
                [(Circle (read r), unwords rest)]
            ("Rectangle":dims:rest) ->
                let (l, h) = parseDims dims
                in [(Rectangle l h, unwords rest)]
            _ -> [] -- Échec de la lecture
        where
            -- Fonction utilitaire pour parser "10.0x20.0"
            parseDims s = 
                let (lStr, hStr) = break (== 'x') s
                in (read lStr, read (tail hStr))

-- 4. Fonction principale de test
main :: IO ()
main = do
    let c = Circle 5.5
    let r = Rectangle 10.0 20.0

    putStrLn "--- Test de Show ---"
    print c
    print r

    putStrLn "\n--- Test de Read ---"
    -- On simule la lecture d'une chaîne de caractères
    let inputStr = "Circle with radius 5.5"
    let parsedShape = read inputStr :: Shape
    
    if parsedShape == c 
        then putStrLn $ "Succès ! Lu : " ++ show parsedShape
        else putStrLn "Erreur de lecture."

```

---

### Explication Détaillée

#### 1. Les Constructeurs avec Arguments

Contrairement aux couleurs (`Red`, `Green`), les constructeurs de `Shape` transportent des données (**Double**).

* `Circle 5.5` stocke une valeur.
* `Rectangle 10.0 20.0` en stocke deux.

#### 2. L'instance `Show`

La fonction `show` est le "toString" de Haskell.

* Nous utilisons le **pattern matching** pour extraire les valeurs numériques (`r`, `l`, `h`).
* Nous concaténons (`++`) du texte personnalisé pour rendre l'affichage plus humain que le format par défaut de Haskell.

#### 3. L'instance `Read` (Le défi)

L'implémentation manuelle de `Read` est plus complexe car elle doit gérer les erreurs de saisie.

* **`readsPrec`** : C'est la fonction coeur de `Read`. Elle retourne une liste de paires `[(Valeur, ResteDuTexte)]`. Si la liste est vide, la lecture a échoué.
* **`words input`** : Découpe la phrase en mots pour faciliter l'analyse.
* **`read r`** : Nous réutilisons la fonction `read` existante pour convertir les chaînes de caractères en nombres `Double`.

#### 4. Annotation de type `:: Shape`

Dans le `main`, vous remarquerez `read inputStr :: Shape`. C'est crucial : comme `read` est générique, Haskell a besoin qu'on lui dise explicitement quel type d'objet nous espérons obtenir de la chaîne de caractères.

---
