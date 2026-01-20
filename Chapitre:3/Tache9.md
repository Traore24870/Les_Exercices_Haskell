HC3T9 - Tâche avancée 9 : Trouver le maximum de trois nombres avec let
---
### Code complet (Haskell)
```haskell
-- Définition de la fonction utilisant le bloc 'let'
maxOfThree :: Int -> Int -> Int -> Int
maxOfThree a b c =
    let maxAB = if a > b then a else b
        resultat = if maxAB > c then maxAB else c
    in resultat

-- Fonction principale pour tester les cas demandés
main :: IO ()
main = do
    putStrLn ("Le maximum de (10, 20, 15) est : " ++ show (maxOfThree 10 20 15))
    putStrLn ("Le maximum de (5, 25, 10) est : " ++ show (maxOfThree 5 25 10))

```

### Explication du fonctionnement

1. **Le bloc `let...in**` :
* La partie `let` sert à déclarer des variables intermédiaires (ici `maxAB` et `resultat`).
* La partie `in` définit ce que la fonction doit finalement retourner.


2. **Logique par étapes** :
* On compare d'abord les deux premiers nombres (`a` et `b`) pour stocker le plus grand dans `maxAB`.
* On compare ensuite ce résultat (`maxAB`) avec le troisième nombre (`c`).


3. **Comparaison avec `where**` : Alors que `where` se place après le corps de la fonction, `let` se place avant. C'est très utile pour décomposer un calcul complexe en étapes logiques avant de donner la réponse finale.

### Résultats des tests

* `maxOfThree 10 20 15` : Le programme identifie que 20 est plus grand que 10, puis que 20 est plus grand que 15. Résultat : **20**.
* `maxOfThree 5 25 10` : Le programme identifie que 25 est plus grand que 5, puis que 25 est plus grand que 10. Résultat : **25**.
---
