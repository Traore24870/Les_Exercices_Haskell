HC5T1 : Utiliser applyTwice
---
### Code source (Haskell)

```haskell
-- Définition de la fonction applyThrice
applyThrice :: (Int -> Int) -> Int -> Int
applyThrice f x = f (f (f x))

-- Fonction principale (le Main)
main :: IO ()
main = do
    -- Définition d'une fonction locale qui ajoute 2
    let ajouterDeux n = n + 2
    
    let valeurInitiale = 10
    
    -- Appel de la fonction
    let resultat = applyThrice ajouterDeux valeurInitiale
    
    -- Affichage du résultat
    putStrLn ("Valeur de départ : " ++ show valeurInitiale)
    putStrLn ("Après avoir appliqué la fonction 3 fois : " ++ show resultat)

```
### Explication du code Haskell
---

### 1. La Signature de Type (Le "Contrat")

```haskell
applyThrice :: (Int -> Int) -> Int -> Int

```

C'est l'étape la plus importante en Haskell. Elle définit précisément ce que la fonction accepte et renvoie :

* **(Int -> Int)** : Le premier argument est une **fonction**. Cette parenthèse dit : "Donne-moi une fonction qui prend un entier et renvoie un entier" (comme `+2` ou `*3`).
* **Int** : Le deuxième argument est l'entier initial ().
* **-> Int** : Le résultat final sera un entier.

### 2. La Définition (La Logique)

```haskell
applyThrice f x = f (f (f x))

```

Haskell utilise la **composition de fonctions**. Le calcul s'effectue de l'intérieur vers l'extérieur :

1. On calcule d'abord `(f x)`.
2. Le résultat est passé à la deuxième fonction `f`.
3. Ce nouveau résultat est passé à la dernière fonction `f`.

### 3. Le bloc Main et le "do"

```haskell
main = do
    let ajouterDeux n = n + 2
    let resultat = applyThrice ajouterDeux 10

```

* **`main :: IO ()`** : En Haskell, toute action qui affiche quelque chose à l'écran (entrée/sortie) doit être dans le `main` avec le type `IO`.
* **`do`** : Ce mot-clé permet d'enchaîner des instructions ligne par ligne (comme dans un langage classique).
* **`let`** : Sert à définir des variables ou des petites fonctions locales. Ici, on crée `ajouterDeux`.
* **`applyThrice ajouterDeux 10`** : On donne la fonction `ajouterDeux` à `applyThrice`. Remarquez qu'il n'y a **pas de parenthèses** ni de virgules entre les arguments ; c'est la syntaxe standard de Haskell.

### 4. L'Affichage

```haskell
putStrLn ("Résultat : " ++ show resultat)

```

* **`putStrLn`** : (Put String Line) Affiche du texte.
* **`show`** : C'est crucial. En Haskell, on ne peut pas mélanger du texte et des nombres. `show` transforme l'entier `16` en chaîne de caractères `"16"` pour qu'il puisse être collé au reste de la phrase avec l'opérateur `++`.

---
