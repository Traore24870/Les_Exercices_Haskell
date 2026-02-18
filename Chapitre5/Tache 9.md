HC5T9 : Fonction d’ordre supérieur pour transformer une liste
---
### Code Source Complet

```haskell
-- transformList prend une fonction (a -> a) et une liste [a]
-- Elle retourne une nouvelle liste transformée
transformList :: (a -> a) -> [a] -> [a]
transformList f xs = map (f . f) xs

-- Exemple d'utilisation
main :: IO ()
main = do
    let maListe = [1, 2, 3, 4, 5]
    -- On passe la fonction (+10) qui sera appliquée deux fois (+20 au total)
    let resultat = transformList (+10) maListe
    
    putStr "Liste originale : "
    print maListe
    putStr "Après transformList (+10) : "
    print resultat

```

---

### Explication Technique

#### 1. La signature `(a -> a) -> [a] -> [a]`

* **(a -> a)** : C'est le premier argument. C'est une fonction qui prend un type `a` et renvoie le même type `a`.
* **[a]** : C'est le deuxième argument, une liste d'éléments de type `a`.
* **[a] (retour)** : La fonction renvoie une liste modifiée.

#### 2. L'opérateur de composition `(.)`

L'expression `(f . f)` crée une nouvelle fonction. Si , alors .
L'utilisation du point `.` est beaucoup plus élégante que d'écrire `map (\x -> f (f x)) xs`.

#### 3. Fonction d'ordre supérieur

`transformList` est dite "d'ordre supérieur" car elle traite une autre fonction (`f`) comme une donnée (un argument). C'est l'un des piliers de la programmation fonctionnelle : on ne dit pas seulement *quoi* transformer, mais *comment* via une règle passée en paramètre.

---
