## ➕ HC1T6 - Tâche 6 : Utilisation de signatures de type

```haskell
-- Définition de la fonction 'addNumbers'.
-- Elle prend deux entiers 'a' et 'b', et retourne leur somme.
-- Le type 'Int' est utilisé pour les nombres entiers standard.
addNumbers :: Int -> Int -> Int
addNumbers a b = a + b

-- Bloc principal pour tester la fonction
main :: IO ()
main = do
    let nombre1 = 15
    let nombre2 = 27
    let nombre3 = 100
    let nombre4 = (-50)
    
    putStrLn "--- Addition de Deux Nombres ---"
    
    -- Test 1 : Addition simple
    let resultat1 = addNumbers nombre1 nombre2
    putStrLn $ show nombre1 ++ " + " ++ show nombre2 ++ " = " ++ show resultat1 -- Résultat: 42
    
    -- Test 2 : Addition avec un nombre négatif
    let resultat2 = addNumbers nombre3 nombre4
    putStrLn $ show nombre3 ++ " + (" ++ show nombre4 ++ ") = " ++ show resultat2 -- Résultat: 50
    
    -- Test de l'application partielle (Currying)
    let addFive = addNumbers 5
    let resultat3 = addFive 10
    putStrLn $ "Application partielle (5 + 10) = " ++ show resultat3 -- Résultat: 15
```

-----

## 💡 Explication

1.  **Signature de Type** : `addNumbers :: Int -> Int -> Int`

      * La signature indique que `addNumbers` prend un premier argument de type **`Int`** (entier), puis un second argument de type **`Int`**, et enfin retourne un résultat de type **`Int`** (leur somme).

2.  **Définition de la Fonction** : `addNumbers a b = a + b`

      * Elle utilise l'opérateur arithmétique standard **`+`** pour effectuer l'addition.

### La Curification (Currying)

Notez l'exemple de **l'application partielle** dans le bloc `main` :

```haskell
let addFive = addNumbers 5
let resultat3 = addFive 10
```

En Haskell, toutes les fonctions prenant plusieurs arguments sont automatiquement *curifiées* (curried).

  * `addNumbers 5` ne retourne pas une erreur, mais retourne une **nouvelle fonction** qui attend le deuxième argument (`b`) et lui ajoute la valeur `5`.
  * Cette nouvelle fonction (`addFive`) est ensuite appelée avec l'argument `10`, donnant le résultat `15`. C'est une caractéristique puissante du langage \!
