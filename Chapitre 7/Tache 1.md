
HC7T1 : Implémenter une instance Eq pour un type personnalisé
---
```haskell
-- 1. Définition du type de données
data Color = Red | Green | Blue

-- 2. Implémentation manuelle de l'instance Eq
instance Eq Color where
    Red   == Red   = True
    Green == Green = True
    Blue  == Blue  = True
    _     == _     = False

-- 3. Fonction principale (le point d'entrée unique)
main :: IO ()
main = do
    let c1 = Red
    let c2 = Red
    let c3 = Blue

    putStrLn "Tests d'egalite pour le type Color :"
    
    putStr "Est-ce que Red == Red ? "
    print (c1 == c2)
    
    putStr "Est-ce que Red == Blue ? "
    print (c1 == c3)
    
    putStr "Est-ce que Green /= Blue ? "
    print (Green /= Blue)
---

```
### Explication Détaillée

#### Le Type de Données (`data Color`)

Nous créons un type nommé `Color`. C'est un type **somme** (ou énumération) avec trois constructeurs : `Red`, `Green`, et `Blue`. À ce stade, Haskell sait que ces trois choses existent, mais il ne sait pas comment les comparer, les afficher ou les trier.

#### L'Instance `Eq`

C'est ici que nous définissons la logique de comparaison.

* **`instance Eq Color where`** : Cette ligne déclare que le type `Color` appartient désormais à la classe de type `Eq` (pour "Equality").
* **Le Pattern Matching** : Nous définissons l'opérateur `==`. Les trois premières lignes comparent les constructeurs identiques. Si Haskell voit `Red == Red`, il suit la règle et renvoie `True`.
* **Le Joker (`_`)** : La ligne `_ == _ = False` est essentielle. Elle signifie : "pour n'importe quelle autre combinaison non listée au-dessus, le résultat est faux".

#### La fonction `main`

* **`print`** : Cette fonction est utilisée pour afficher le résultat des booléens (`True` ou `False`).
* **L'opérateur `/=**` : Vous remarquerez que nous n'avons pas implémenté l'opérateur "différent de" (`/=`). C'est l'un des avantages de Haskell : dans la définition de la classe `Eq`, `/=` est défini par défaut comme l'inverse de `==`. En définissant `==`, vous obtenez `/=` gratuitement !

---

