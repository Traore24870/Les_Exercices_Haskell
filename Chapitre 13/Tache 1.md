HC13T1 : Lister les fichiers du répertoire courant
---

Voici comment lister les fichiers d'un répertoire en utilisant le module `System.Directory`.

### Code Source (Main.hs)

```haskell
import System.Directory (listDirectory)

-- Fonction principale pour lister les fichiers
main :: IO ()
main = do
    putStrLn "--- Liste des fichiers dans le répertoire courant ---"
    
    -- Récupère la liste des fichiers et dossiers (sauf '.' et '..')
    fichiers <- listDirectory "."
    
    -- Affiche chaque élément de la liste
    if null fichiers
        then putStrLn "Le répertoire est vide."
        else mapM_ putStrLn fichiers
```

---

### Explication détaillée

#### 1. Le module `System.Directory`
Ce module est la bibliothèque standard de Haskell pour interagir avec le système de fichiers de votre ordinateur. Il permet de copier, déplacer, supprimer ou, comme ici, l'ister des éléments.

#### 2. La fonction `listDirectory`
*   Elle prend un chemin en argument (ici `"."`, qui représente le répertoire courant).
*   Elle retourne une action `IO [FilePath]`, c'est-à-dire une liste de chaînes de caractères contenant les noms des fichiers.
*   **Note importante** : Contrairement à d'anciennes fonctions comme `getDirectoryContents`, `listDirectory` est plus propre car elle ignore automatiquement les symboles de navigation `.` (répertoire actuel) et `..` (répertoire parent).

#### 3. L'opérateur `<-`
On utilise `fichiers <- listDirectory "."` pour "extraire" la liste de l'action entrées/sorties. Sans cet opérateur, vous manipuleriez une promesse d'action et non la liste elle-même.

#### 4. La fonction `mapM_`
C'est une fonction très puissante en Haskell :
*   **`map`** : Applique une fonction à chaque élément d'une liste.
*   **`M`** : Signifie que la fonction produit une action "Monadique" (ici une action `IO` comme `putStrLn`).
*   **`_`** : Indique que l'on ignore le résultat final de l'opération (on veut juste l'affichage, pas une liste de retour).
*   En résumé, `mapM_ putStrLn fichiers` parcourt votre liste et affiche chaque nom de fichier sur une nouvelle ligne.

---

