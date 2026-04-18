HC11T6 : AdvancedEq pour Blockchain
---
### Le Code Source (Main.hs)

```haskell
-- Définition simplifiée d'une Blockchain
-- Une Blockchain est soit un bloc vide (Genesis), 
-- soit un bloc contenant une donnée (String) et un lien vers le reste de la chaîne.
data Blockchain = Genesis | Block String Blockchain deriving (Show, Eq)

-- Définition de la classe AdvancedEq qui étend Eq
-- Pour implémenter AdvancedEq, un type DOIT déjà implémenter Eq
class Eq a => AdvancedEq a where
    compareEquality :: a -> a -> String
    
-- Implémentation pour le type Blockchain
instance AdvancedEq Blockchain where
    compareEquality b1 b2
        | b1 == b2  = "Les blockchains sont strictement identiques (intégrité totale)."
        | otherwise = "Alerte : Les blockchains diffèrent (données ou structure modifiées)."

-- Fonction de test
main :: IO ()
main = do
    let chain1 = Block "Transaction 1" (Block "Transaction 2" Genesis)
    let chain2 = Block "Transaction 1" (Block "Transaction 2" Genesis)
    let chain3 = Block "Transaction 1" (Block "FRAUDE" Genesis)
    
    putStrLn "--- Test de AdvancedEq sur Blockchain ---"
    putStrLn $ "Comparaison 1 & 2 : " ++ compareEquality chain1 chain2
    putStrLn $ "Comparaison 1 & 3 : " ++ compareEquality chain1 chain3
```

---

### Explication détaillée du code

#### 1. L'Héritage de Classe (`Eq a => AdvancedEq a`)
C'est le point central de l'exercice. La syntaxe `Eq a =>` crée une **contrainte de classe**. 
* Cela signifie : "On ne peut pas être une instance de `AdvancedEq` si on n'est pas déjà capable de faire des comparaisons de base avec `Eq`."
* Cela permet à `compareEquality` d'utiliser l'opérateur `==` à l'intérieur de sa propre définition sans aucune erreur.

#### 2. Le type `Blockchain`
Nous utilisons ici un type récursif :
* `Genesis` : Le point de départ.
* `Block String Blockchain` : Chaque bloc contient une donnée et "pointe" vers le bloc précédent. 
* Comme nous avons ajouté `deriving (Eq)`, Haskell sait déjà comparer deux chaînes bloc par bloc de manière récursive.



#### 3. La méthode `compareEquality`
Au lieu de renvoyer un simple `True` ou `False`, cette méthode enrichit le comportement :
* Nous utilisons des **guards** (`|`) pour tester la condition.
* Si `b1 == b2`, nous renvoyons un message de validation.
* Sinon, nous renvoyons un message d'alerte.

C'est une façon élégante d'ajouter une couche de "sémantique" (du sens métier) par-dessus une simple opération technique de comparaison.

