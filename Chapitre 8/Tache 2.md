HC8T2 : Types personnalisés et constructeurs de données
---
### Le Code Haskell

```haskell
-- 1. Définition du type personnalisé PaymentMethod
data PaymentMethod = Cash | Card | Cryptocurrency
    deriving (Show) -- Permet d'afficher la valeur dans la console

-- 2. Définition du type Person
-- L'adresse est un tuple (String, Int) représentant (Rue, Numéro)
data Person = Person {
    name          :: String,
    address       :: (String, Int),
    paymentMethod :: PaymentMethod
} deriving (Show)

-- 3. Création de l'instance "bob"
bob :: Person
bob = Person {
    name = "Bob",
    address = ("Rue de la Paix", 75),
    paymentMethod = Cash
}

main :: IO ()
main = do
    print bob

```

---

### Explication détaillée

#### 1. Le type `PaymentMethod`

C'est ce qu'on appelle un **type énuméré**.

* `Cash`, `Card` et `Cryptocurrency` sont des **constructeurs de données**.
* Ils représentent les seules valeurs possibles pour ce type.
* L'ajout de `deriving (Show)` est essentiel pour que Haskell sache comment transformer ces valeurs en texte si vous voulez les afficher avec `print`.

#### 2. Le type `Person` (Syntaxe d'enregistrement)

Ici, nous utilisons la **"Record Syntax"** (syntaxe d'enregistrement) :

* **Les champs nommés :** `name`, `address` et `paymentMethod` créent automatiquement des fonctions d'accès (des "getters"). Par exemple, taper `name bob` retournera `"Bob"`.
* **Le tuple :** L'adresse est définie comme `(String, Int)`. Les tuples sont parfaits pour regrouper un nombre fixe d'éléments de types différents qui forment une seule entité (ici, le nom de la rue et le numéro).

#### 3. L'instance `bob`

* Lors de la création de `bob`, nous spécifions les valeurs pour chaque champ.
* Comme demandé, sa méthode de paiement est `Cash`.
* Notez que l'adresse est entourée de parenthèses `("Rue de la Paix", 75)` car c'est la syntaxe standard des tuples en Haskell.

**Astuce :** Si vous aviez voulu que Bob paie par carte, vous auriez simplement écrit `paymentMethod = Card`. Grâce au système de types de Haskell, il est impossible d'assigner une valeur qui n'est pas prévue dans `PaymentMethod` à une `Person`.
