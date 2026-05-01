HC12T4 : Premiers 10 nombres de Fibonacci
---

### Code Source (Main.hs)

```haskell
-- Fonction récursive pour calculer le n-ième nombre de Fibonacci
fibonacci :: Int -> Int
fibonacci 0 = 0
fibonacci 1 = 1
fibonacci n = fibonacci (n - 1) + fibonacci (n - 2)

-- Génère une liste des n premiers nombres de Fibonacci
fibList :: Int -> [Int]
fibList n = [fibonacci i | i <- [0..n-1]]

main :: IO ()
main = do
    putStrLn "Les 10 premiers nombres de la suite de Fibonacci sont :"
    print (fibList 10)
```

---

### Explication détaillée

#### 1. La définition mathématique (Récursion double)
La suite de Fibonacci commence par 0 et 1, puis chaque nombre suivant est la somme des deux précédents : $F_n = F_{n-1} + F_{n-2}$.
*   **Cas de base** : On définit explicitement `fibonacci 0 = 0` et `fibonacci 1 = 1`.
*   **Cas récursif** : Pour tout $n > 1$, la fonction s'appelle elle-même deux fois.

#### 2. La compréhension de liste (List Comprehension)
La ligne `[fibonacci i | i <- [0..n-1]]` est une syntaxe très puissante en Haskell, similaire à la notation mathématique des ensembles :
*   `i <- [0..n-1]` : On crée d'abord une liste allant de 0 à 9.
*   `fibonacci i` : On applique la fonction à chaque élément de cette liste.
*   Le tout produit une nouvelle liste d'entiers `[Int]`.

#### 3. L'affichage de la liste
La fonction `print` est capable de formater automatiquement une liste Haskell. Elle affichera le résultat sous cette forme : `[0,1,1,2,3,5,8,13,21,34]`.

---

### Note sur l'optimisation
La récursion double telle qu'écrite ici est simple à comprendre mais devient lente pour de très grands nombres (car elle recalcule plusieurs fois les mêmes valeurs). Dans vos futurs projets en Haskell, vous découvrirez qu'on peut optimiser cela en utilisant des **listes infinies** et l'**évaluation paresseuse** (*lazy evaluation*), une des grandes forces du langage :

```haskell
-- Version avancée et ultra-rapide
fibs = 0 : 1 : zipWith (+) fibs (tail fibs)
-- Pour afficher les 10 premiers : take 10 fibs
```
