HC6T1 : Factorielle (récursif)
---
### Code Source Complet

```haskell
-- Signature : prend un Integer et renvoie un Integer
-- On utilise Integer pour gérer de très grands nombres sans erreur de dépassement
factorial :: Integer -> Integer

-- Cas de base : la factorielle de 0 est 1
factorial 0 = 1

-- Cas récursif : n! = n * (n - 1)!
factorial n = n * factorial (n - 1)

main :: IO ()
main = do
    putStr "La factorielle de 5 est : "
    print (factorial 5)
    
    putStr "La factorielle de 20 est : "
    print (factorial 20)

```

---

### Explication du fonctionnement

La récursion fonctionne comme une pile d'assiettes que l'on empile jusqu'à atteindre le fond, puis que l'on dépile pour obtenir le résultat final.

1. **Le Cas de Base (`factorial 0 = 1`)** : C'est la condition d'arrêt. Sans elle, la fonction s'appellerait indéfiniment (provoquant une erreur de type *stack overflow*).
2. **Le Cas Récursif (`n * factorial (n - 1)`)** : La fonction s'appelle elle-même avec un argument plus petit.

#### Déroulement pour `factorial 3` :

* `factorial 3` appelle `3 * factorial 2`
* `factorial 2` appelle `2 * factorial 1`
* `factorial 1` appelle `1 * factorial 0`
* `factorial 0` renvoie `1` (Cas de base atteint)

---

