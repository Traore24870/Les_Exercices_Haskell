
HC2T6 - Tâche 6 : Comprendre Int vs Integer
---

### 1. Définition des variables

Dans GHCi, nous définissons les deux types d'entiers pour observer leur comportement :

* **`smallNumber = 2^62 :: Int`**
Le type `Int` est un entier de **précision fixe** (basé sur l'architecture de votre processeur). Sur un système 64 bits, sa valeur maximale est 2^{63}-1. 2^{62} est donc stocké sans erreur.
* **`bigNumber = 2^127 :: Integer`**
Le type `Integer` est un entier de **précision arbitraire**. Il n'a pas de limite de taille autre que la mémoire vive (RAM) de votre ordinateur.

### 2. Évaluation de `2^64 :: Int`

L'exécution de cette commande produit le résultat suivant :

> **Résultat : `0**`

### 3. Pourquoi ce résultat ? (Le phénomène d'Overflow)

Le résultat est `0` à cause d'un **dépassement de capacité** (*integer overflow*).

* **Stockage limité :** Un `Int` ne possède que 64 emplacements (bits) pour stocker l'information.
* **Le calcul :** En binaire, 2^{64} s'écrit avec un `1` suivi de 64 zéros. Ce nombre nécessite donc **65 bits**.
* **La coupure :** Haskell ne pouvant conserver que les 64 bits de droite, le `1` (le 65ème bit) est "jeté". Il ne reste alors que les 64 zéros, ce qui vaut mathématiquement `0`.

---

### Tableau Comparatif

| Type | Nature | Limite (64 bits) | Usage |
| --- | --- | --- | --- |
| **`Int`** | Précision fixe | -2^{63} à 2^{63}-1 | Rapide, optimisé pour le processeur. |
| **`Integer`** | Précision arbitraire | Aucune (limité par la RAM) | Calculs mathématiques de haute précision. |

