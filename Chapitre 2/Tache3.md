HC2T3 - Tâche 3 : Variables immuables
---

Voici comment définir ces valeurs, et ce qui se passe lorsque nous essayons de les modifier :

| Nom de la liaison | Type souhaité | Définition GHCi | Type réel GHCi |
| --- | --- | --- | --- |
| **`myAge`** | `Int` | `let myAge = 30` | `Integer` (par défaut) |
| **`piValue`** | `Double` | `let piValue = 3.14159 :: Double` | `Double` |
| **`greeting`** | `String` | `let greeting = "Bonjour Haskell !"` | `[Char]` |
| **`isHaskellFun`** | `Bool` | `let isHaskellFun = True` | `Bool` |

---

###2. Tentative de Modification et Résultat Puisque les valeurs définies avec `let` en Haskell sont **immuables** (elles ne changent jamais), il est **impossible** de les modifier comme on le ferait dans des langages impératifs (utilisant un opérateur d'affectation).

####Ce qui se passe en GHCi : Le Masquage (Shadowing)Si vous essayez de "modifier" `myAge` dans GHCi en utilisant `let` à nouveau :

1. **Liaison initiale :**
```haskell
Prelude> let myAge = 30

```


2. **Tentative de "modification" (création d'une nouvelle liaison) :**
```haskell
Prelude> let myAge = 31

```



**Résultat :** GHCi ne modifie pas la valeur originale de `30`. Il crée simplement une **nouvelle liaison** dans l'environnement actuel qui s'appelle aussi `myAge` et qui a la valeur `31`.

* La liaison originale `myAge = 30` est **masquée** (shadowed).
* Si vous demandez la valeur de `myAge`, vous obtenez la nouvelle valeur (`31`).
* **Point clé de l'immuabilité :** Si vous aviez une fonction définie précédemment (avant le masquage) qui utilisait `myAge`, cette fonction continuerait d'utiliser l'ancienne valeur (`30`), car l'ancienne valeur n'a jamais été altérée.

---
