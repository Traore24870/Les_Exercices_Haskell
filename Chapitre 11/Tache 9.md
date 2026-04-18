HC11T9 : Type Length avec unités
---
### Le Code Source (Main.hs)

```haskell
-- Définition du type Length avec Mètres et Kilomètres
data Length = M Double | Km Double deriving (Show)

-- Implémentation manuelle de l'instance Eq
instance Eq Length where
    -- On convertit tout en mètres pour la comparaison
    (M m1)  == (M m2)  = m1 == m2
    (Km k1) == (Km k2) = k1 == k2
    (M m)   == (Km k)  = m == k * 1000
    (Km k)  == (M m)   = k * 1000 == m

-- Test de l'égalité intelligente
main :: IO ()
main = do
    let dist1 = M 1000
    let dist2 = Km 1
    let dist3 = M 500
    
    putStrLn "--- Test de comparaison d'unités ---"
    putStrLn $ "Est-ce que 1000m == 1km ? " ++ show (dist1 == dist2)
    putStrLn $ "Est-ce que 1km == 1000m ? " ++ show (dist2 == dist1)
    putStrLn $ "Est-ce que 500m == 1km ?  " ++ show (dist3 == dist2)
```

---

### Explication détaillée

#### 1. Pourquoi supprimer `deriving Eq` ?
En Haskell, si vous écrivez `deriving Eq`, le compilateur génère une fonction qui ressemble à ceci :
* `(M x) == (M y) = x == y`
* `(Km x) == (Km y) = x == y`
* `_ == _ = False` (Un `M` n'est jamais un `Km`)

Cela ne convient pas pour des unités de mesure. En supprimant la dérivation automatique, nous reprenons le contrôle total sur l'opérateur `==`.

#### 2. La logique de conversion
Dans l'instance manuelle, nous définissons quatre cas pour couvrir toutes les combinaisons possibles :
* **M vs M** et **Km vs Km** : Comparaison directe des nombres.
* **M vs Km** : On multiplie les kilomètres par 1000 pour obtenir des mètres avant de comparer.
* **Km vs M** : L'inverse (ou on peut simplement appeler l'autre définition).

#### 3. Le type `Double`
J'ai utilisé `Double` au lieu de `Int` pour permettre des mesures précises (comme `Km 1.5`). Notez que la comparaison de nombres flottants avec `==` peut parfois être capricieuse en informatique à cause de la précision, mais pour cet exercice de logique de type, c'est la méthode standard.



> **Astuce de peer :** En programmation fonctionnelle, on appelle souvent cela une **forme normale**. Ici, notre "forme normale" pour la comparaison est le mètre. Transformer toutes les données vers une unité commune est la stratégie la plus sûre pour éviter les erreurs de calcul.
