HC6T7 : Taille d’une liste
---
### Code Source Complet

Voici l'implémentation utilisant le **pattern matching** pour décomposer la liste.

```haskell
-- Signature : prend une liste d'éléments de type 'a' et renvoie un entier
listLength :: [a] -> Int

-- Cas de base : la longueur d'une liste vide est 0
listLength [] = 0

-- Cas récursif : on ignore l'élément actuel (_) et on ajoute 1
-- au calcul de la longueur du reste de la liste (xs)
listLength (_:xs) = 1 + listLength xs

main :: IO ()
main = do
    let maListe = [10, 20, 30, 40, 50]
    putStr "La taille de la liste est : "
    print (listLength maListe)

```

---

### Explication Technique

#### 1. Le Pattern Matching (Filtrage par motif)

La fonction utilise deux définitions :

* `listLength []` : C'est la condition d'arrêt. Si la liste est vide, on renvoie `0`.
* `listLength (_:xs)` : Ici, on sépare la tête de la liste du reste. Le symbole `_` (wildcard) est utilisé car la **valeur** de l'élément ne nous intéresse pas pour compter, seule son **existence** compte. `xs` représente le reste de la liste.

#### 2. Le mécanisme de récursion

Haskell va "déplier" la fonction jusqu'à atteindre la liste vide.
Pour `listLength [1, 2, 3]` :

1. `1 + (listLength [2, 3])`
2. `1 + (1 + (listLength [3]))`
3. `1 + (1 + (1 + (listLength [])))`
4. `1 + 1 + 1 + 0 = 3`

