HC13T4 : Module SumNonEmpty
---
### Code Source Combiné (Main.hs)

```haskell
-- ==========================================
-- LOGIQUE DU MODULE SumNonEmpty
-- ==========================================

-- Fonction qui calcule la somme d'une liste non vide
-- Si la liste est vide, on déclenche une erreur explicite
sumNonEmpty :: [Int] -> Int
sumNonEmpty [] = error "Erreur : La liste ne doit pas etre vide !"
sumNonEmpty xs = sum xs

-- ==========================================
-- PROGRAMME PRINCIPAL
-- ==========================================

main :: IO ()
main = do
    -- Définition de nos jeux de données pour le test
    let listeValide = [10, 20, 30, 40]
    let listeVide   = []
    
    putStrLn "--- Test de la fonction sumNonEmpty ---"
    
    -- Cas 1 : Test avec une liste contenant des entiers
    putStr "Somme de [10, 20, 30, 40] : "
    print (sumNonEmpty listeValide)
    
    -- Cas 2 : Test avec une liste vide
    -- ATTENTION : Cette ligne va arrêter le programme avec un message d'erreur
    putStrLn "\nTentative de calcul sur une liste vide..."
    print (sumNonEmpty listeVide)
```

---

### Explication de la combinaison

1.  **Suppression de l'import** : Comme tout est dans le même fichier, nous n'avons plus besoin de la ligne `import SumNonEmpty`. Cela évite l'erreur de "module non trouvé" que vous avez rencontrée précédemment.
2.  **Ordre des définitions** : En Haskell, l'ordre n'est pas strictement imposé pour les fonctions, mais il est plus lisible de définir vos outils (comme `sumNonEmpty`) en haut du fichier avant de les appeler dans le `main`.
3.  **Le comportement de l'erreur** : 
    *   Le premier test affichera correctement `100`.
    *   Le second test déclenchera l'instruction `error`. Dans votre terminal ou console en ligne, le programme s'arrêtera brusquement en affichant : `*** Exception: Erreur : La liste ne doit pas etre vide !`.

C'est une excellente façon de vérifier que vos "gardes" (sécurités) fonctionnent bien ! Une fois que vous avez testé le cas d'erreur, vous pouvez mettre la dernière ligne en commentaire (`-- print (sumNonEmpty listeVide)`) pour que le programme se termine "proprement".
```
