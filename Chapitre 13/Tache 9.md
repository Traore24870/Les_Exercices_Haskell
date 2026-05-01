HC13T9 : Renommer un espace de noms de module
---
### Code Source (Main.hs)

```haskell
-- On renomme Data.List en 'L' et Data.Char en 'C'
import qualified Data.List as L
import qualified Data.Char as C

-- Fonction qui nettoie une chaîne : 
-- 1. Transforme en majuscules (via Char)
-- 2. Supprime les doublons (via List)
cleanAndUpper :: String -> String
cleanAndUpper input = L.nub (L.map C.toUpper input)

main :: IO ()
main = do
    let texte = "haskell est genial"
    
    putStrLn "--- Test du renommage d'espaces de noms ---"
    putStrLn $ "Texte original : " ++ texte
    
    -- Appel de notre fonction utilisant les deux alias
    let resultat = cleanAndUpper texte
    
    putStrLn $ "Résultat (Majuscules + Uniques) : " ++ resultat
```

---

### Explication technique

#### 1. L'alias ultra-court (`as L`, `as C`)
Dans les gros projets, les développeurs utilisent souvent une seule lettre pour les modules extrêmement fréquents. 
*   **`L.nub`** : On comprend immédiatement qu'il s'agit d'une opération sur les listes (L pour List).
*   **`C.toUpper`** : On comprend qu'il s'agit d'une opération sur un caractère (C pour Char).

#### 2. Utilisation combinée
Dans la fonction `cleanAndUpper`, nous voyons la puissance de cette approche :
*   `L.map` : Applique une fonction à chaque élément de la liste.
*   `C.toUpper` : La fonction appliquée (transforme un caractère en majuscule).
*   `L.nub` : Prend le résultat final pour supprimer les lettres répétées.

#### 3. Pourquoi renommer ?
*   **Éviter la répétition** : Écrire `Data.List.map` partout alourdit le code inutilement.
*   **Concision** : Cela permet de garder des lignes de code courtes, ce qui est très apprécié en Haskell pour la lisibilité.
*   **Professionnalisme** : C'est une convention standard dans la communauté Haskell (par exemple, `Data.Text` est presque toujours importé `as T`).

---
