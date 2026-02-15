HC5T4 : Utiliser les fonctions lambda
---
### Code source (Haskell)

```haskell
-- 1. Signature de type : prend un entier (Int) et renvoie un Booléen
biggerThan10 :: Int -> Bool
-- 2. Définition utilisant une fonction lambda
biggerThan10 = \x -> x > 10

main :: IO ()
main = do
    let valeur = 15
    
    -- Utilisation de la fonction
    if biggerThan10 valeur
        then putStrLn (show valeur ++ " est plus grand que 10.")
        else putStrLn (show valeur ++ " est plus petit ou égal à 10.")

    -- Exemple d'usage courant : la lambda directement dans un filtre
    let nombres = [5, 12, 8, 20]
    -- Ici, la signature est implicitement (Int -> Bool) pour correspondre à la liste d'Int
    let resultat = filter (\x -> x > 10) nombres
    
    putStrLn "Nombres filtrés ( > 10 ) :"
    print resultat

```

---

### Pourquoi mettre une signature avec une lambda ?

Même si une lambda est par définition "anonyme", lorsqu'on l'assigne à un nom comme `biggerThan10`, elle se comporte comme n'importe quelle autre fonction. Lui donner une signature apporte plusieurs avantages :

* **Clarté immédiate** : `Int -> Bool` indique tout de suite que la fonction répond à une question (Vrai/Faux) sur un nombre.
* **Contrôle strict** : Si vous essayez plus tard d'appliquer `biggerThan10` à un caractère (`'a'`) ou une chaîne de caractères (`"15"`), Haskell générera une erreur de compilation précise grâce à cette signature.
* **Abstraction** : La signature définit le *quoi* (les types), tandis que la lambda définit le *comment* (la logique).

### Anatomie de la signature `Int -> Bool`

* **`biggerThan10`** : Le nom que nous donnons à notre expression lambda.
* **`::`** : Se lit "est de type".
* **`Int`** : Le type de l'argument à gauche de la flèche de la lambda (`\x`).
* **`->`** : Représente la transformation.
* **`Bool`** : Le type du résultat produit par l'expression `x > 10`.
