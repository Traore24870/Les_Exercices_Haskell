HC13T10 : Multi-modules de fonction principale
---
### Code Complet (Main.hs)

```haskell
import qualified System.Directory as Dir
import qualified Data.List as List
import qualified Data.Char as Char

-- Fonction de recherche : Filtre et Trie
-- Elle utilise le module Data.List (pour filter et sort) et Data.Char (pour toLower)
searchAndSort :: String -> [FilePath] -> [FilePath]
searchAndSort query fichiers = 
    let criteria = Char.toLower <$> query
        -- Filtrage insensible à la casse
        filtered = List.filter (\f -> criteria `List.isInfixOf` (Char.toLower <$> f)) fichiers
    in List.sort filtered

main :: IO ()
main = do
    putStrLn "=== Explorateur de fichiers Haskell ==="
    putStr "Entrez le nom (ou partie du nom) à rechercher : "
    query <- getLine
    
    -- 1. Récupération des fichiers via System.Directory
    tousLesFichiers <- Dir.listDirectory "."
    
    -- 2. Traitement des données
    let resultats = searchAndSort query tousLesFichiers
    
    -- 3. Affichage des résultats
    putStrLn $ "\nRésultats pour \"" ++ query ++ "\" :"
    if List.null resultats
        then putStrLn " Aucun fichier trouvé."
        else do
            putStrLn $ " [ " ++ show (List.length resultats) ++ " fichier(s) trouvé(s) ]"
            -- Correction : on utilise mapM_ directement (du Prelude)
            mapM_ (\f -> putStrLn $ "  - " ++ f) resultats
```

---

### Explication du Code

#### 1. Gestion des Modules et Espaces de Noms
*   **`import qualified ... as ...`** : Cette syntaxe permet d'utiliser des fonctions de plusieurs bibliothèques sans qu'elles ne se mélangent. Par exemple, `List.filter` appartient au module de manipulation de listes, tandis que `Dir.listDirectory` appartient au module de gestion du système de fichiers.
*   **Le cas `mapM_`** : Comme vous l'avez vu dans votre erreur, cette fonction n'est pas dans `Data.List`. Elle fait partie du **Prelude** (les fonctions de base chargées automatiquement). C'est pourquoi on l'écrit simplement `mapM_` sans préfixe.

#### 2. Logique de Recherche (`searchAndSort`)
*   **`Char.toLower <$> query`** : On transforme la recherche en minuscules. L'opérateur `<$>` (fmap) applique la transformation à chaque lettre de la chaîne de caractères.
*   **`List.isInfixOf`** : Cette fonction vérifie si une chaîne est contenue dans une autre.
*   **`List.sort`** : Une fois les fichiers trouvés, on les trie par ordre alphabétique pour une présentation propre.

#### 3. Interaction avec le Système (`IO`)
*   **`Dir.listDirectory "."`** : Cette fonction demande au système d'exploitation de lire le dossier actuel (`"."`).
*   **`getLine`** : Permet de récupérer la saisie de l'utilisateur de manière interactive.

### Pourquoi cette structure est importante pour vous ?
En tant qu'étudiant en **Licence 2 Informatique**, cette approche modulaire est exactement ce qui est attendu pour des projets rigoureux. Elle sépare :
1.  **L'acquisition des données** (système de fichiers).
2.  **Le traitement logique** (filtrage et tri).
3.  **L'interface utilisateur** (affichage dans la console).
