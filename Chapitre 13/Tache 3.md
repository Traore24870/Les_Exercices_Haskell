HC13T3 : Trier et retourner les fichiers filtrés
---
### Code Source (Main.hs)

```haskell
import System.Directory (listDirectory)
import Data.List (isInfixOf, sort)

-- Fonction qui filtre puis trie la liste des fichiers
filterAndSortFiles :: String -> [FilePath] -> [FilePath]
filterAndSortFiles query fichiers = sort (filter (isInfixOf query) fichiers)

main :: IO ()
main = do
    putStrLn "Entrez le mot-clé pour filtrer les fichiers :"
    query <- getLine
    
    -- Récupération de la liste brute
    tousLesFichiers <- listDirectory "."
    
    -- Application du traitement (Filtre + Tri)
    let resultat = filterAndSortFiles query tousLesFichiers
    
    putStrLn $ "\n--- Résultats pour '" ++ query ++ "' (triés par ordre alphabétique) ---"
    if null resultat
        then putStrLn "Aucun fichier trouvé."
        else mapM_ putStrLn resultat
```

---

### Explication détaillée

#### 1. L'importance de l'ordre des opérations
Dans la fonction `filterAndSortFiles`, nous écrivons :
`sort (filter (isInfixOf query) fichiers)`
*   **D'abord le filtre** : On réduit la liste pour ne garder que ce qui nous intéresse. C'est plus efficace car le tri (qui est une opération plus lourde) s'appliquera sur une liste plus petite.
*   **Ensuite le tri** : La fonction **`sort`** du module `Data.List` range les éléments restants par ordre alphabétique (ordre croissant par défaut pour les chaînes de caractères).

#### 2. Composition de fonctions (Le style Haskell)
En Haskell, on pourrait aussi écrire cette fonction en utilisant l'opérateur de composition `.` pour un style plus "fonctionnel" :
```haskell
filterAndSortFiles query = sort . filter (isInfixOf query)
```
Cela se lit : "C'est la fonction `sort` **après** la fonction `filter`". C'est une manière très propre de construire des pipelines de données.

#### 3. Pourquoi trier est essentiel en informatique ?
Pour un technicien ou un développeur, l'ordre alphabétique est crucial lors de la gestion de fichiers :
*   **Versions** : Si vous cherchez des fichiers nommés `diag_v1`, `diag_v2`, le tri permet de les voir dans l'ordre chronologique de création si le nommage est bien fait.
*   **Lisibilité** : Dans un dossier contenant des centaines de fichiers système, une liste non triée est presque impossible à exploiter visuellement.

---
