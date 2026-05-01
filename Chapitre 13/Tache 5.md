HC13T5 : Restreindre la visibilité dans le module
---
```haskell
-- ==========================================
-- DÉFINITION DU MODULE (Logique interne)
-- ==========================================

-- Seule la fonction 'sumNonEmpty' est exportée. 
-- La fonction 'errorMessage' restera invisible pour l'utilisateur du module.
module SumNonEmpty (sumNonEmpty) where

-- Fonction utilitaire PRIVÉE (non exportée)
-- Elle centralise la gestion des messages pour éviter la répétition
errorMessage :: String
errorMessage = "ERREUR FATALE : Tentative de calcul sur une liste vide dans le module SumNonEmpty."

-- Fonction PUBLIQUE (exportée)
sumNonEmpty :: [Int] -> Int
sumNonEmpty [] = error errorMessage
sumNonEmpty xs = sum xs

-- ==========================================
-- PROGRAMME PRINCIPAL (Utilisateur du module)
-- ==========================================

-- Ici, on ne peut pas appeler 'errorMessage'. 
-- Si on essayait, Haskell renverrait une erreur de compilation.

main :: IO ()
main = do
    let listeValide = [5, 10, 15]
    
    putStrLn "--- Test de visibilité restreinte ---"
    
    -- Utilisation de la fonction autorisée
    putStr "Somme de [5, 10, 15] : "
    print (sumNonEmpty listeValide)
    
    -- Tentative d'utilisation de la liste vide
    putStrLn "\nTest de la sécurité interne..."
    print (sumNonEmpty [])
```

---

### Explication de la Refactorisation

#### 1. La liste d'exportation `(sumNonEmpty)`
En écrivant `module SumNonEmpty (sumNonEmpty) where`, vous créez une barrière de sécurité. Même si votre module contient 100 fonctions utilitaires, l'utilisateur du module (votre `main`) ne pourra en voir qu'une seule. C'est ce qu'on appelle la **réduction de la surface d'exposition**.

#### 2. L'utilité de `errorMessage` en privé
*   **Maintenance** : Si vous voulez changer le message d'erreur plus tard (par exemple, le traduire en anglais), vous n'avez qu'à le faire à un seul endroit dans le module.
*   **Propreté** : La fonction `sumNonEmpty` devient plus lisible car elle ne contient plus de longues chaînes de caractères au milieu de sa logique.

#### 3. Protection des données
En tant qu'étudiant en informatique, imaginez que `errorMessage` soit une clé de diagnostic système ou une configuration sensible. En la gardant hors de la liste d'exportation, vous garantissez qu'aucun autre programmeur ne pourra l'utiliser par erreur ou la modifier depuis l'extérieur du module.

### Ce qui se passe si vous essayez d'appeler `errorMessage` dans le `main` :
Si vous ajoutiez la ligne `putStrLn errorMessage` dans votre `main`, le compilateur GHC s'arrêterait immédiatement avec ce message :
> `Variable not in scope: errorMessage`

