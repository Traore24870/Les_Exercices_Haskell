HC11T5 : Fonction guessWhat'sInside pour Containe
---

### Le Code Source (Main.hs)

```haskell
-- Rappel de la classe Container
class Container f where
    isEmpty  :: f a -> Bool
    contains :: Eq a => a -> f a -> Bool
    replace  :: f a -> b -> f b

-- Définition des types Box et Present
data Box a = Box a deriving (Show)
data Present a = Wrapped a | Empty deriving (Show)

-- Instances (simplifiées pour l'exemple)
instance Container Box where
    isEmpty _ = False
    contains x (Box val) = x == val
    replace _ newVal = Box newVal

instance Container Present where
    isEmpty Empty = True
    isEmpty _     = False
    contains x (Wrapped val) = x == val
    contains _ Empty = False
    replace _ newVal = Wrapped newVal

-- LA FONCTION DEMANDÉE : guessWhat'sInside
-- Cette fonction accepte n'importe quel conteneur 'c' 
-- à condition que 'c' soit une instance de la classe Container.
guessWhat'sInside :: (Container c, Eq a) => a -> c a -> String
guessWhat'sInside guess container =
    if contains guess container
        then "Bravo ! Vous avez trouvé le contenu."
        else "Dommage... Ce n'est pas ce qui se trouve à l'intérieur."

-- Test de la fonction
main :: IO ()
main = do
    let maBoite = Box 10
    let monCadeau = Wrapped "Vélo"
    
    putStrLn $ "Test Boîte : " ++ guessWhat'sInside 10 maBoite
    putStrLn $ "Test Cadeau : " ++ guessWhat'sInside "Trottinette" monCadeau
```

---

### Explication détaillée

#### 1. La Signature (Le "Contrat")
La signature de la fonction est la partie la plus importante :
`guessWhat'sInside :: (Container c, Eq a) => a -> c a -> String`

* **(Container c) =>** : Cela signifie que la fonction ne peut être utilisée qu'avec des types qui implémentent l'interface `Container` (comme `Box` ou `Present`).
* **(Eq a) =>** : Puisque nous allons comparer l'élément `guess` avec le contenu du conteneur, le type de cet élément doit pouvoir être comparé (il doit implémenter `Eq`).
* **c a** : Représente le conteneur `c` contenant une valeur de type `a`.

#### 2. L'Abstraction
L'un des grands avantages ici est que `guessWhat'sInside` **ne sait pas** comment `contains` est implémenté. Elle se contente d'appeler la méthode. 
* Si vous lui passez une `Box`, elle utilisera la logique de `contains` pour `Box`.
* Si vous lui passez un `Present`, elle utilisera la logique de `contains` pour `Present`.

C'est ce qu'on appelle le **polymorphisme ad-hoc**.

#### 3. Fonctionnement logique
La fonction prend deux arguments :
1.  `guess` : La valeur que l'utilisateur essaie de deviner.
2.  `container` : La structure de données qui contient (peut-être) quelque chose.

Elle utilise ensuite une structure `if ... then ... else` basée sur le résultat booléen renvoyé par `contains`.

---

### Pourquoi est-ce utile ?
Imaginez que vous créiez plus tard un nouveau type `Backpack` (Sac à dos). Si vous déclarez `Backpack` comme une instance de `Container`, la fonction `guessWhat'sInside` fonctionnera **automatiquement** avec vos sacs à dos sans que vous ayez besoin de modifier une seule ligne de son code.

