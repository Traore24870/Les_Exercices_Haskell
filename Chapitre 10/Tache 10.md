HC10T10 : Classe Concatenatable
---
---

## Code Source (Haskell)

```haskell
-- 1. Définition de la classe de type Concatenatable
-- La fonction concatWith prend deux arguments de type 'a' 
-- et retourne un résultat de type 'a'.
class Concatenatable a where
    concatWith :: a -> a -> a

-- 2. Implémentation de l'instance pour le type [Char] (String)
-- En Haskell, String est un synonyme de [Char].
instance Concatenatable [Char] where
    concatWith s1 s2 = s1 ++ s2

-- 3. Fonction principale pour tester l'implémentation
main :: IO ()
main = do
    let mot1 = "Hello "
    let mot2 = "World!"
    
    let resultat = concatWith mot1 mot2
    
    putStrLn "--- Test de la classe Concatenatable ---"
    putStrLn ("Mot 1      : " ++ mot1)
    putStrLn ("Mot 2      : " ++ mot2)
    putStrLn ("Résultat   : " ++ resultat)
```

---

## Explication Détaillée

### 1. La Signature `a -> a -> a`
Cette signature est particulière. Contrairement à `convert :: a -> b`, ici le type de sortie est identique au type d'entrée. 
* Cela permet de **chaîner** les opérations. 
* Si `concatWith` fonctionne pour deux chaînes, vous pouvez utiliser le résultat pour concaténer une troisième chaîne : `concatWith (concatWith s1 s2) s3`.



### 2. L'Instance pour `[Char]` (String)
En Haskell, le type `String` n'est pas un type primitif atomique, c'est une liste de caractères (`[Char]`). 
* L'opérateur standard pour joindre deux listes est `++`.
* Notre implémentation de `concatWith` se contente donc d'appeler l'opérateur de concaténation natif des listes.

### 3. Lien avec les Semigroupes
Si vous explorez la bibliothèque standard de Haskell (`base`), vous trouverez la classe **`Semigroup`** qui possède la méthode `<>`. 
Le travail que nous venons de faire avec `Concatenatable` et `concatWith` est exactement ce que fait `Semigroup` avec `<>`. 

### 4. Pourquoi est-ce utile ?
Créer une classe comme `Concatenatable` permet d'écrire du code générique qui "assemble" des choses sans savoir ce qu'elles sont. Par exemple, on pourrait aussi l'implémenter pour :
* **Les Listes d'entiers** : `concatWith [1,2] [3,4]` donnerait `[1,2,3,4]`.
* **Les vecteurs ou matrices** : pour les additionner ou les fusionner.
* **Les documents PDF** : pour les mettre bout à bout.

---

