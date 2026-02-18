HC6T3 : Somme des éléments avec foldr
---
### Code Source Complet

Voici le code incluant la signature de type, l'implémentation avec `foldr` et une fonction `main` pour le test.

```haskell
-- Signature : prend une liste de nombres et retourne leur somme
-- On utilise la classe de type Num pour que cela fonctionne avec Int, Float, etc.
sumWithFoldr :: Num a => [a] -> a
sumWithFoldr xs = foldr (+) 0 xs

main :: IO ()
main = do
    let nombres = [1, 2, 3, 4, 5, 10]
    putStr "La somme de la liste [1, 2, 3, 4, 5, 10] est : "
    print (sumWithFoldr nombres)

```

---

### Explication Technique

La fonction `foldr` prend trois arguments :

1. **Une fonction binaire** : ici `(+)`, qui définit comment combiner les éléments.
2. **Une valeur initiale** : ici `0`, qui est l'élément neutre de l'addition (le point de départ).
3. **La liste à traiter** : ici `xs`.

#### Comment `foldr` transforme la liste :

`foldr` remplace récursivement le constructeur de liste `:` par l'opérateur fourni et la liste vide `[]` par la valeur initiale.

Pour une liste `[1, 2, 3]`, qui s'écrit en réalité `1 : (2 : (3 : []))` en Haskell, `foldr (+) 0` effectue la transformation suivante :
`1 + (2 + (3 + 0))`

**Le processus visuel :**

* On part de la droite (le `0`).
* On ajoute `3` → `3`.
* On ajoute `2` → `5`.
* On ajoute `1` → `6`.

---
