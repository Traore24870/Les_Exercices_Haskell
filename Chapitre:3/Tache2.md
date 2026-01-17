HC3T2 - Tâche 2 : Déterminer la note à partir d'un score avec des gardes
---
Voici la solution pour la **Tâche 2**, en utilisant cette fois-ci les **gardes** (`|`). Cette syntaxe est beaucoup plus élégante et lisible en Haskell que les instructions `if-then-else` imbriquées lorsqu'il y a plusieurs conditions.

---

## Code Source (Main.hs)

```haskell
import System.IO (hSetEncoding, stdout, utf8)

-- Définition de la fonction avec des gardes
grade :: Int -> String
grade score
    | score >= 90 = "A"
    | score >= 80 = "B"
    | score >= 70 = "C"
    | score >= 60 = "D"
    | otherwise   = "F"

-- Fonction de test
main :: IO ()
main = do
    hSetEncoding stdout utf8
    putStrLn $ "Score 95 : " ++ grade 95
    putStrLn $ "Score 72 : " ++ grade 72
    putStrLn $ "Score 50 : " ++ grade 50

```

---

## Explications Techniques

### 1. Le fonctionnement des Gardes (`|`)

Les gardes fonctionnent comme une liste de conditions testées de haut en bas. Dès qu'une condition est vraie, le résultat correspondant est retourné et les suivantes sont ignorées.

* L'ordre est crucial : si nous avions mis `score >= 60` en premier, un score de 95 aurait retourné "D" ! On commence donc par la valeur la plus haute.

### 2. Le mot-clé `otherwise`

Le mot-clé `otherwise` est simplement un alias pour `True`. Il est utilisé à la fin pour capturer tous les cas restants (ici, tout ce qui est inférieur à 60). C'est l'équivalent du `else` final.

### 3. L'opérateur `$`

Dans le `main`, j'ai utilisé l'opérateur `$`. C'est une astuce de syntaxe en Haskell qui permet d'éviter les parenthèses.

* `putStrLn $ "..."` est identique à `putStrLn ("...")`.

---

### Résultat attendu

```text
Score 95 : A
Score 72 : C
Score 50 : F

```
