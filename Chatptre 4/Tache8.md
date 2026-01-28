HC4T8 - Tâche 8 : Extraire des valeurs de tuples
---
### Le Code Haskell

Voici une fonction qui prend un tuple de trois éléments (un nom, un âge et une ville) et les extrait pour créer une phrase.

```haskell
-- Le tuple contient (String, Int, String)
decrireTuple :: (String, Int, String) -> String
decrireTuple (nom, age, ville) = 
    nom ++ " a " ++ show age ++ " ans et habite à " ++ ville ++ "."

main :: IO ()
main = do
    let personne = ("Alice", 25, "Paris")
    putStrLn (decrireTuple personne)
    putStrLn (decrireTuple ("Bob", 40, "Lyon"))

```

---

### Explications détaillées

#### 1. La structure du Tuple

En Haskell, un tuple comme `(String, Int, String)` est une structure où chaque position a un type précis. On ne peut pas mélanger un tuple de 2 éléments avec un tuple de 3 éléments ; ce sont des types totalement différents.

#### 2. L'extraction par Pattern Matching

Dans la ligne `decrireTuple (nom, age, ville)`, nous ne faisons pas que recevoir un argument, nous le **décomposons** :

* Le premier élément du tuple est automatiquement lié à la variable `nom`.
* Le deuxième est lié à `age`.
* Le troisième est lié à `ville`.

#### 3. Combinaison des données

* **`show age`** : Comme l'âge est un entier (`Int`), on doit le convertir en texte avant de pouvoir le "coller" aux autres chaînes de caractères.
* **L'opérateur `++**` : Il sert à concaténer les morceaux de texte.

### Cas particulier : Ignorer des valeurs

Si vous aviez un tuple de 10 éléments mais que vous ne vouliez que le premier, vous pourriez utiliser le symbole `_` pour ignorer les autres, exactement comme avec les listes :
`decrireSeulementNom (nom, _, _, _, _, _, _, _, _, _) = nom`

---
