HC8T1 : Synonymes de type et fonction de base
---
```haskell
-- Définition des synonymes de type
type Address = String
type Value = Int

-- Définition de la fonction de génération de transaction
generateTx :: Address -> Address -> Value -> String
generateTx from to val = 
    "Transfert de " ++ show val ++ " de " ++ from ++ " vers " ++ to

-- Fonction principale pour tester le code
main :: IO ()
main = do
    let addrA = "0x123...abc"
    let addrB = "0x456...def"
    let montant = 500
    
    let result = generateTx addrA addrB montant
    putStrLn result

```

---

### Explication détaillée du code

#### 1. Les Synonymes de Type (`type`)

Les lignes `type Address = String` et `type Value = Int` ne créent pas de nouveaux types de données. Elles créent simplement des **alias**.

* **Pourquoi faire ?** Au lieu d'avoir une signature de fonction générique comme `String -> String -> Int -> String`, on utilise des noms qui ont du sens pour le domaine métier (la blockchain ou la finance ici).
* **Interchangeabilité :** Haskell traitera toujours une `Address` exactement comme une `String`. Vous pouvez utiliser n'importe quelle fonction de chaîne de caractères sur une `Address`.

#### 2. La Signature de la Fonction

`generateTx :: Address -> Address -> Value -> String`

* Cette ligne indique que la fonction prend trois arguments : deux de type `Address` et un de type `Value`.
* Elle retourne un résultat de type `String`.
* L'utilisation des alias rend l'ordre des arguments beaucoup plus clair pour le développeur.

#### 3. Le Corps de la Fonction

`generateTx from to val = ...`

* **Concaténation (`++`)** : En Haskell, on utilise l'opérateur `++` pour coller deux chaînes de caractères ensemble.
* **La fonction `show**` : C'est un point crucial. La variable `val` est de type `Int` (via l'alias `Value`). On ne peut pas concaténer directement un entier avec une chaîne. `show val` transforme l'entier `500` en chaîne `"500"`.

#### 4. Le bloc `main`

* `let` : Permet de définir des variables locales.
* `putStrLn` : La fonction standard pour afficher une chaîne de caractères dans la console suivie d'un retour à la ligne.

---
