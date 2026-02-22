HC6T10 : Récupérer les chiffres d’un nombre (récursif)
---
### Code Source Complet

Voici l'implémentation en Haskell. Elle traite les cas particuliers comme le zéro et les nombres négatifs.

```haskell
-- Signature : prend un entier et retourne une liste d'entiers
digits :: Int -> [Int]

-- Cas particulier pour 0
digits 0 = [0]

-- On utilise une fonction auxiliaire pour gérer la récursion proprement
-- On utilise abs pour supporter les nombres négatifs
digits n = reverse (helper (abs n))
  where
    helper 0 = []
    helper x = (x `mod` 10) : helper (x `div` 10)

main :: IO ()
main = do
    let nombre = 12345
    putStr "Les chiffres de "
    putStr (show nombre)
    putStr " sont : "
    print (digits nombre)

```

---

### Explication Technique

Le calcul repose sur deux opérateurs mathématiques :

1. **`mod 10`** : Récupère le reste de la division par 10 (le chiffre des unités). Par exemple, `123 `mod` 10` donne `3`.
2. **`div 10`** : Effectue la division entière par 10 (enlève le dernier chiffre). Par exemple, `123 `div` 10` donne `12`.

#### Pourquoi utiliser une fonction `helper` et `reverse` ?

Si nous faisons la récursion directement, nous récupérons les chiffres dans le mauvais sens (le chiffre des unités en premier).

* `helper 123` produit d'abord `3`, puis `2`, puis `1`, soit `[3, 2, 1]`.
* Nous appliquons `reverse` à la fin pour obtenir `[1, 2, 3]`.

#### Le processus pas à pas pour `123` :

* `helper 123` : `123 mod 10 = 3`. Reste `123 div 10 = 12`.
* `helper 12` : `12 mod 10 = 2`. Reste `12 div 10 = 1`.
* `helper 1` : `1 mod 10 = 1`. Reste `1 div 10 = 0`.
* `helper 0` : `[]` (Cas de base).
* **Résultat de helper** : `3 : 2 : 1 : []` = `[3, 2, 1]`.
* **Après reverse** : `[1, 2, 3]`.

---

### Alternative sans récursion explicite

En Haskell, on peut aussi convertir le nombre en chaîne de caractères, puis chaque caractère en chiffre. C'est plus court, mais moins "mathématique" :

```haskell
digitsEasy :: Int -> [Int]
digitsEasy n = map (\c -> read [c]) (show (abs n))

```
