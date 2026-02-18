HC5T10 : Combiner les fonctions d’ordre supérieur
---
### Code Source Complet

```haskell
-- La fonction prend une liste d'entiers et renvoie un Booléen
checkSquareAbove50 :: [Int] -> Bool
checkSquareAbove50 xs = any (> 50) $ map (^2) xs

-- Note : Le 'filter' est ici implicitement géré par 'any' 
-- car 'any' combine le filtrage et la vérification logique.
-- Si l'on veut forcer l'usage de filter comme demandé :
checkWithFilter :: [Int] -> Bool
checkWithFilter xs = not $ null $ filter (> 50) $ map (^2) xs

main :: IO ()
main = do
    let liste1 = [1, 3, 5, 7] -- 7^2 = 49 (devrait être False)
    let liste2 = [1, 5, 8, 10] -- 8^2 = 64 (devrait être True)
    
    putStrLn $ "Liste [1,3,5,7] a un carré > 50 ? " ++ show (checkSquareAbove50 liste1)
    putStrLn $ "Liste [1,5,8,10] a un carré > 50 ? " ++ show (checkSquareAbove50 liste2)

```

---

### Explication du fonctionnement

Pour construire cette solution, nous utilisons un **pipeline de données** qui se lit de droite à gauche grâce à l'opérateur `$` :

1. **`map (^2) xs`** : On commence par prendre chaque élément de la liste `xs` et on l'élève au carré.
* *Exemple :* `[5, 8]` devient `[25, 64]`.


2. **`filter (> 50)`** : (Optionnel dans la logique pure mais demandé par l'exercice) On ne garde que les nombres qui dépassent 50.
* *Exemple :* `[25, 64]` devient `[64]`.


3. **`any (> 50)`** ou **`not . null`** :
* `any (> 50)` est la manière la plus élégante : elle parcourt la liste et s'arrête dès qu'elle trouve une valeur vraie. C'est ce qu'on appelle une évaluation "paresseuse" (lazy evaluation).
* Si on utilise `filter`, on vérifie si la liste résultante n'est pas vide (`not . null`).


---


Ici, on compose directement les fonctions. C'est très efficace car Haskell ne créera pas de liste intermédiaire complète en mémoire grâce à la fusion de boucles (stream fusion).

Souhaitez-vous que je vous explique comment fonctionne la **paresse (laziness)** de Haskell dans ce cas précis, notamment pourquoi il ne calcule pas tous les carrés si le premier est déjà supérieur à 50 ?
