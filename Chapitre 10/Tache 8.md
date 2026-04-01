HC10T8 : Sous-classe AdvancedEq de Eq
---
---

## Code Source (Haskell)

```haskell
-- 1. Définition du type de données (exemple : Point)
data Point = Point Int Int deriving (Show)

-- 2. On doit d'abord implémenter Eq pour notre type
-- (Ou utiliser 'deriving Eq', mais faisons-le manuellement pour la clarté)
instance Eq Point where
    (Point x1 y1) == (Point x2 y2) = x1 == x2 && y1 == y2

-- 3. Définition de la sous-classe AdvancedEq
-- La syntaxe (Eq a) => signifie : "Pour être AdvancedEq, 'a' doit d'abord être Eq"
class (Eq a) => AdvancedEq a where
    compareEquality :: a -> a -> Bool
    -- On peut fournir une implémentation par défaut
    compareEquality x y = x == y

-- 4. Implémentation de l'instance AdvancedEq pour Point
instance AdvancedEq Point where
    -- On pourrait redéfinir une logique spécifique ici si besoin
    compareEquality p1 p2 = p1 == p2

-- 5. Fonction principale de test
main :: IO ()
main = do
    let p1 = Point 5 10
    let p2 = Point 5 10
    let p3 = Point 0 0
    
    putStrLn "--- Test de la sous-classe AdvancedEq ---"
    putStr "p1 == p2 (via compareEquality) : "
    print (compareEquality p1 p2)
    
    putStr "p1 == p3 (via compareEquality) : "
    print (compareEquality p1 p3)
```

---

## Explication Détaillée

### 1. La Hiérarchie des Classes (`(Eq a) =>`)
C'est le point central de l'exercice. La flèche `=>` dans la définition de la classe crée une **contrainte de super-classe**. 
* Cela signifie que `Eq` est une condition préalable pour `AdvancedEq`. 
* Si vous essayez de déclarer `instance AdvancedEq MonType` sans avoir déclaré `instance Eq MonType`, le compilateur générera une erreur.



### 2. La Méthode `compareEquality`
Dans cet exemple, `compareEquality` agit comme un alias ou une extension de l'égalité standard. L'avantage d'une sous-classe est que vous avez accès à toutes les méthodes de la classe mère (comme `==` et `/=`) à l'intérieur des fonctions de la sous-classe.

### 3. Pourquoi utiliser des sous-classes ?
Le sous-classement est utilisé en Haskell pour construire des structures de plus en plus riches. Par exemple, dans la bibliothèque standard :
* **`Ord`** est une sous-classe de **`Eq`** (on ne peut pas trier des éléments si on ne sait pas s'ils sont égaux).
* **`Num`** (les nombres) est souvent une sous-classe de **`Show`** et **`Eq`**.

### 4. Application Pratique
Dans notre code, le type `Point` implémente `Eq` pour comparer les coordonnées `x` et `y`. Ensuite, `AdvancedEq` hérite de cette capacité. Cela garantit une cohérence : si deux points sont considérés comme "avancés-égaux", ils sont forcément "égaux" au sens de base.

---
