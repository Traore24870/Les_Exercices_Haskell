HC8T7 : Types de données et description d’animaux
---
### Le Code Haskell

```haskell
-- 1. Définition du type Animal
-- Dog et Cat attendent tous deux un argument de type String (le nom)
data Animal = Dog String | Cat String
    deriving (Show)

-- 2. Fonction de description utilisant le filtrage par motif (Pattern Matching)
describeAnimal :: Animal -> String
describeAnimal (Dog name) = "C'est un chien fidèle nommé " ++ name ++ "."
describeAnimal (Cat name) = "C'est un chat indépendant nommé " ++ name ++ "."

-- 3. Création des instances et test
main :: IO ()
main = do
    let monChien = Dog "Rex"
    let monChat  = Cat "Mistigri"
    
    putStrLn $ describeAnimal monChien
    putStrLn $ describeAnimal monChat

```

---

### Explication détaillée du code

#### 1. Les Constructeurs avec Paramètres

Contrairement aux exercices précédents où nous avions soit des constantes simples (`Cash`), soit des enregistrements nommés (`{name :: String}`), nous utilisons ici des **constructeurs de données positionnels** :

* `Dog String` signifie : "Pour créer un `Dog`, tu dois me donner une `String`".
* C'est une manière très légère et rapide de lier une donnée à un type précis sans s'encombrer de la syntaxe d'enregistrement.

#### 2. Le Filtrage par Motif (Pattern Matching)

Dans la fonction `describeAnimal`, nous "déballons" l'animal pour accéder à son nom :

* `(Dog name)` : Si l'animal est un chien, Haskell extrait la chaîne de caractères à l'intérieur et l'affecte à la variable locale `name`.
* On peut alors utiliser cette variable `name` pour construire notre phrase de retour.

#### 3. Flexibilité

L'avantage de cette approche est que vous pouvez traiter les chiens et les chats de manière uniforme (ils sont tous deux du type `Animal`), tout en conservant une logique spécifique à chaque espèce lors de l'exécution.

---

