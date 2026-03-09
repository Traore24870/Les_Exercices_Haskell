HC8T5 : Syntaxe d’enregistrement pour Person
---
### Le Code Haskell

```haskell
-- 1. Définition du type Person avec la syntaxe d'enregistrement
data Person = Person { 
    name       :: String, 
    age        :: Int, 
    isEmployed :: Bool 
} deriving (Show)

-- 2. Création de person1 (employée)
person1 :: Person
person1 = Person { 
    name = "Alice", 
    age = 30, 
    isEmployed = True 
}

-- 3. Création de person2 (sans emploi)
person2 :: Person
person2 = Person { 
    name = "Bob", 
    age = 22, 
    isEmployed = False 
}

main :: IO ()
main = do
    putStrLn "Détails de Person 1 :"
    print person1
    putStrLn "\nDétails de Person 2 :"
    print person2

```

---

### Explication détaillée du code

#### 1. Le type `Bool` pour l'emploi

Le champ `isEmployed :: Bool` est parfait pour représenter une situation binaire (vrai/faux). En Haskell, les valeurs booléennes sont **`True`** ou **`False`** (attention à la majuscule, elle est obligatoire).

#### 2. Avantages de la Syntaxe d'Enregistrement

Comme nous l'avons vu précédemment, cette syntaxe offre une clarté immédiate. Si vous aviez simplement écrit `data Person = Person String Int Bool`, il serait facile de confondre l'ordre des arguments. Ici, `isEmployed = True` ne laisse aucune place à l'ambiguïté.

#### 3. Manipulation des données

Haskell génère automatiquement des fonctions d'accès. Par exemple, si vous voulez vérifier si quelqu'un travaille, vous pouvez simplement appeler la fonction `isEmployed` :

```haskell
checkStatus :: Person -> String
checkStatus p = if isEmployed p 
                then name p ++ " a un emploi." 
                else name p ++ " est à la recherche d'un emploi."

```

---

### Pour aller plus loin

Vous avez maintenant une solide base sur les types en Haskell :

* **Alias de type** (`type`) pour la lisibilité.
* **Types Algébriques** (`data` avec `|`) pour les choix multiples.
* **Syntaxe d'enregistrement** (`{}`) pour les structures de données complexes.
