HC6T9 : Implémentation de map
---
### Code Source Complet

Voici l'implémentation de notre propre fonction `myMap`, avec sa signature de type générique et un exemple concret dans le `main`.

```haskell
-- Signature : prend une fonction (a -> b) et une liste [a]
-- Retourne une nouvelle liste [b]
myMap :: (a -> b) -> [a] -> [b]

-- Cas de base : appliquer une fonction à une liste vide donne une liste vide
myMap _ [] = []

-- Cas récursif : on applique 'f' à la tête (x) 
-- et on l'attache (:) au résultat de l'application de 'f' sur le reste (xs)
myMap f (x:xs) = f x : myMap f xs

main :: IO ()
main = do
    let nombres = [1, 2, 3, 4, 5]
    
    putStr "Liste originale : "
    print nombres
    
    putStr "Chaque élément au carré : "
    -- On passe la fonction (^2) à notre myMap
    print (myMap (^2) nombres)
    
    putStr "Chaque élément converti en texte : "
    -- On transforme la liste d'entiers en liste de chaînes
    print (myMap show nombres)

```

---

### Explication Technique

#### 1. La Signature générique `(a -> b) -> [a] -> [b]`

C'est la partie la plus importante :

* **(a -> b)** : Le premier argument est une fonction qui transforme un type `a` en type `b`.
* **[a]** : Le deuxième argument est une liste contenant des éléments de type `a`.
* **[b]** : Le résultat est une liste contenant des éléments de type `b`.
* *Note :* `a` et `b` peuvent être du même type (ex: `Int -> Int`) ou de types différents (ex: `Int -> String`).

#### 2. Le mécanisme de transformation

La fonction travaille de manière "paresseuse" et récursive :

1. Elle sépare la tête `x` du reste `xs`.
2. Elle calcule `f x`.
3. Elle utilise l'opérateur de construction `:` (cons) pour attacher ce nouveau résultat devant l'appel récursif `myMap f xs`.

#### 3. Trace de l'exécution pour `myMap (*2) [1, 2]`

* `myMap (*2) (1:2:[])`
*  `(*2) 1 : myMap (*2) (2:[])`
*  `2 : ((*2) 2 : myMap (*2) [])`
*  `2 : (4 : [])`
* **Résultat :** `[2, 4]`

---
