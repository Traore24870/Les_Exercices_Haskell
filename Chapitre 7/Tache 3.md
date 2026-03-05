HC7T3 : Fonction avec contraintes multiples
---
### Le Code Source (Haskell)

```haskell

-- 1. Fonction avec contraintes multiples
-- On exige que 'a' implémente les classes Eq et Ord
compareValues :: (Eq a, Ord a) => a -> a -> a
compareValues x y = if x >= y then x else y

-- 3. Point d'entrée pour les tests
main :: IO ()
main = do
    putStrLn "--- Test avec des Entiers ---"
    let maxInt = compareValues 10 25
    putStr "Le plus grand entre 10 et 25 est : "
    print maxInt
```

---

### Explication Détaillée

#### 1. La Signature et les Contraintes `(Eq a, Ord a) =>`

C'est la partie la plus importante de l'exercice.

* **`a`** : C'est une variable de type. Elle signifie que la fonction peut accepter n'importe quel type (Int, Float, Color, etc.).
* **`=>`** : Ce symbole sépare les **contraintes** du reste de la signature.
* **`(Eq a, Ord a)`** : Nous disons au compilateur : "Tu peux utiliser n'importe quel type `a`, **à condition** que ce type possède une instance `Eq` (pour l'égalité) et une instance `Ord` (pour la comparaison)".

> **Note :** En réalité, comme `Ord` hérite déjà de `Eq` en Haskell, la contrainte `Ord a` suffirait techniquement, mais l'écrire explicitement comme demandé montre que vous maîtrisez la syntaxe des contraintes multiples.

#### 2. Le corps de la fonction

La logique `if x >= y then x else y` utilise l'opérateur `>=`. Cet opérateur n'est disponible que parce que nous avons précisé la contrainte `Ord a`. Si nous l'avions oubliée, Haskell générerait une erreur car il ne saurait pas si le type `a` supporte la comparaison.

---

