
HC2T2 - Tâche 2 : Signatures de fonctions
---
Voici les signatures de types (type signatures) et les implémentations pour les trois fonctions demandées.

###📝 1. Fonction `add`Cette fonction additionne deux entiers.

* **Signature de Type (Type Signature) :**
La fonction prend un `Int`, puis un autre `Int`, et retourne un `Int` (leur somme).
```haskell
add :: Int -> Int -> Int

```


* **Implémentation :**
```haskell
add x y = x + y

```



###📝 2. Fonction `isEven`Cette fonction vérifie si un entier est pair, retournant `True` ou `False`.

* **Signature de Type (Type Signature) :**
La fonction prend un `Int` et retourne un `Bool`.
```haskell
isEven :: Int -> Bool

```


* **Implémentation (Utilisation de l'opérateur modulo `mod`) :**
Pour être pair, le reste de la division par 2 doit être 0.
```haskell
isEven n = n `mod` 2 == 0

```


> *(Alternative : Haskell fournit une fonction prédéfinie `even` qui a la même signature : `even :: Integral a => a -> Bool`)*



###📝 3. Fonction `concatStrings`Cette fonction combine deux chaînes de caractères.

* **Signature de Type (Type Signature) :**
La fonction prend une `String`, puis une autre `String`, et retourne une `String` (la chaîne combinée).
```haskell
concatStrings :: String -> String -> String

* **Implémentation (Utilisation de l'opérateur de concaténation `++`) :**
```haskell
concatStrings s1 s2 = s1 ++ s2



Prelude> concatStrings "Haskell " "est genial"
"Haskell est genial"

```
