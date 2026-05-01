HC12T3 : Fonction factorielle
---
### Code Source (Main.hs)

```haskell
-- Définition de la fonction factorielle avec filtrage de motifs (pattern matching)
factorial :: Int -> Int
factorial 0 = 1
factorial n = n * factorial (n - 1)

-- Point d'entrée pour tester la fonction
main :: IO ()
main = do
    let nombre = 5
    let resultat = factorial nombre
    putStr "La factorielle de "
    putStr (show nombre)
    putStr " est : "
    print resultat
```

---

### Explication détaillée

#### 1. Le Pattern Matching (Filtrage de motifs)
Au lieu d'utiliser un `if/else` classique, nous définissons la fonction en deux étapes :
*   **`factorial 0 = 1`** : C'est notre **cas de base**. La factorielle de 0 est mathématiquement égale à 1. Cela permet d'arrêter la récursion.
*   **`factorial n = n * factorial (n - 1)`** : C'est le **cas récursif**. Pour calculer $n!$, on multiplie $n$ par la factorielle de $n-1$.

#### 2. La logique de récursion
Si on appelle `factorial 3`, Haskell va décomposer le calcul ainsi :
1.  `3 * factorial 2`
2.  `3 * (2 * factorial 1)`
3.  `3 * (2 * (1 * factorial 0))`
4.  `3 * (2 * (1 * 1))` $\rightarrow$ **6**

#### 3. Affichage combiné
Dans le `main`, nous utilisons une petite variante pour l'affichage :
*   **`putStr`** : Affiche le texte sans retourner à la ligne immédiatement.
*   **`show`** : Transforme le nombre en `String` pour qu'il puisse être utilisé par `putStr`.
*   **`print`** : Affiche le résultat final et termine la ligne.

---

### Une version plus robuste (Optionnelle)
En informatique, on utilise parfois des "gardes" (`guards`) pour éviter les erreurs si l'utilisateur saisit un nombre négatif :

```haskell
factorialGuarded :: Int -> Int
factorialGuarded n
    | n < 0     = error "La factorielle n'est pas définie pour les nombres négatifs"
    | n == 0    = 1
    | otherwise = n * factorialGuarded (n - 1)
```
Les barres verticales `|` agissent comme des conditions logiques très lisibles en Haskell.
