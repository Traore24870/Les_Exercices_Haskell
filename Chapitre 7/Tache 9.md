HC7T9 : Définir une classe de type avec plusieurs instances
---

### Le Code Source (Haskell)

```haskell
-- 1. Définition du type Shape (pour l'instance)
data Shape = Circle Double | Rectangle Double Double

-- 2. Définition de la classe de type Describable
class Describable a where
    describe :: a -> String

-- 3. Instance pour le type Bool (Type natif)
instance Describable Bool where
    describe True  = "C'est une verite absolue."
    describe False = "C'est une affirmation fausse."

-- 4. Instance pour le type Shape (Type personnalise)
instance Describable Shape where
    describe (Circle r)      = "Un cercle parfait de rayon " ++ show r
    describe (Rectangle l h) = "Un rectangle de " ++ show l ++ " par " ++ show h

-- 5. Fonction principale de test
main :: IO ()
main = do
    putStrLn "--- Test de la classe Describable ---"

    -- Test avec Bool
    putStrLn $ "Bool (True)  : " ++ describe True
    putStrLn $ "Bool (False) : " ++ describe False

    -- Test avec Shape
    let myCircle = Circle 10.5
    let myRect   = Rectangle 4 2
    putStrLn $ "Shape (Circ) : " ++ describe myCircle
    putStrLn $ "Shape (Rect) : " ++ describe myRect

```

---

### Explication Détaillée

#### 1. La création de la classe (`class Describable a`)

C'est ici que l'on définit le "plan" (le contrat).

* **`class`** : Mot-clé pour créer une nouvelle classe de type.
* **`Describable a`** : Nous nommons la classe et déclarons une variable de type `a`.
* **`describe :: a -> String`** : C'est la signature obligatoire. N'importe quel type `a` qui veut être `Describable` **doit** fournir une fonction nommée `describe` qui prend ce type et retourne une `String`.

#### 2. L'instance pour `Bool`

Même si `Bool` est un type déjà défini dans le langage, vous pouvez lui ajouter des comportements supplémentaires. C'est la force du polymorphisme d'Haskell : on peut étendre les types existants sans modifier leur code source original.

#### 3. L'instance pour `Shape`

Ici, nous utilisons le **pattern matching** à l'intérieur de l'instance. La fonction `describe` se comporte différemment selon que la forme est un `Circle` ou un `Rectangle`. On peut dire que `describe` est une fonction surchargée de manière élégante.

#### 4. Utilisation dans le `main`

Remarquez que nous appelons la même fonction `describe` sur des types totalement différents (`Bool` et `Shape`). Le compilateur Haskell regarde le type de l'argument et choisit automatiquement la bonne implémentation à exécuter.

---

### Résumé des concepts

* **Classe de type** : Un ensemble de fonctions qu'un type doit implémenter.
* **Instance** : L'implémentation concrète de ces fonctions pour un type spécifique.
* **Polymorphisme** : La capacité d'une même fonction (`describe`) à s'adapter à différents types de données.

