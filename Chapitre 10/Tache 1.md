HC10T1 : Classe de type ShowSimple
---
---

## Code Source Complet

```haskell
-- 1. Définition du type de données PaymentMethod
data PaymentMethod = CreditCard String | PayPal String | Cash

-- 2. Définition de la classe de type ShowSimple
-- Elle définit un contrat : tout type 'a' membre de cette classe 
-- doit implémenter la fonction showSimple.
class ShowSimple a where
    showSimple :: a -> String

-- 3. Implémentation de l'instance pour le type PaymentMethod
instance ShowSimple PaymentMethod where
    showSimple (CreditCard nb) = "Paiement par Carte : " ++ nb
    showSimple (PayPal email)  = "Paiement via PayPal : " ++ email
    showSimple Cash            = "Paiement en Espèces"

-- 4. Fonction principale pour tester l'implémentation
main :: IO ()
main = do
    let methode1 = CreditCard "4970-XXXX-XXXX-1234"
    let methode2 = PayPal "user@example.com"
    let methode3 = Cash
    
    putStrLn "--- Test de la classe ShowSimple ---"
    putStrLn (showSimple methode1)
    putStrLn (showSimple methode2)
    putStrLn (showSimple methode3)
```

---

## Explication Détaillée

### 1. Le Type Algébrique de Données (`data`)
Nous définissons `PaymentMethod` avec trois constructeurs de données. C'est un type **somme** :
* `CreditCard` et `PayPal` transportent une valeur de type `String` (le numéro ou l'email).
* `Cash` ne transporte aucune valeur supplémentaire.

### 2. La Classe de Type (`class`)
La déclaration `class ShowSimple a where` crée une nouvelle catégorie de types. 
* **`a`** est une variable de type. 
* La signature `showSimple :: a -> String` indique que pour "faire partie" de cette classe, un type doit fournir une fonction capable de se transformer en texte.
* C'est très similaire à une **Interface** en Java ou C#, mais appliqué au système de types de Haskell.

### 3. L'Instance (`instance`)
L'instance est la réalisation concrète du contrat pour un type spécifique.
* Nous utilisons le **pattern matching** pour définir un comportement différent selon le constructeur utilisé (`CreditCard`, `PayPal` ou `Cash`).
* L'opérateur `++` est utilisé pour la concaténation de chaînes de caractères.

### 4. Le programme principal (`main`)
Dans le `main`, nous créons trois variables de type `PaymentMethod`. 
* Lorsque nous appelons `showSimple`, le compilateur Haskell regarde le type de l'argument.
* Puisqu'il s'agit de `PaymentMethod`, il appelle l'implémentation spécifique que nous avons définie dans le bloc `instance`.

---

## Pourquoi créer sa propre classe au lieu d'utiliser `Show` ?

En Haskell, la classe standard `Show` est généralement réservée à la représentation interne du code (pour le débogage). Par exemple, `show (CreditCard "123")` produirait normalement la chaîne `"CreditCard \"123\""`. 

En créant `ShowSimple`, nous séparons :
1. **La représentation technique** (utile au développeur).
2. **La représentation métier** (utile à l'utilisateur final, avec un formatage personnalisé comme "Paiement par Carte...").
