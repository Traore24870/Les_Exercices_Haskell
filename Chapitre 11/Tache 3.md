HC11T3 : Classe de type Container pour Box
---
### Le Code Source (Main.hs)

```haskell
-- Définition du type de données Box
data Box a = Box a deriving (Show, Eq)

-- Définition de la classe de type Container
-- 'f' est un constructeur de type (comme Box)
class Container f where
    isEmpty  :: f a -> Bool
    contains :: Eq a => a -> f a -> Bool
    replace  :: f a -> b -> f b

-- Implémentation de l'instance Container pour Box
instance Container Box where
    -- Une Box contient toujours un élément, donc elle n'est jamais vide
    isEmpty _ = False

    -- Vérifie si l'élément 'x' est celui dans la boîte
    contains x (Box val) = x == val

    -- Remplace le contenu actuel par une nouvelle valeur de type 'b'
    replace (Box _) newVal = Box newVal

-- Fonction principale pour tester l'implémentation
main :: IO ()
main = do
    let myBox = Box 42
    let emptyBox = Box "Haskell"
    
    putStrLn "--- Test de la Classe Container avec Box ---"
    
    -- Test de isEmpty
    putStrLn $ "Est-ce que myBox est vide ? " ++ show (isEmpty myBox)
    
    -- Test de contains
    putStrLn $ "Est-ce que myBox contient 42 ? " ++ show (contains 42 myBox)
    putStrLn $ "Est-ce que myBox contient 10 ? " ++ show (contains 10 myBox)
    
    -- Test de replace
    let newBox = replace myBox "Bonjour"
    putStrLn $ "Ancienne boîte : " ++ show myBox
    putStrLn $ "Nouvelle boîte après replace : " ++ show newBox
```

---

### Explication détaillée du code

#### 1. Le Type de Données `Box a`
Nous définissons un type simple appelé `Box`. C'est un **type polymorphe**, ce qui signifie qu'une boîte peut contenir n'importe quel type de donnée (`Int`, `String`, etc.). 
* `deriving (Show, Eq)` permet à Haskell d'afficher le contenu de la boîte et de comparer deux boîtes entre elles automatiquement.

#### 2. La Classe de Type `Container`
C'est ici que nous définissons l'interface demandée :
* **`f a`** : Ici, `f` représente le conteneur (dans notre cas, `Box`).
* **`isEmpty`** : Prend un conteneur et renvoie un booléen.
* **`contains`** : Notez la contrainte `Eq a =>`. Elle est nécessaire car pour vérifier si un élément est présent, Haskell doit être capable de comparer les valeurs avec l'opérateur `==`.
* **`replace`** : Cette fonction est intéressante car elle change le type du contenu. On passe d'un conteneur de type `a` à un conteneur de type `b`.



#### 3. L'Instance `Container Box`
C'est l'implémentation concrète pour notre type `Box` :
* **Logique de `isEmpty`** : Par définition, une `Box` telle que définie ici contient toujours une valeur. Nous retournons donc toujours `False`. Si nous avions utilisé un type comme `Maybe`, nous aurions pu retourner `True` pour `Nothing`.
* **Logique de `contains`** : On utilise le *pattern matching* `(Box val)` pour extraire la valeur et la comparer à `x`.
* **Logique de `replace`** : On ignore la valeur existante (symbole `_`) et on recrée une nouvelle `Box` avec la valeur `newVal`.

#### 4. Le `main`
La fonction `main` sert de démonstration. On y voit notamment que `replace` est très flexible : elle nous a permis de transformer une `Box Int` (contenant 42) en une `Box String` (contenant "Bonjour").
