HC8T8 : Synonymes de type et fonction de salutation
---
### Le Code Haskell

```haskell
-- 1. Définition des synonymes de type
type Name = String
type Age  = Int

-- 2. Fonction de salutation
greet :: Name -> Age -> String
greet name age = 
    "Bonjour " ++ name ++ " ! Tu as " ++ show age ++ " ans."

-- 3. Programme principal pour tester la fonction
main :: IO ()
main = do
    let monNom = "Alice"
    let monAge = 25
    
    -- Appel de la fonction et affichage du résultat
    putStrLn (greet monNom monAge)

```

---

### Explication détaillée

#### 1. Pourquoi utiliser `Name` et `Age` ?

Même si `Name` est techniquement une `String` et `Age` est un `Int`, la signature `greet :: Name -> Age -> String` est beaucoup plus parlante que `greet :: String -> Int -> String`.

* Elle évite les erreurs d'inversion d'arguments (bien que Haskell ne l'empêche pas techniquement ici, car ce sont des alias, cela aide grandement le développeur humain).
* C'est ce qu'on appelle de l'**auto-documentation**.

#### 2. La fonction `show`

Comme dans nos exercices précédents, n'oubliez pas que l'on ne peut pas concaténer directement un `Int` avec une `String`. La fonction `show` transforme la valeur numérique de l'âge en texte pour permettre l'assemblage de la phrase finale avec l'opérateur `++`.

#### 3. Fonctionnement interne

Il est crucial de se rappeler que `type` ne crée pas de "barrière". Vous pouvez tout à fait passer une `String` classique à une fonction qui attend un `Name`, car pour le compilateur, c'est exactement la même chose. C'est la différence majeure avec `newtype` ou `data`, qui créent de véritables types distincts et étanches.

---
