HC3T6 - Tâche avancée 6 : Vérifier une année bissextile avec if-then-else
---

### Code corrigé

Voici la version fonctionnelle qui respecte votre logique :

```haskell
isLeapYear :: Int -> Bool
isLeapYear annee =
    if annee `mod` 400 == 0
        then True
    else if annee `mod` 100 == 0 && annee `mod` 400 /= 0
        then False
    else if annee `mod` 4 == 0
        then True
    else False

main :: IO ()
main = do
    putStrLn (show (isLeapYear 2000))
    putStrLn (show (isLeapYear 1900))
    putStrLn (show (isLeapYear 2024))

```

---

### Explication des corrections

#### La logique des types

En Haskell, le type `Bool` n'accepte que deux valeurs : `True` et `False` (avec des majuscules). Si vous voulez absolument afficher "Vrai" ou "Faux" en français, il faudrait changer la signature de la fonction en `Int -> String`, mais pour un calcul logique, `Bool` est préférable.

#### L'affichage dans le `main`

* **Faux :** `putStrLn ++ show(...)` -> Le `++` sert à coller deux textes ensemble, pas à appliquer une fonction.
* **Juste :** `putStrLn (show (...))` -> Ici, `show` transforme le booléen en texte, puis `putStrLn` l'affiche.

