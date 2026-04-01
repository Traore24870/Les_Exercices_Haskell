HC10T4 : Instance Eq pour Box
---
---

## Code Source (Haskell)

```haskell
-- 1. Définition du type paramétrique Box
-- Le 'a' signifie que la boîte peut contenir n'importe quel type.
data Box a = Box a

-- 2. Implémentation manuelle de l'instance Eq
-- Notez la contrainte (Eq a) : on ne peut comparer deux Box 
-- que si le contenu 'a' est lui-même comparable.
instance (Eq a) => Eq (Box a) where
    (Box x) == (Box y) = x == y
    (Box x) /= (Box y) = not (x == y)

-- 3. Fonction principale pour tester
main :: IO ()
main = do
    let boxInt1 = Box 10
    let boxInt2 = Box 10
    let boxInt3 = Box 5
    
    let boxStr1 = Box "Haskell"
    let boxStr2 = Box "Java"

    putStrLn "--- Test de l'instance Eq pour Box ---"
    putStr "Box 10 == Box 10 ? "
    print (boxInt1 == boxInt2)
    
    putStr "Box 10 == Box 5  ? "
    print (boxInt1 == boxInt3)
    
    putStr "Box 'Haskell' == Box 'Java' ? "
    print (boxStr1 == boxStr2)
```

---

## Explication Détaillée

### 1. Le Type Paramétrique (`Box a`)
Le type `Box a` est un conteneur simple. Le **`a`** est une variable de type. Cela signifie que vous pouvez avoir une `Box Int`, une `Box String`, ou même une `Box (Box Int)`. C'est le principe fondamental de la réutilisabilité en Haskell.

### 2. La Contrainte de Type (`Eq a =>`)
C'est la partie la plus importante de l'exercice. 
* Pour savoir si deux `Box` sont égales, nous devons regarder à l'intérieur et comparer leurs contenus.
* Cependant, tous les types en Haskell ne sont pas comparables (par exemple, on ne peut pas comparer deux fonctions).
* **`(Eq a) =>`** dit au compilateur : "Je peux définir l'égalité pour `Box a` **à condition que** le type `a` possède lui-même une instance de `Eq`".

### 3. L'implémentation de `==` et `/=`
* **`==`** : Nous utilisons le pattern matching pour extraire les valeurs `x` et `y` des deux boîtes. Si `x == y` (en utilisant l'égalité propre au type `a`), alors les boîtes sont égales.
* **`/=`** : En Haskell, l'inégalité est souvent définie comme la négation de l'égalité.

---

## Le saviez-vous ? (La Dérivation Automatique)
En Haskell, pour un type aussi simple que `Box`, on n'écrit généralement pas l'instance à la main. On utilise le mot-clé **`deriving`** :

```haskell
data Box a = Box a deriving (Eq)
```

Le compilateur génère alors automatiquement exactement le même code que celui que nous avons écrit manuellement, ce qui évite les erreurs répétitives et rend le code plus propre.
