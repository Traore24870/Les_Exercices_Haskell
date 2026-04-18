HC11T10 : Fonction sortContainers
---
### Le Code Source (Main.hs)

```haskell
import Data.List (sort)

-- Nous réutilisons notre type Box avec dérivation automatique
-- L'instance Ord pour Box compare d'abord le constructeur, puis le contenu
data Box a = Box a deriving (Show, Eq, Ord)

-- LA FONCTION DEMANDÉE : sortContainers
-- Elle prend une liste de conteneurs et renvoie la liste triée.
-- Contrainte : 'c' doit être un type qui implémente Ord.
sortContainers :: Ord c => [c] -> [c]
sortContainers containers = sort containers

-- Fonction principale de test
main :: IO ()
main = do
    -- 1. Test avec des Box d'entiers
    let boxes = [Box 50, Box 10, Box 30, Box 20]
    putStrLn "--- Tri de boîtes d'entiers ---"
    putStrLn $ "Avant : " ++ show boxes
    putStrLn $ "Après : " ++ show (sortContainers boxes)
    
    -- 2. Test avec des Box de chaînes de caractères
    let wordBoxes = [Box "Zèbre", Box "Alpha", Box "Haskell"]
    putStrLn "\n--- Tri de boîtes de texte ---"
    putStrLn $ "Avant : " ++ show wordBoxes
    putStrLn $ "Après : " ++ show (sortContainers wordBoxes)
```

---

### Explication détaillée

#### 1. La Signature `Ord c => [c] -> [c]`
* **`c`** : Ici, `c` représente le type complet (par exemple `Box Int`). 
* **`Ord c =>`** : C'est la condition indispensable. On dit au compilateur : "Tu peux utiliser cette fonction sur n'importe quelle liste, tant que les éléments de la liste savent se comparer entre eux."
* **Pourquoi ne pas utiliser `Box a` dans la signature ?** En utilisant une variable de type générique `c`, notre fonction `sortContainers` est plus flexible. Elle pourrait trier des `Box`, des `Present`, ou même de simples entiers.

#### 2. Le fonctionnement du tri
La fonction `sort` (importée de `Data.List`) utilise l'algorithme **Merge Sort** (tri fusion). Son efficacité repose entièrement sur l'instance `Ord` que nous avons dérivée :
1.  Elle prend deux éléments de la liste.
2.  Elle appelle `compare` entre eux.
3.  Elle les réorganise selon que le résultat est `LT`, `EQ` ou `GT`.

#### 3. La dérivation récursive
C'est la magie du système de types de Haskell. Quand on écrit `deriving (Ord)` pour `Box a` :
* Haskell comprend que pour comparer deux `Box a`, il doit savoir comparer deux `a`.
* Si vous essayez de trier `[Box (Int -> Int)]`, le compilateur affichera une erreur car les fonctions ne sont pas dans la classe `Ord`.



apacité à définir des contrats stricts mais génériques qui rend Haskell si robuste pour les systèmes complexes comme les Blockchains ou les moteurs de calcul physique.
