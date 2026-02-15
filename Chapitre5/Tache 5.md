HC5T5 : Application partielle
---
### Code source (Haskell)

```haskell
-- 1. Signature de type
-- Prend un entier et renvoie un entier
multiplyByFive :: Int -> Int

-- 2. Définition par application partielle
-- On ne précise pas l'argument 'x', on "prépare" juste la fonction (*) avec 5
multiplyByFive = (*) 5

-- 3. Fonction principale pour le test
main :: IO ()
main = do
    let nombre = 10
    
    -- Appel de la fonction
    let resultat = multiplyByFive nombre
    
    putStrLn ("5 multiplié par " ++ show nombre ++ " donne : " ++ show resultat)
    
    -- On peut aussi l'utiliser avec map sur une liste
    let nombres = [1, 2, 3, 4, 5]
    print (map multiplyByFive nombres)

```

---

### Explication détaillée

#### 1. Qu'est-ce que l'application partielle ?

En Haskell, une fonction comme la multiplication `(*)` attend normalement deux nombres. Si vous ne lui en donnez qu'un seul (ici le `5`), elle ne renvoie pas d'erreur. À la place, elle renvoie une **nouvelle fonction** qui attend "le reste" (le deuxième nombre).

C'est exactement ce que nous faisons avec `multiplyByFive = (*) 5`.

#### 2. Pourquoi écrire `(*) 5` ?

* Normalement, on écrit `5 * x`. L'étoile est un opérateur "infixe" (au milieu).
* En mettant l'opérateur entre parenthèses `(*)`, on le transforme en fonction "préfixe" (qu'on met au début).
* `(*) 5` signifie donc : "Prends la fonction multiplication et fixe le premier paramètre à 5".

#### 3. La Signature `Int -> Int`

Même si `multiplyByFive` est créée à partir d'une multiplication, son type final est simple : elle prend un `Int` (celui qui manque) et renvoie un `Int` (le résultat final).

#### 4. Comparaison des syntaxes

Toutes ces écritures sont équivalentes, mais la première est la plus "Haskellienne" :

* **Partielle :** `multiplyByFive = (*) 5`
* **Section :** `multiplyByFive = (5 *)`
* **Lambda :** `multiplyByFive = \x -> 5 * x`
* **Classique :** `multiplyByFive x = 5 * x`

