
## 💻HC1T1 - Tâche 1 : Composition de fonctions

Le code inclut les définitions des trois fonctions et une section `main` pour tester leur exécution.

```haskell
-- Définition de la fonction 'double'
-- Elle prend un nombre (a) et retourne ce nombre multiplié par 2.
double :: Num a => a -> a
double n = n * 2

-- Définition de la fonction 'increment'
-- Elle prend un nombre (a) et retourne ce nombre augmenté de 1.
increment :: Num a => a -> a
increment n = n + 1

-- Définition de la fonction 'doubleThenIncrement'
-- Elle utilise la composition de fonctions (l'opérateur '.') pour
-- appliquer d'abord 'double', puis 'increment'.
doubleThenIncrement :: Num a => a -> a
doubleThenIncrement = increment . double

-- Bloc principal pour tester les fonctions
main :: IO ()
main = do
    let nombreInitial = 5
    
    putStrLn "--- Composition de Fonctions ---"
    
    -- Test de 'double'
    let resultatDouble = double nombreInitial
    putStrLn $ "1. double(" ++ show nombreInitial ++ ") = " ++ show resultatDouble ++ " (Résultat: 10)"
    
    -- Test d' 'increment'
    let resultatIncrement = increment resultatDouble
    putStrLn $ "2. increment(" ++ show resultatDouble ++ ") = " ++ show resultatIncrement ++ " (Résultat: 11)"
    
    putStrLn ""
    
    -- Test de la composition 'doubleThenIncrement'
    let resultatComposition = doubleThenIncrement nombreInitial
    putStrLn $ "3. doubleThenIncrement(" ++ show nombreInitial ++ ") (increment . double) = " ++ show resultatComposition ++ " (Résultat final: 11)"

    -- Test avec un autre nombre
    let autreNombre = 10
    putStrLn $ "\nTest supplémentaire : doubleThenIncrement(" ++ show autreNombre ++ ") = " ++ show (doubleThenIncrement autreNombre) ++ " (Résultat: 21)"
```

-----

## 📝 Explication Détaillée du Code

### 1\. Définitions des Fonctions de Base

  * **`double :: Num a => a -> a`**

      * **Signature de Type** : Indique que `double` prend un argument de n'importe quel type `a` qui appartient à la classe de types **`Num`** (c'est-à-dire un type numérique, comme `Int` ou `Float`) et retourne une valeur du même type `a`.
      * **Définition** : `double n = n * 2` effectue la multiplication par 2.

  * **`increment :: Num a => a -> a`**

      * **Signature de Type** : Similaire à `double`, elle opère sur tout type numérique `a`.
      * **Définition** : `increment n = n + 1` ajoute 1 à l'argument `n`.

### 2\. Composition de Fonctions (`doubleThenIncrement`)

  * **`doubleThenIncrement :: Num a => a -> a`**

      * **Définition** : `doubleThenIncrement = increment . double`

    C'est le cœur de l'exercice : l'utilisation de l'opérateur de composition **`.`** (point).

      * **Composition (`.`):** En Haskell (et en mathématiques), l'opérateur de composition **$f \circ g$** (ou $f . g$ en Haskell) signifie **"appliquer $g$, puis appliquer $f$ au résultat de $g$"**.
      * Dans notre cas, `increment . double` signifie :
        1.  **D'abord**, appliquer la fonction la **plus à droite** : **`double`**
        2.  **Ensuite**, appliquer la fonction la **plus à gauche** au résultat : **`increment`**
      * Si on appelle `doubleThenIncrement 5`, l'exécution sera :
        1.  `double 5` $\rightarrow 10$
        2.  `increment 10` $\rightarrow 11$

### 3\. Bloc Principal pour le Test (`main`)

  * **`main :: IO ()`** : La fonction `main` est le point d'entrée d'un programme Haskell exécutable. Elle retourne une action d'entrée/sortie (`IO ()`).
  * **`let nombreInitial = 5`** : Déclare une variable locale pour les tests.
  * **`putStrLn ...`** : Utilisé pour afficher du texte à l'écran.
  * **`show`** : La fonction `show` est essentielle pour l'affichage. Elle prend une valeur (comme le nombre 5) et la convertit en une chaîne de caractères (`String`) afin qu'elle puisse être concaténée avec d'autres chaînes pour l'affichage.

Le bloc `main` démontre que le résultat de l'exécution séquentielle de `double` puis `increment` (qui donne 11) est **identique** au résultat de l'appel direct à la fonction composée `doubleThenIncrement` (qui donne également 11).
