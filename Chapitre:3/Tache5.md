HC3T5 - Tâche 5 : Déterminer le type d'un triangle avec des gardes
---
Pour cette dernière tâche, nous utilisons à nouveau les **gardes** (`|`). La logique repose sur la comparaison des longueurs des côtés. En Haskell, l'ordre des tests est primordial : on vérifie d'abord la condition la plus restrictive (3 côtés égaux) avant de passer aux autres.

---

## Code Source (Main.hs)

```haskell
import System.IO (hSetEncoding, stdout, utf8)

-- Tâche 5 : Classification des triangles
triangleType :: Float -> Float -> Float -> String
triangleType a b c
    | a == b && b == c = "Équilatéral"
    | a == b || b == c || a == c = "Isocèle"
    | otherwise = "Scalène"

main :: IO ()
main = do
    hSetEncoding stdout utf8
    putStrLn $ "Triangle 3 3 3 : " ++ triangleType 3 3 3
    putStrLn $ "Triangle 5 5 8 : " ++ triangleType 5 5 8
    putStrLn $ "Triangle 6 7 8 : " ++ triangleType 6 7 8

```

---

## Explications de la logique

### 1. Pourquoi cet ordre ?

* **Équilatéral (`a == b && b == c`)** : Si cette condition est vraie, le triangle a 3 côtés égaux. On s'arrête là.
* **Isocèle (`a == b || b == c || a == c`)** : Si la première condition était fausse mais que celle-ci est vraie, cela signifie qu'il y a exactement deux côtés égaux (ou que le test précédent a échoué). L'opérateur `||` signifie "OU".
* **Scalène (`otherwise`)** : Si aucune des égalités ci-dessus n'est vraie, le triangle est forcément scalène (tous les côtés sont différents).

### 2. Les opérateurs de comparaison

* **`==`** : Teste l'égalité entre deux valeurs.
* **`&&`** : Opérateur "ET" (toutes les conditions doivent être vraies).
* **`||`** : Opérateur "OU" (au moins une condition doit être vraie).

---

## Résultat attendu dans la console

```text
Triangle 3 3 3 : Équilatéral
Triangle 5 5 8 : Isocèle
Triangle 6 7 8 : Scalène

```
