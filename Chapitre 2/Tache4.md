HC2T4 - Tâche 4 : Notation préfixe et infixe
---

##1. Notation Préfixe (Fonction normale)La notation préfixe place le nom de la fonction (ou l'opérateur) **avant** ses arguments. C'est la façon standard d'appeler des fonctions en Haskell.

| Expression en Infixe | Expression en Préfixe | Explication |
| --- | --- | --- |
| `5 + 3` | **`(+) 5 3`** | L'opérateur `+` est utilisé comme une fonction en l'entourant de parenthèses. |
| `10 * 4` | **`(*) 10 4`** | L'opérateur `*` est utilisé comme une fonction. |
| `True && False` | **`(&&) True False`** | L'opérateur `&&` est utilisé comme une fonction. |

---

##2. Notation Infixe (Opérateur)La notation infixe place l'opérateur **entre** ses deux arguments. En Haskell, pour transformer n'importe quelle fonction binaire (prenant deux arguments) en opérateur infixe, on l'encadre avec des **accents graves** (backticks :).

| Expression en Préfixe | Expression en Infixe | Explication |
| --- | --- | --- |
| `(+) 7 2` | **`7 + 2`** | `(+)` est la version fonctionnelle de l'opérateur infixe `+`. |
| `(*) 6 5` | **`6 * 5`** | `(*)` est la version fonctionnelle de l'opérateur infixe `*`. |
| `(&&) True False` | **`True && False`** | `(&&)` est la version fonctionnelle de l'opérateur infixe `&&`. |

###💡 Le Rôle des Accents Graves (Backticks)Si vous aviez défini une fonction binaire nommée, par exemple, `addNumbers`, vous pourriez l'utiliser en infixe grâce aux accents graves :

```haskell
addNumbers x y = x + y

-- Utilisation en préfixe (standard)
result1 = addNumbers 10 5  -- 15

-- Utilisation en infixe (avec accents graves)
result2 = 10 `addNumbers` 5 -- 15

```
