HC5T8 : Style point-free
---
### Code Source Complet


```haskell
-- Définition en style point-free
-- On retire l'argument 'x' des deux côtés de l'équation
addFive :: Int -> Int
addFive = (+ 5)

main :: IO ()
main = do
    putStr "Le résultat de addFive 10 est : "
    print (addFive 10)

```

---

### Explication 

Le style "point-free" ne signifie pas "sans points", mais "sans points de données" (les arguments). Voici comment nous passons de la forme classique à la forme point-free :

#### 1. La Section de l'Opérateur

En Haskell, les opérateurs comme `+` sont des fonctions infixées. On peut les transformer en fonctions préfixées ou utiliser des **sections**.

* `(x + 5)` est équivalent à `((+) x 5)`.
* Par la propriété de la **section d'opérateur**, `(+ 5)` est une fonction qui attend un argument pour lui ajouter 5.

#### 2. La Simplification

Dans notre cas :

* **Style classique :** `addFive x = (+ 5) x`
* **Style point-free :** `addFive = (+ 5)`

L'argument  est "implicite" ; il est passé directement à la section `(+ 5)`.

### Avantages et Limites

* **Clarté :** Le code est plus concis. On définit ce que la fonction *est* plutôt que ce qu'elle *fait* avec ses données.
* **Lisibilité :** C'est très efficace pour les petites fonctions, mais cela peut devenir illisible (le "point-fail style") si on abuse de la composition sur des fonctions complexes.
