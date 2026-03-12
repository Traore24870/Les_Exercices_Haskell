HC8T10 : Deriving Show pour Book
---
### Le Code Haskell

```haskell
-- 1. Définition du type Book avec la syntaxe d'enregistrement
-- La clause deriving (Show) génère automatiquement le code d'affichage
data Book = Book {
    title  :: String,
    author :: String,
    year   :: Int
} deriving (Show)

-- 2. Création d'une instance et affichage
main :: IO ()
main = do
    -- Création d'un livre
    let myBook = Book { 
                    title = "Le Petit Prince", 
                    author = "Antoine de Saint-Exupéry", 
                    year = 1943 
                 }
    
    -- Affichage direct grâce à l'instance Show
    print myBook

```

---

### Explication détaillée du code

#### 1. Le rôle de `deriving (Show)`

En Haskell, `Show` est une **classe de types** (typeclass). Elle définit une fonction nommée `show` qui convertit une donnée en `String`.

* En ajoutant `deriving (Show)`, vous demandez au compilateur d'écrire cette fonction pour vous.
* Le résultat sera formaté exactement comme la structure du code : `Book {title = "...", author = "...", year = ...}`.

#### 2. La fonction `print`

La fonction `print` est un raccourci très utilisé en Haskell. Elle équivaut à faire :
`putStrLn (show monObjet)`
Elle appelle automatiquement la méthode `show` fournie par notre dérivation avant d'envoyer le texte vers la console.

#### 3. Structure de l'enregistrement

* **`title` et `author**` : Utilisent le type `String` (listes de caractères).
* **`year`** : Utilise le type `Int` pour représenter l'année de publication de manière entière.

---
