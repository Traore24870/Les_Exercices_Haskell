HC5T2 : Filtrer les nombres impairs
---
### Code source structuré (Haskell)

```haskell
-- 1. Définition de la fonction de signature (Le contrat)
-- Elle prend une liste d'entiers et renvoie une liste d'entiers
filtrerImpairs :: [Int] -> [Int]
filtrerImpairs liste = filter odd liste

-- 2. Fonction principale
main :: IO ()
main = do
    -- Création de la liste de 1 à 30
    let nombres = [1..30]
    
    -- Appel de notre fonction définie plus haut
    let resultat = filtrerImpairs nombres
    
    -- Affichage
    putStrLn "Liste des nombres impairs de 1 à 30 :"
    print resultat

```

1. **La Documentation** : La ligne `filtrerImpairs :: [Int] -> [Int]` indique immédiatement à n'importe quel développeur ce que fait la fonction sans même lire le code.
2. **La Sécurité (Le Typage)** : Haskell est extrêmement strict. Si vous essayez de passer une liste de mots (`String`) à cette fonction, le compilateur refusera de lancer le programme car il attend des `Int`.
3. **La Réutilisation** : En définissant la fonction à l'extérieur du `main`, vous pouvez l'utiliser partout ailleurs dans votre projet. Si elle est dans le `let` du `main`, elle est "prisonnière" et invisible pour le reste du code.

### Analyse de la signature `[Int] -> [Int]`

* **`[Int]`** : Les crochets signifient "une liste de...". Ici, une liste d'entiers.
* **`->`** : Symbolise la transformation.
* Le tout se lit : *"Prend une liste d'entiers en entrée et produit une liste d'entiers en sortie."*

