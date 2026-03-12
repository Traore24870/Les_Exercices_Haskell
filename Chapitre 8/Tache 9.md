HC8T9 : Type enregistrement Transaction et fonction associée
---
### Le Code Haskell

```haskell
-- Rappel des synonymes de type nécessaires
type Address = String
type Value   = Int

-- 1. Définition du type Transaction en syntaxe d'enregistrement
data Transaction = Transaction {
    from          :: Address,
    to            :: Address,
    amount        :: Value,
    transactionId :: String
} deriving (Show)

-- 2. Fonction pour créer une transaction et retourner son ID
createTransaction :: Address -> Address -> Value -> String
createTransaction sender receiver val =
    let 
        -- Génération d'un ID fictif basé sur les adresses
        newId = "TX-" ++ sender ++ "-" ++ show val
        -- Création de l'enregistrement
        tx = Transaction { 
                from = sender, 
                to = receiver, 
                amount = val, 
                transactionId = newId 
             }
    in transactionId tx -- On retourne uniquement le champ ID

-- 3. Exemple d'exécution
main :: IO ()
main = do
    let idResult = createTransaction "Alice" "Bob" 100
    putStrLn $ "ID de la transaction générée : " ++ idResult

```

---

### Explication détaillée du code

#### 1. La structure `Transaction`

L'utilisation de la syntaxe d'enregistrement (`{ ... }`) ici est particulièrement utile car une transaction contient plusieurs champs du même type (`Address` et `String` pour l'ID). Sans les noms de champs, il serait très facile de se tromper d'ordre lors de la manipulation des données.

#### 2. La fonction `createTransaction`

* **Logique interne** : La fonction prend trois arguments (expéditeur, destinataire, montant).
* **Le bloc `let...in**` : C'est une structure locale qui permet de définir des variables intermédiaires.
* Nous créons d'abord `newId`.
* Nous créons ensuite l'objet `tx` de type `Transaction`.


* **Retour de valeur** : La dernière ligne `transactionId tx` utilise le "getter" automatique généré par Haskell pour extraire l'identifiant de l'objet que nous venons de créer et le renvoyer.

#### 3. Pourquoi passer par un objet intermédiaire ?

Bien que nous ne renvoyions que le `String` de l'ID, créer l'objet `Transaction` complet à l'intérieur de la fonction garantit que les données sont valides et conformes à notre modèle de données métier avant de confirmer l'opération.

