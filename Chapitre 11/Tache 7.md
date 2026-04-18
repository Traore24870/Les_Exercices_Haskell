HC11T7 : Instance Ord pour Box
---
### Le Code Source (Main.hs)

```haskell
-- Définition du type Box
data Box a = Box a deriving (Eq)

-- On personnalise l'affichage pour mieux voir les tests
instance Show a => Show (Box a) where
    show (Box x) = "Box(" ++ show x ++ ")"

-- Implémentation manuelle de l'instance Ord
instance Ord a => Ord (Box a) where
    -- On implémente compare qui renvoie un type Ordering (LT, EQ, ou GT)
    compare (Box x) (Box y) = compare x y

-- Fonction principale de test
main :: IO ()
main = do
    let b1 = Box 10
    let b2 = Box 20
    let b3 = Box 10
    
    putStrLn "--- Comparaisons de Box ---"
    putStrLn $ "b1 = " ++ show b1
    putStrLn $ "b2 = " ++ show b2
    
    -- Utilisation de compare directement
    putStrLn $ "Résultat de compare b1 b2 : " ++ show (compare b1 b2)
    
    -- Utilisation des opérateurs dérivés de compare (<, >, <=, >=)
    putStrLn $ "Est-ce que b1 < b2 ? "  ++ show (b1 < b2)
    putStrLn $ "Est-ce que b1 > b2 ? "  ++ show (b1 > b2)
    putStrLn $ "Est-ce que b1 == b3 ? " ++ show (b1 == b3)
```

---

### Explication détaillée du code

#### 1. La contrainte `Ord a =>`
Dans la déclaration `instance Ord a => Ord (Box a)`, le fragment `Ord a` est crucial. Il signifie : "Nous pouvons comparer deux `Box` uniquement si le contenu à l'intérieur de la boîte (le type `a`) est lui-même comparable." 
* Si vous avez une `Box Int`, cela fonctionne car les entiers sont ordonnables.
* Si vous aviez une `Box (Int -> Int)` (une fonction), cela échouerait car on ne peut pas comparer deux fonctions.

#### 2. La fonction `compare`
La méthode `compare` est le cœur de la classe `Ord`. Elle ne renvoie pas un booléen, mais un type de donnée spécial appelé **`Ordering`** qui possède trois valeurs possibles :
* **`LT`** (Less Than) : Le premier élément est plus petit.
* **`EQ`** (Equal) : Les deux éléments sont égaux.
* **`GT`** (Greater Than) : Le premier élément est plus grand.

Dans notre implémentation, `compare (Box x) (Box y) = compare x y`, nous déléguons simplement la responsabilité de la comparaison au contenu de la boîte.

#### 3. Les opérateurs dérivés
L'avantage de définir `compare` est que Haskell vous donne gratuitement tous les opérateurs relationnels : `<`, `>`, `<=`, et `>=`. Ils sont tous implémentés en interne en utilisant le résultat de votre fonction `compare`.



#### 4. Instance `Show` personnalisée
Au lieu d'utiliser `deriving (Show)`, j'ai écrit une instance manuelle pour rendre la sortie console plus lisible, affichant `Box(10)` au lieu de simplement `Box 10`.
