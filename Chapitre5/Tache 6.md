HC5T6 : Composition de fonctions
---
### Code source (Haskell)

```haskell
-- 1. Signature de type
-- Prend une liste d'entiers et retourne une liste d'entiers
carresPairs :: [Int] -> [Int]
-- 2. Définition par composition de fonctions
-- On lit de droite à gauche : d'abord on calcule les carrés, puis on filtre
carresPairs = filter even . map (\x -> x * x)

-- 3. Fonction principale pour le test
main :: IO ()
main = do
    let nombres = [1, 2, 3, 4, 5, 6]
    
    -- Appel de la fonction composée
    let resultat = carresPairs nombres
    
    putStrLn ("Liste originale : " ++ show nombres)
    putStrLn ("Carrés des nombres, gardant uniquement les pairs :")
    print resultat

```

---

### Explication détaillée

#### 1. L'opérateur de composition `(.)`

L'opérateur `.` permet de coller deux fonctions ensemble pour n'en former qu'une seule.

* **Syntaxe** : `(fonctionFinale . fonctionInitiale)`
* **Flux de données** : Les données entrent par la droite, passent par la première fonction, et le résultat est envoyé à la fonction suivante.

#### 2. Décomposition de notre pipeline

Dans notre expression `filter even . map (\x -> x * x)` :

1. **`map (\x -> x * x)`** : C'est la première étape (à droite). Elle prend la liste d'entrée et calcule le carré de chaque nombre.
* *Exemple* : `[1, 2, 3, 4]` devient `[1, 4, 9, 16]`.


2. **`filter even`** : C'est la deuxième étape. Elle reçoit la liste de carrés et ne garde que ceux qui sont pairs.
* *Exemple* : `[1, 4, 9, 16]` devient `[4, 16]`.



#### 3. Pourquoi ne pas mettre d'argument `liste` ?

Vous remarquerez que j'ai écrit :
`carresPairs = filter even . map (\x -> x * x)`
au lieu de :
`carresPairs liste = filter even (map (\x -> x * x) liste)`

C'est ce qu'on appelle le style **"Point-free"**. Puisque les deux côtés de l'équation attendent une liste, on peut les omettre. C'est une manière très courante et très "propre" d'écrire en Haskell, car cela met l'accent sur la transformation des données plutôt que sur les variables elles-mêmes.

#### 4. Le résultat

Si on teste avec `[1, 2, 3, 4, 5]`, le programme fait :

* Carrés : `1, 4, 9, 16, 25`
* Filtre (pairs uniquement) : `4, 16`
