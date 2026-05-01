HC13T6 : Convertir des fichiers filtrés en map
---
### Code Source Combiné (Main.hs)

```haskell
import System.Directory (listDirectory)
import Data.List (isInfixOf)
import qualified Data.Map as Map

-- Fonction qui convertit une liste de fichiers en Map (Nom -> Longueur du nom)
createFileMap :: [FilePath] -> Map.Map FilePath Int
createFileMap fichiers = Map.fromList [(f, length f) | f <- fichiers]

main :: IO ()
main = do
    putStrLn "Entrez une extension ou un mot-clé pour filtrer (ex: .hs) :"
    query <- getLine
    
    -- 1. Récupération des fichiers
    tousLesFichiers <- listDirectory "."
    
    -- 2. Filtrage (comme vu précédemment)
    let fichiersFiltres = filter (isInfixOf query) tousLesFichiers
    
    -- 3. Conversion en Map
    let maMap = createFileMap fichiersFiltres
    
    putStrLn $ "\n--- Map des fichiers filtrés (Clé: Nom, Valeur: Taille du nom) ---"
    if Map.null maMap
        then putStrLn "La Map est vide."
        else print maMap
```

---

### Explication détaillée

#### 1. L'import qualifié `qualified Data.Map as Map`
Le module `Data.Map` contient des fonctions dont les noms (comme `filter` ou `lookup`) existent déjà dans le prélude standard de Haskell. En utilisant `qualified`, on oblige le programme à utiliser le préfixe `Map.` (ex: `Map.fromList`). Cela évite les conflits de noms et rend votre code beaucoup plus professionnel.

#### 2. La fonction `Map.fromList`
C'est la méthode la plus simple pour créer une Map. Elle prend une **liste de tuples** `[(clé, valeur)]`. 
Dans notre cas, nous utilisons une compréhension de liste : `[(f, length f) | f <- fichiers]`.
*   **Clé** : Le nom du fichier (`FilePath`).
*   **Valeur** : Le nombre de caractères du nom (`Int`).

#### 3. Pourquoi utiliser une Map ?
Dans un projet de diagnostic informatique ou de gestion de parc automobile (comme celui que vous avez commencé en Java), une Map est extrêmement efficace car :
*   **Recherche rapide** : Trouver une information associée à un fichier (comme son chemin complet ou sa date de modification) est beaucoup plus rapide dans une Map que dans une simple liste.
*   **Unicité** : Une Map garantit qu'il n'y a pas de doublons pour les clés.

