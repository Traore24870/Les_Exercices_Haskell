HC9T3 : Fonction pour additionner les valeurs dans une Box
---
---

### Code Source (Haskell)

```haskell
-- Définition du type Box (comme précédemment)
data Box a = Empty | Has a 
    deriving (Show)

-- 1. Définition de la fonction addN
-- On précise que 'a' doit appartenir à la classe Num (nombres)
addN :: Num a => a -> Box a -> Box a
addN n Empty   = Empty          -- Si la boîte est vide, elle reste vide
addN n (Has x) = Has (x + n)    -- Si elle contient x, on emballe (x + n)

-- 2. Fonction principale main()
main :: IO ()
main = do
    let n = 10
    let box1 = Has 5
    let box2 = Empty :: Box Int

    putStrLn $ "Nombre à ajouter : " ++ show n
    
    -- Test avec une boîte pleine
    let result1 = addN n box1
    putStrLn $ "Test avec Has 5  -> " ++ show result1

    -- Test avec une boîte vide
    let result2 = addN n box2
    putStrLn $ "Test avec Empty  -> " ++ show result2
```

---

### Explication détaillée du code

#### La signature `Num a => a -> Box a -> Box a`
* **`Num a =>`** : C'est une contrainte de classe. Elle indique que le type `a` ne peut pas être n'importe quoi (comme une String) ; il doit s'agir d'un type numérique (Int, Float, Double) pour que l'addition `+` soit possible.
* **`a -> Box a -> Box a`** : La fonction prend un nombre de type `a`, une boîte contenant un `a`, et renvoie une nouvelle boîte de même type.

#### Le mécanisme de la fonction `addN`
La fonction utilise deux branches de **pattern matching** pour couvrir tous les cas de figure :

1.  **Le cas `Empty`** : Si vous essayez d'ajouter 10 à "rien", le résultat est toujours "rien". La fonction renvoie donc `Empty`. Cela permet d'éviter les erreurs de calcul sur des données absentes.
2.  **Le cas `Has x`** : La fonction "ouvre" la boîte, extrait la valeur `x`, lui ajoute `n`, puis utilise le constructeur `Has` pour replacer le résultat dans une nouvelle boîte.

#### Sécurité du code
L'avantage de cette approche est qu'elle est **pure**. Vous n'avez pas besoin de vérifier manuellement si la boîte est vide avec un `if/else` complexe ou de risquer une erreur de pointeur nul. Le type `Box` force la gestion du cas vide dès la compilation.

---
