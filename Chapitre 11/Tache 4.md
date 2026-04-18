HC11T4 : Instance Container pour Present
---

### Le Code Source (Main.hs)

```haskell
-- Définition du type Present
-- Un cadeau peut être soit "Wrapped" (emballé avec un contenu) soit "Empty"
data Present a = Wrapped a | Empty deriving (Show, Eq)

-- Définition de la classe de type Container (reprise de l'exercice précédent)
class Container f where
    isEmpty  :: f a -> Bool
    contains :: Eq a => a -> f a -> Bool
    replace  :: f a -> b -> f b

-- Implémentation de l'instance Container pour Present
instance Container Present where
    -- Un cadeau est vide s'il correspond au constructeur Empty
    isEmpty Empty = True
    isEmpty _     = False

    -- On ne peut trouver quelque chose que si le cadeau est Wrapped
    contains x (Wrapped val) = x == val
    contains _ Empty         = False

    -- Si on remplace le contenu d'un cadeau vide, il devient un cadeau emballé
    -- Si on remplace un cadeau déjà emballé, on change simplement son contenu
    replace _ newVal = Wrapped newVal

-- Exemples d'utilisation
main :: IO ()
main = do
    let gift = Wrapped "Montre"
    let noGift = Empty
    
    putStrLn $ "Est-ce que le cadeau est vide ? " ++ show (isEmpty gift)
    putStrLn $ "Est-ce que le cadeau vide est vide ? " ++ show (isEmpty noGift)
    
    putStrLn $ "Contient une montre ? " ++ show (contains "Montre" gift)
    
    let upgradedGift = replace noGift "Diamant"
    putStrLn $ "Après avoir rempli le cadeau vide : " ++ show upgradedGift
```

---

### Explication de l'implémentation

L'intérêt d'utiliser `Present` par rapport à `Box` est qu'il introduit une structure de contrôle pour les cas "vides", similaire au type standard `Maybe`.

#### 1. Gestion du vide (`isEmpty`)
Contrairement à la classe `Box` qui contient toujours une valeur, le type `Present` possède deux **constructeurs**. Nous utilisons le *pattern matching* pour distinguer les deux :
* Si c'est `Empty`, `isEmpty` renvoie `True`.
* Si c'est `Wrapped a`, il renvoie `False`.

#### 2. Recherche de contenu (`contains`)
La méthode `contains` doit gérer le cas où il n'y a rien à comparer :
* `contains x (Wrapped val)` : Compare `x` avec `val`.
* `contains _ Empty` : Retourne immédiatement `False` car on ne peut rien trouver dans un cadeau vide.

#### 3. Transformation (`replace`)
La fonction `replace` illustre la flexibilité des types en Haskell :
* Peu importe l'état initial (que le cadeau soit `Empty` ou déjà `Wrapped`), l'action de "remplacer" par une nouvelle valeur transforme le conteneur en un `Wrapped newVal`.
* Notez le changement de signature : on passe de `Present a` à `Present b`. Cela permet, par exemple, de remplacer un cadeau contenant un nombre (`Int`) par un cadeau contenant du texte (`String`).

