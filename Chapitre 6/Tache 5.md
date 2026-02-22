HC6T5 : Inverser une liste (récursif)
---
### Code Source Complet

Voici l'implémentation classique utilisant le **pattern matching** et l'opérateur de concaténation `++`.

```haskell
-- Signature : prend une liste de n'importe quel type 'a' et renvoie une liste du même type
reverseList :: [a] -> [a]

-- Cas de base : l'inverse d'une liste vide est une liste vide
reverseList [] = []

-- Cas récursif : on prend le premier élément (x), 
-- on inverse le reste (xs), puis on place x à la toute fin.
reverseList (x:xs) = reverseList xs ++ [x]

main :: IO ()
main = do
    let maListe = [1, 2, 3, 4, 5]
    putStr "Liste originale : "
    print maListe
    putStr "Liste inversée  : "
    print (reverseList maListe)

```

---

### Explication Technique

Le fonctionnement repose sur le principe de "diviser pour régner" :

1. **Décomposition** : Pour inverser `[1, 2, 3]`, on sépare le `1` du reste `[2, 3]`.
2. **Appel récursif** : On demande à la fonction d'inverser `[2, 3]`.
3. **Combinaison** : Une fois que `[2, 3]` est devenu `[3, 2]`, on ajoute `[1]` à la fin du résultat avec l'opérateur `++`.

#### Trace de l'exécution pour `reverseList [1, 2, 3]` :

* `reverseList [1,2,3]`  `reverseList [2,3] ++ [1]`
* `reverseList [2,3]`    `reverseList [3] ++ [2]`
* `reverseList [3]`      `reverseList [] ++ [3]`
* `reverseList []`       `[]` (Cas de base)

En remontant la pile : `[] ++ [3] ++ [2] ++ [1]` donne `[3, 2, 1]`.

---

### Optimisation : L'accumulateur (Plus efficace)

L'implémentation ci-dessus est simple mais peu performante sur de très grandes listes car l'opérateur `++` doit parcourir toute la liste à chaque étape (complexité ).

Voici la version "professionnelle" utilisant un **accumulateur**, qui est beaucoup plus rapide (complexité ) :

```haskell
reverseFast :: [a] -> [a]
reverseFast list = helper list []
  where
    helper [] acc = acc
    helper (x:xs) acc = helper xs (x:acc)

```
