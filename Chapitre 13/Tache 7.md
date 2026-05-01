HC13T7 : Utiliser un module personnalisé dans main
---
### Code Source (Main.hs)

```haskell
-- ==========================================
-- MODULE SumNonEmpty
-- ==========================================
module SumNonEmpty (sumNonEmpty) where

-- On définit la fonction avec une sécurité contre les listes vides
sumNonEmpty :: [Int] -> Int
sumNonEmpty [] = error "ERREUR : La liste est vide."
sumNonEmpty xs = sum xs

-- ==========================================
-- PROGRAMME PRINCIPAL (Utilisation du module)
-- ==========================================
-- Dans un vrai projet, cette partie serait dans un fichier Main.hs
-- et on utiliserait : import SumNonEmpty (sumNonEmpty)

main :: IO ()
main = do
    -- 1. Définition de la liste de nombres
    let mesNombres = [12, 45, 7, 23, 13]
    
    putStrLn "--- Calcul de somme via module personnalisé ---"
    
    -- 2. Appel de la fonction du module
    let resultat = sumNonEmpty mesNombres
    
    -- 3. Affichage du résultat
    putStr "La somme de la liste "
    print mesNombres
    putStr "Résultat final : "
    print resultat
```

---

### Points clés de l'exercice

*   **Modularité** : Le code est séparé en deux blocs distincts. Le bloc `module` contient la logique de calcul "métier", tandis que le bloc `main` gère l'interface utilisateur et l'affichage.
*   **Signature de type** : La fonction `sumNonEmpty` est strictement typée pour accepter une liste d'entiers (`[Int]`) et retourner un entier (`Int`), ce qui garantit la cohérence des données lors de l'appel dans le `main`.
*   **Sécurité** : Si vous aviez besoin de traiter des données issues d'un système de gestion (comme le parc automobile que vous avez étudié), cette structure permet d'intercepter les erreurs avant qu'elles ne corrompent vos calculs.

### Résultat attendu dans le terminal
```text
--- Calcul de somme via module personnalisé ---
La somme de la liste [12,45,7,23,13]
Résultat final : 100
```
