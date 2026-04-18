HC11T8 : Dérivation de Eq et Ord pour PaymentMethod
---
### Le Code Source (Main.hs)

```haskell
-- Définition du type PaymentMethod
 import Data.List (sort) -- On importe sort pour tester l'ordre
-- L'ordre de déclaration définit la hiérarchie pour Ord
data PaymentMethod = Cash | Check | Card | Crypto
    deriving (Show, Eq, Ord)

-- Fonction de test pour explorer les comparaisons
main :: IO ()
main = do
    let myCash = Cash
    let myCard = Card
    let myCrypto = Crypto
    
    putStrLn "--- Test de Dérivation Eq et Ord ---"
    
    -- Test de l'égalité (Eq)
    putStrLn $ "Est-ce que Cash == Card ? " ++ show (myCash == myCard)
    putStrLn $ "Est-ce que Crypto == Crypto ? " ++ show (myCrypto == Crypto)
    
    -- Test de l'ordre (Ord)
    putStrLn "\n--- Classement (Ord) ---"
    putStrLn $ "Cash est-il 'plus petit' que Card ? " ++ show (myCash < myCard)
    putStrLn $ "Crypto est-il 'plus grand' que Check ? " ++ show (myCrypto > Check)
    
    -- Démonstration de l'ordre avec une liste
    let payments = [Crypto, Cash, Card, Check]
    putStrLn $ "\nListe originale : " ++ show payments
    putStrLn $ "Liste triée :     " ++ show (sort payments)
```

---

### Explication détaillée du code

#### 1. La dérivation automatique (`deriving`)
En ajoutant `deriving (Eq, Ord)`, vous demandez à Haskell d'écrire le code à votre place :
* **Pour `Eq`** : Deux valeurs sont égales si elles utilisent le même constructeur. `Cash == Cash` est vrai, `Cash == Card` est faux.
* **Pour `Ord`** : Haskell regarde l'ordre de haut en bas. Ici :
    1.  `Cash` est le plus petit.
    2.  Puis `Check`.
    3.  Puis `Card`.
    4.  `Crypto` est le plus grand.

#### 2. L'importance de l'ordre des constructeurs
Si vous aviez écrit `data PaymentMethod = Crypto | Cash ...`, alors `Crypto` serait devenu la valeur minimale. C'est très utile pour modéliser des priorités ou des niveaux de sécurité sans écrire de logique complexe.



#### 3. Utilisation pratique : le tri
L'un des plus grands avantages de dériver `Ord` est que votre type devient instantanément compatible avec toutes les fonctions de la bibliothèque standard qui nécessitent un ordre, comme `sort` (tri de liste), `min`, `max`, ou l'utilisation comme clé dans un `Data.Map`.

#### 4. Le type `Ordering`
Sous le capot, Haskell utilise toujours la fonction `compare` que nous avons vue précédemment. Par exemple, `compare Cash Crypto` retournera `LT` (Less Than) car `Cash` apparaît avant dans la définition.

---

