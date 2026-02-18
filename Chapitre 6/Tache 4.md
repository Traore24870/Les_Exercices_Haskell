HC6T4 : Produit des éléments avec foldl
---
### Code Source Complet

Voici l'implémentation complète avec la signature de type et une fonction `main` pour tester le résultat.

```haskell
-- Signature : fonctionne pour n'importe quel type numérique (Int, Double, etc.)
productWithFoldl :: Num a => [a] -> a
productWithFoldl xs = foldl (*) 1 xs

main :: IO ()
main = do
    let nombres = [2, 3, 4]
    putStr "Le produit de la liste [2, 3, 4] est : "
    print (productWithFoldl nombres) -- Résultat attendu : 24

```

---

### Explication Technique

La fonction `foldl` (pour *fold left*) réduit une liste en appliquant une opération binaire de manière cumulative de la gauche vers la droite.

#### 1. Fonctionnement étape par étape

Pour une liste `[2, 3, 4]`, l'appel `foldl (*) 1 [2, 3, 4]` se décompose ainsi :

1. On commence avec la valeur initiale : **1**
2. On applique l'opération avec le premier élément à gauche (2) : `(1 * 2) = 2`
3. On utilise ce résultat avec l'élément suivant (3) : `(2 * 3) = 6`
4. On utilise ce résultat avec le dernier élément (4) : `(6 * 4) = 24`

L'expression parenthésée ressemble à ceci : `((1 * 2) * 3) * 4`.

#### 2. Différence entre `foldl` et `foldr`

Contrairement à `foldr` qui commence par la fin de la liste, `foldl` traite les éléments dès le début. Pour la multiplication (qui est commutative), le résultat est identique, mais la structure de calcul change.

---

En Haskell, pour de très grandes listes, on utilise souvent `foldl'`(avec une apostrophe, disponible dans `Data.List`).

* `foldl` est "paresseux" : il crée une énorme expression mathématique en mémoire avant de la calculer.
* `foldl'` est "strict" : il calcule le résultat intermédiaire à chaque étape, ce qui évite de saturer la mémoire (consommation de pile).
