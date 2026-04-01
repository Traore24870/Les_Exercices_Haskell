HC11T2 : Fonction fancyFunction pour WeAccept
---
---

## 1. Code Source (`FancyFunction.hs`)

```haskell
-- 1. Définition du type WeAccept (Prédicat)
type WeAccept a = a -> Bool

-- 2. Définition des différents types de données
data Cardano = ADA { amount :: Double, staked :: Bool } deriving Show
data Cash    = Cash { currency :: String, value :: Int } deriving Show
data Country = Country { name :: String, population :: Int } deriving Show

-- 3. La fonction "fancyFunction"
-- Elle prend une liste d'éléments et un critère WeAccept,
-- et retourne la liste des éléments validés.
fancyFunction :: [a] -> WeAccept a -> [a]
fancyFunction list criterion = filter criterion list

-- 4. Main pour tester avec différents types
main :: IO ()
main = do
    -- --- Test avec Cardano ---
    let wallet = [ADA 100.5 True, ADA 50.0 False, ADA 2000.0 True]
    let isStaked = fancyFunction wallet staked
    putStrLn "Cardano (Staked only):"
    print isStaked

    -- --- Test avec Cash ---
    let pocket = [Cash "USD" 10, Cash "EUR" 50, Cash "USD" 100]
    let bigDollars = fancyFunction pocket (\c -> currency c == "USD" && value c > 20)
    putStrLn "\nCash (USD > 20):"
    print bigDollars

    -- --- Test avec Country ---
    let world = [Country "France" 67, Country "Monaco" 0, Country "India" 1400]
    let bigCountries = fancyFunction world (\ct -> population ct > 50)
    putStrLn "\nCountries (Pop > 50M):"
    print bigCountries
```

---

## 2. Explication Détaillée

### La signature de `fancyFunction`
La signature `[a] -> WeAccept a -> [a]` est la clé de la réutilisabilité :
* **`[a]`** : Une liste contenant des éléments de n'importe quel type `a`.
* **`WeAccept a`** : Une fonction qui prend un type `a` et renvoie un booléen.
* **Résultat `[a]`** : Une nouvelle liste de même type.

C'est ce qu'on appelle une **fonction générique** (ou polymorphe). Elle ne se soucie pas de savoir si elle manipule de l'argent ou des pays ; elle applique simplement la logique de filtrage.

### Les types de données
* **Cardano** : Représente une unité de crypto avec un montant et un état (staked ou non).
* **Cash** : Représente une monnaie classique.
* **Country** : Représente une nation. 

Chaque type possède des propriétés différentes, mais `fancyFunction` peut tous les traiter sans modification de son propre code.

### Flexibilité des critères (Lambdas)
Dans le `main()`, nous utilisons deux manières de passer le critère :
1.  **Référence directe** : Pour Cardano, on passe `staked`. Comme `staked` est une fonction générée par le record qui renvoie un `Bool`, elle correspond parfaitement à la signature `WeAccept Cardano`.
2.  **Expressions Lambda** : Pour `Cash` et `Country`, nous utilisons des fonctions anonymes `(\x -> ...)` pour définir des conditions complexes (ex: vérifier à la fois la devise et la valeur).

---

## 3. Pourquoi est-ce "Fancy" ?
Ce qui rend cette approche élégante, c'est le **découplage total**. En programmation impérative classique, vous auriez souvent besoin d'une interface commune ou d'une classe de base pour filtrer des types aussi disparates. En Haskell, tant que vous pouvez fournir une fonction qui retourne un `Bool`, `fancyFunction` fera son travail, respectant ainsi l'abstraction maximale.
