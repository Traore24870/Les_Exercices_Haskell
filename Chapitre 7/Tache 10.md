HC7T10 : Fonction avec plusieurs contraintes de classes de types
---

### Le Code Source (Haskell)

```haskell
-- 1. On récupère nos bases : Shape et la classe Describable
data Shape = Circle Double | Rectangle Double Double
    deriving (Eq, Ord, Show) -- Ord est nécessaire pour comparer !

class Describable a where
    describe :: a -> String

instance Describable Shape where
    describe (Circle r)      = "Un cercle de rayon " ++ show r
    describe (Rectangle l h) = "Un rectangle de " ++ show l ++ "x" ++ show h

-- 2. La fonction avec contraintes multiples
-- Elle nécessite que 'a' soit à la fois Describable et Ord
describeAndCompare :: (Describable a, Ord a) => a -> a -> String
describeAndCompare x y = 
    if x >= y 
    then "Le plus grand est : " ++ describe x
    else "Le plus grand est : " ++ describe y

-- 3. Test dans le main
main :: IO ()
main = do
    let s1 = Circle 5.0      -- Petit cercle
    let s2 = Circle 10.0     -- Grand cercle
    
    putStrLn "--- Test de describeAndCompare ---"
    putStrLn $ describeAndCompare s1 s2
    
    -- Test avec des entiers (si on ajoute l'instance)
    -- (Voir l'explication ci-dessous)

```

---

### Explication Détaillée

#### 1. La signature `(Describable a, Ord a) =>`

C'est le cœur de l'exercice. Nous définissons une fonction qui ne peut travailler qu'avec des types possédant **deux caractéristiques** :

* **`Ord a`** : Indispensable pour pouvoir utiliser l'opérateur `>=`. Sans cela, la fonction ne saurait pas laquelle des deux valeurs est la "plus grande".
* **`Describable a`** : Indispensable pour pouvoir appeler la méthode `describe` sur le résultat.

#### 2. Le fonctionnement interne

La fonction compare d'abord les deux arguments `x` et `y`. Une fois le "vainqueur" déterminé par la logique de `Ord`, elle passe cet objet à la fonction `describe`. C'est un bel exemple de **polymorphisme contraint** : la fonction est générique, mais elle impose un "contrat" strict sur ce qu'elle reçoit.

#### 3. L'importance de `deriving (Ord)`

Pour que `Shape` fonctionne avec cette fonction, il **doit** avoir une instance `Ord`. Dans mon exemple, j'ai utilisé `deriving Ord`.

> **Note technique :** Par défaut, `deriving Ord` pour un type `data` compare les constructeurs dans l'ordre de leur déclaration. Ici, `Rectangle` serait considéré comme "plus grand" que `Circle`. Si vous voulez comparer par surface, il faudrait écrire l'instance `Ord` manuellement comme nous l'avons fait dans l'exercice HC7T2.

---

### Résumé de la hiérarchie

| Élément | Rôle |
| --- | --- |
| **`x >= y`** | Utilise la contrainte **`Ord`**. |
| **`describe x`** | Utilise la contrainte **`Describable`**. |
| **`a -> a -> String`** | Prend deux objets identiques et rend du texte. |

