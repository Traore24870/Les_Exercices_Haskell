HC12T2 : Additionner deux nombres
---

### Code Source (Main.hs)

```haskell
-- Fonction qui additionne deux entiers
addTwoNumbers :: Int -> Int -> Int
addTwoNumbers x y = x + y

-- Point d'entrée du programme
main :: IO ()
main = do
    let resultat = addTwoNumbers 15 27
    putStrLn "Le résultat de l'addition est :"
    print resultat
```

---

### Explication détaillée

#### 1. La fonction `addTwoNumbers`
*   **Signature (`Int -> Int -> Int`)** : En Haskell, cela se lit ainsi : la fonction prend un premier `Int`, puis un second `Int`, et retourne un `Int`.
*   **Logique** : Contrairement à d'autres langages, il n'y a pas de mot-clé `return`. La dernière expression évaluée (`x + y`) est automatiquement la valeur de retour.

#### 2. Le mot-clé `let`
À l'intérieur d'un bloc `do`, on utilise `let` pour définir des variables locales ou stocker le résultat d'un calcul pur (comme notre addition) avant de l'utiliser dans une action d'affichage.

#### 3. La fonction `print`
Vous remarquerez que nous utilisons `print` au lieu de `putStrLn` pour le résultat :
*   **`putStrLn`** : Ne fonctionne qu'avec des chaînes de caractères (`String`).
*   **`print`** : Est une fonction très pratique qui transforme automatiquement un nombre (ou d'autres types de données) en texte avant de l'afficher. C'est l'équivalent de faire `putStrLn (show resultat)`.

---
