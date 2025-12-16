HC2T1 - Tâche 1 : Vérification des types dans GHCi
---
Voici le tableau récapitulatif des expressions, leurs types attendus, et ce que GHCi nous confirme.

---

##🎯 Analyse des Types en HaskellCet exercice montre la distinction entre les types de base (`Char`, `Bool`) et les types numériques **polymorphes** (`Num t`, `Fractional t`).

| Expression | Type attendu | Résultat GHCi (`:t expression`) | Explication Détaillée |
| --- | --- | --- | --- |
| **`42`** | `Integer` (ou tout type `Num`) | **`(Num t) => t`** | **Entier Littéral.** Ce type signifie que `42` peut être n'importe quel type `t` qui appartient à la classe de types **`Num`** (exemples : `Int`, `Integer`, `Float`, `Double`). |
| **`3.14`** | `Double` (ou tout type `Fractional`) | **`(Fractional t) => t`** | **Décimal/Flottant.** Ce type signifie que `3.14` peut être n'importe quel type `t` qui appartient à la classe de types **`Fractional`** (exemples : `Float`, `Double`). |
| **`"Haskell"`** | `String` | **`[Char]`** | **Chaîne de Caractères.** En Haskell, une chaîne est une **liste** de caractères. `String` est un alias pour `[Char]`. |
| **`'Z'`** | `Char` | **`Char`** | **Caractère Unique.** Il est toujours de type `Char`, délimité par des guillemets simples. |
| **`True && False`** | `Bool` | **`Bool`** | **Opération Booléenne.** Le résultat d'une expression utilisant l'opérateur logique `&&` (ET) est toujours un **Booléen** (`True` ou `False`). |

---

 Utilisation de la commande `:t` (pour **type**) pour confirmer :
```haskell
Prelude> :t 42
42 :: (Num t) => t

Prelude> :t "Haskell"
"Haskell" :: [Char]

Prelude> :t True && False
True && False :: Bool

