HC7T2 : Implémenter une instance Ord pour un type personnalisé
---

### Le Code Source (Haskell)

```haskell
-- 1. Définition du type de données
data Color = Red | Green | Blue

-- 2. Instance Eq (Obligatoire avant d'implémenter Ord)
instance Eq Color where
    Red   == Red   = True
    Green == Green = True
    Blue  == Blue  = True
    _     == _     = False

-- 3. Implémentation manuelle de l'instance Ord
instance Ord Color where
    -- On définit la fonction compare qui renvoie LT (Less Than), EQ (Equal) ou GT (Greater Than)
    compare Red   Red   = EQ
    compare Red   _     = LT  -- Red est inférieur à tout le reste
    
    compare Green Red   = GT  -- Green est supérieur à Red
    compare Green Green = EQ
    compare Green Blue  = LT  -- Green est inférieur à Blue
    
    compare Blue  Blue  = EQ
    compare Blue  _     = GT  -- Blue est supérieur à tout le reste

-- 4. Fonction principale de test
main :: IO ()
main = do
    putStrLn "Tests de l'ordre (Ord) pour le type Color :"
    
    putStr "Est-ce que Red < Green ? "
    print (Red < Green)    -- Devrait afficher True
    
    putStr "Est-ce que Green < Blue ? "
    print (Green < Blue)   -- Devrait afficher True
    
    putStr "Est-ce que Blue > Red ? "
    print (Blue > Red)     -- Devrait afficher True
    
    putStr "Le plus petit entre Green et Blue est : "
    -- Note : On ne peut pas 'print' directement les couleurs sans instance Show, 
    -- donc on teste la logique :
    if min Green Blue == Green then putStrLn "Green" else putStrLn "Blue"

```

---

### Explication Détaillée

#### 1. La dépendance `Eq`

En Haskell, pour qu'un type soit ordonnable (`Ord`), il doit obligatoirement être comparable en égalité (`Eq`). C'est pourquoi nous gardons l'instance `Eq` du premier exercice.

#### 2. La fonction `compare`

La méthode la plus efficace pour implémenter `Ord` est de définir la fonction `compare`. Elle prend deux valeurs et retourne un type spécial appelé `Ordering`, qui peut être :

* `LT` (Less Than) : Plus petit.
* `EQ` (Equal) : Égal.
* `GT` (Greater Than) : Plus grand.

Dans notre code :

* Nous avons fixé `Red` comme étant `LT` (inférieur) dès qu'il est comparé à autre chose que lui-même.
* Nous avons fixé `Blue` comme étant `GT` (supérieur) dès qu'il est comparé à autre chose.
* Cela crée naturellement la chaîne : **Red < Green < Blue**.

#### 3. Les opérateurs dérivés

L'avantage de définir `compare` est que Haskell génère **automatiquement** tous les autres opérateurs pour vous : `<`, `>`, `<=`, `>=`, `min` et `max`. Vous n'avez pas besoin de les écrire un par un.

#### 4. Le Pattern Matching

Remarquez l'utilisation du caractère `_` (underscore). Par exemple, `compare Red _ = LT` permet de dire de façon concise : "Si le premier élément est Red et que ce n'est pas le cas d'égalité traité juste au-dessus, alors Red est forcément plus petit".

