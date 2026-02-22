HC6T6 : Existence d’un élément dans une liste
---
### Code Source Complet

Voici l'implémentation utilisant le **pattern matching** et les **gardes**, ce qui est la méthode la plus pédagogique pour comprendre le parcours d'une liste.

```haskell
-- Signature : 'a' doit être un type comparable (Eq)
-- La fonction prend un élément, une liste et renvoie un Booléen
exists :: Eq a => a -> [a] -> Bool

-- Cas de base 1 : Si la liste est vide, l'élément n'existe pas
exists _ [] = False

-- Cas récursif avec gardes :
exists target (x:xs)
    | target == x = True            -- Si on trouve l'élément, c'est gagné
    | otherwise   = exists target xs -- Sinon, on cherche dans le reste (la queue)

main :: IO ()
main = do
    let maListe = [10, 20, 30, 40, 50]
    putStrLn $ "Est-ce que 30 est dans la liste ? " ++ show (exists 30 maListe)
    putStrLn $ "Est-ce que 100 est dans la liste ? " ++ show (exists 100 maListe)

```

---

### Explication Technique

1. **La contrainte `Eq a**` : C'est une "classe de type". Elle indique à Haskell que cette fonction ne peut fonctionner que sur des types que l'on peut comparer avec l'opérateur `==` (comme les entiers, les caractères ou les chaînes).
2. **Le symbole `_` (Wildcard)** : Dans `exists _ []`, le tiret bas signifie que peu importe ce que nous cherchons, si la liste est vide, le résultat est forcément `False`.
3. **Le mécanisme de recherche** : La fonction regarde la "tête" de la liste (`x`). Si elle correspond à notre cible, elle s'arrête immédiatement et renvoie `True` (grâce à l'évaluation paresseuse). Sinon, elle "découpe" la liste et recommence avec la suite (`xs`).

---

