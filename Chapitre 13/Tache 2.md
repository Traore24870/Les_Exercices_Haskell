HC13T2 : Filtrer les fichiers par sous-chaîne
---

### Code Source (Main.hs)

```haskell
import System.Directory (listDirectory)
import Data.List (isInfixOf)

-- Fonction qui filtre la liste des fichiers selon une sous-chaîne
filterFiles :: String -> [FilePath] -> [FilePath]
filterFiles query fichiers = filter (isInfixOf query) fichiers

main :: IO ()
main = do
    putStrLn "Entrez la sous-chaîne à rechercher dans les noms de fichiers :"
    query <- getLine
    
    -- Récupération de tous les fichiers
    tousLesFichiers <- listDirectory "."
    
    -- Application du filtre
    let fichiersFiltres = filterFiles query tousLesFichiers
    
    putStrLn $ "--- Fichiers contenant '" ++ query ++ "' ---"
    if null fichiersFiltres
        then putStrLn "Aucun fichier ne correspond à votre recherche."
        else mapM_ putStrLn fichiersFiltres
```

---

### Explication détaillée

#### 1. Le module `Data.List` et `isInfixOf`
La fonction **`isInfixOf`** est l'outil parfait pour cette tâche. 
*   Elle prend deux listes (ici deux chaînes de caractères).
*   Elle retourne `True` si la première liste est contenue n'importe où dans la seconde.
*   *Exemple :* `"hs" \`isInfixOf\` "Main.hs"` retourne `True`.

#### 2. La fonction de haut niveau `filter`
Plutôt que d'écrire une boucle, on utilise la fonction native `filter`. 
*   `filter (isInfixOf query) fichiers` parcourt chaque élément de la liste `fichiers`.
*   Elle ne conserve l'élément que si la condition `isInfixOf query` est vraie.

#### 3. Logique du programme
*   On demande à l'utilisateur ce qu'il cherche (par exemple ".hs" pour voir les fichiers Haskell).
*   On récupère la liste brute via `listDirectory "."`.
*   On passe cette liste à notre fonction de filtrage.

---
