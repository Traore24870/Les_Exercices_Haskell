HC6T2 : Suite de Fibonacci (récursif)
---
### Code Source Complet

Voici l'implémentation utilisant le **pattern matching** pour définir les cas de base et le cas récursif.

```haskell
-- Signature : prend l'indice n et retourne le n-ième nombre de Fibonacci
fibonacci :: Int -> Integer
-- Cas de base 1 : Fibonacci de 0 est 0
fibonacci 0 = 0
-- Cas de base 2 : Fibonacci de 1 est 1
fibonacci 1 = 1
-- Cas récursif : Somme des deux précédents
fibonacci n = fibonacci (n - 1) + fibonacci (n - 2)

main :: IO ()
main = do
    putStrLn "Calcul des premiers nombres de Fibonacci :"
    -- Affiche les 10 premiers termes
    print [fibonacci n | n <- [0..10]]

```

---

### Explication Technique

#### 1. Les Cas de Base

Une fonction récursive a besoin de points d'arrêt. Ici, nous en avons deux : `0` et `1`. Sans eux, la fonction essaierait de calculer `fibonacci (-1)`, ce qui mènerait à une récursion infinie.

#### 2. L'Arbre de Récursion

Cette méthode est dite "récursion double". Pour calculer `fibonacci 4`, le programme doit calculer :

* `fibonacci 3` et `fibonacci 2`
* Mais pour `fibonacci 3`, il doit aussi recalculer `fibonacci 2` et `fibonacci 1`

#### 3. Limite de cette approche

Bien que très élégante et fidèle à la définition mathématique, cette implémentation est **inefficace** pour de grands nombres (comme `fibonacci 50`). Pourquoi ? Parce qu'elle recalcule inutilement les mêmes valeurs des milliers de fois. Sa complexité est exponentielle ().

---

### Une version optimisée (Linéaire)

Pour éviter de recalculer les mêmes valeurs, on peut utiliser une fonction auxiliaire qui "transporte" les résultats précédents (une approche de programmation dynamique ou récursion terminale) :

```haskell
fibFast :: Int -> Integer
fibFast n = helper 0 1 n
  where
    helper a b 0 = a
    helper a b n = helper b (a + b) (n - 1)

```
