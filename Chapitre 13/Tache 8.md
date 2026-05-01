HC13T8 : Importations qualifiées pour les conflits de noms
---
### 1. Le Problème : Le Conflit
Si vous écrivez `import Data.List` et `import Data.Map`, et que vous essayez d'utiliser la fonction `filter`, Haskell ne saura pas laquelle choisir et renverra une erreur d'ambiguïté.

### 2. La Solution : L'Importation Qualifiée (Main.hs)

Voici comment gérer proprement ce conflit en utilisant des alias.

```haskell
import qualified Data.List as List
import qualified Data.Map as Map

-- Imaginons que nous avons une liste de fichiers
-- et que nous voulons aussi utiliser une Map (comme dans l'exercice HC13T6)

main :: IO ()
main = do
    let nombres = [1, 2, 3, 4, 5, 2, 3]
    
    putStrLn "--- Gestion des conflits de noms ---"
    
    -- 1. Utilisation de la fonction 'filter' du module List
    -- On doit obligatoirement utiliser le préfixe List.
    let pairs = List.filter even nombres
    putStr "Nombres pairs (via List.filter) : "
    print pairs
    
    -- 2. Utilisation d'une fonction de Map avec le même nom (si on avait une Map)
    -- let maMap = Map.fromList [(1, "A"), (2, "B")]
    -- let mapFiltree = Map.filter (== "A") maMap
    
    -- 3. Utilisation de 'nub' (supprime les doublons) de Data.List
    let uniques = List.nub nombres
    putStr "Nombres uniques (via List.nub) : "
    print uniques
```

---

### Explication technique

#### Le mot-clé `qualified`
Il indique à Haskell que les fonctions du module ne seront pas disponibles "en vrac" dans votre code. Vous **devez** les précéder du nom du module ou de son alias.

#### L'alias `as ...`
C'est un raccourci pour plus de confort. 
*   Au lieu d'écrire `Data.List.filter`, on écrit simplement `List.filter`.
*   C'est une convention très utilisée en Haskell, tout comme on utilise souvent `Map` pour `Data.Map` ou `Set` pour `Data.Set`.

#### Pourquoi est-ce une bonne pratique ?
1.  **Clarté** : N'importe quel développeur qui lit votre code sait immédiatement d'où vient la fonction.
2.  **Éviter les erreurs** : Cela empêche le compilateur de mélanger des fonctions qui portent le même nom mais ont des comportements différents.
3.  **Maintenance** : Dans vos projets complexes (comme la gestion de votre parking scolaire), cela évite que l'ajout d'une nouvelle bibliothèque ne casse votre code existant à cause d'un nom de fonction déjà utilisé.
