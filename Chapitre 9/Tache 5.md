HC9T5 : Type de données paramétrique avec syntaxe d’enregistrement
---
---

### Code Source (Haskell)

```haskell
-- 1. Définition du type Shape avec la syntaxe d'enregistrement
-- 'a' est le paramètre de type pour la couleur (ex: String, Int, ou un type Color)
data Shape a 
    = Circle { color :: a, radius :: Double }
    | Rectangle { color :: a, width :: Double, height :: Double }
    deriving (Show)

-- 2. Fonction principale main()
main :: IO ()
main = do
    -- Création d'un cercle avec une couleur de type String
    let myCircle = Circle { color = "Rouge", radius = 5.0 }
    
    -- Création d'un rectangle avec la même structure de couleur
    let myRect = Rectangle { color = "Bleu", width = 10.0, height = 20.0 }
    
    -- Utilisation de la fonction d'accès 'color' générée automatiquement
    putStrLn $ "La couleur du cercle est : " ++ show (color myCircle)
    putStrLn $ "La couleur du rectangle est : " ++ show (color myRect)
    
    -- Affichage complet des structures
    print myCircle
    print myRect
```

---

### Explication détaillée du code

* **`data Shape a`** : Nous définissons un type de données générique. Le paramètre `a` permet d'utiliser n'importe quel système de couleur (une simple chaîne de caractères `"Rouge"`, un code hexadécimal, ou un tuple RGB).
* **Syntaxe d'enregistrement `{ color :: a, ... }`** : 
    * Au lieu de simples arguments positionnels, nous nommons les champs.
    * Le champ `color` est présent dans les deux constructeurs (`Circle` et `Rectangle`).
    * **Avantage majeur** : Haskell crée automatiquement une fonction nommée `color`. Si vous passez n'importe quelle `Shape` à cette fonction, elle extraira la valeur du champ `color`.
* **Constructeurs multiples** :
    * `Circle` possède deux champs : `color` et `radius`.
    * `Rectangle` possède trois champs : `color`, `width` et `height`.
* **Flexibilité** : Comme le type est paramétrique, vous pourriez très bien définir une forme avec un identifiant numérique pour la couleur : `Circle { color = 255, radius = 1.0 }` (ici, `a` devient un `Int`).
