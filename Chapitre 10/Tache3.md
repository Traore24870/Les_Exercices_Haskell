HC10T3 : Classe de type Comparable
---
---

## Code Source (Haskell)

```haskell
-- 1. Définition du type de données Blockchain
-- Une Blockchain est ici représentée par une liste de blocs (chaînes de caractères)
data Blockchain = Chain [String]

-- 2. Définition de la classe de type Comparable
-- Elle exige la fonction compareWith qui renvoie un type Ordering (LT, EQ, ou GT)
class Comparable a where
    compareWith :: a -> a -> Ordering

-- 3. Implémentation de l'instance pour Blockchain
instance Comparable Blockchain where
    compareWith (Chain b1) (Chain b2)
        | length b1 < length b2 = LT
        | length b1 > length b2 = GT
        | otherwise             = EQ

-- 4. Fonction principale (main) pour le test
main :: IO ()
main = do
    let bc1 = Chain ["Genesis", "Block 1"]           -- Longueur 2
    let bc2 = Chain ["Genesis", "Block 1", "Block 2"] -- Longueur 3
    
    putStrLn "--- Comparaison de Blockchains ---"
    let resultat = compareWith bc1 bc2
    
    case resultat of
        LT -> putStrLn "La première chaîne est plus courte."
        GT -> putStrLn "La première chaîne est plus longue."
        EQ -> putStrLn "Les deux chaînes ont la même longueur."
```

---

## Explication Détaillée

### 1. Le Type `Blockchain`
Nous avons défini un type `Blockchain` qui utilise un constructeur de données `Chain`. Il encapsule une liste de `String`. Dans un système réel, ce serait une liste d'objets `Block` complexes, mais le principe de comparaison resterait le même.

### 2. La Classe `Comparable`
Cette classe introduit une variable de type **`a`**.
* **`compareWith :: a -> a -> Ordering`** : Cette signature indique que la fonction prend deux arguments du même type et doit retourner une valeur de type `Ordering`.
* **`Ordering`** est un type standard en Haskell qui possède trois valeurs possibles :
    * **`LT`** (Less Than) : Plus petit.
    * **`GT`** (Greater Than) : Plus grand.
    * **`EQ`** (Equal) : Égal.

### 3. L'Instance pour `Blockchain`
C'est ici que nous définissons la **logique métier**. Pour comparer deux blockchains, nous utilisons des **gardes** (`|`) :
* Nous comparons la `length` (longueur) de la liste des blocs.
* Si la première est plus courte que la seconde, nous renvoyons `LT`.
* Si elle est plus longue, `GT`.
* Sinon, `EQ`.

### 4. Le programme `main`
Dans le `main`, nous illustrons comment consommer ce résultat. L'utilisation d'un bloc `case...of` est la manière la plus élégante en Haskell de réagir aux différentes valeurs d'un type énuméré comme `Ordering`.

---
