HC8T4 : Syntaxe d’enregistrement pour Employee
---
### Le Code Haskell

```haskell
-- 1. Définition du type Employee avec la syntaxe d'enregistrement
data Employee = Employee { 
    name              :: String, 
    experienceInYears :: Float 
} deriving (Show)

-- 2. Création de l'instance "richard"
richard :: Employee
richard = Employee { 
    name = "Richard", 
    experienceInYears = 7.5 
}

-- 3. Exemple d'utilisation dans le main
main :: IO ()
main = do
    putStrLn "Informations sur l'employé :"
    print richard
    
    -- Utilisation d'un getter automatique
    putStrLn $ "Années d'expérience : " ++ show (experienceInYears richard)

```

---

### Explication détaillée du code

#### 1. La structure `data Employee`

Contrairement à une simple liste d'arguments, l'utilisation des accolades `{ ... }` définit des **champs nommés**.

* **`name :: String`** : Définit un champ pour le nom.
* **`experienceInYears :: Float`** : Définit un champ pour l'expérience (le type `Float` est idéal ici car il accepte les nombres à virgule comme `7.5`).
* **`deriving (Show)`** : Indique à Haskell de générer automatiquement une représentation textuelle de l'objet pour pouvoir l'afficher avec `print`.

#### 2. L'instanciation de `richard`

Lorsqu'on crée `richard`, on utilise le nom des champs. L'avantage majeur est que **l'ordre n'importe plus** : vous auriez pu définir l'expérience avant le nom sans que cela ne pose d'erreur, tant que tous les champs sont présents.

#### 3. Les fonctions d'accès (Getters)

C'est la magie de la syntaxe d'enregistrement. Haskell crée "sous le capot" une fonction pour chaque champ. Par exemple :

* La fonction `experienceInYears` prend un `Employee` et renvoie un `Float`.
* Pour obtenir l'expérience de Richard, on écrit simplement : `experienceInYears richard`.

---
