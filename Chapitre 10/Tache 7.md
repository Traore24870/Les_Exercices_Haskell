HC10T7 : Classe de type Convertible
---
---

## Code Source (Haskell)

```haskell
{-# LANGUAGE MultiParamTypeClasses #-}

-- 1. Définition du type de données PaymentMethod
data PaymentMethod = CreditCard String | Cash

-- 2. Définition de la classe de type Convertible
-- 'a' est le type d'origine, 'b' est le type de destination
class Convertible a b where
    convert :: a -> b

-- 3. Implémentation de l'instance (Conversion de PaymentMethod vers String)
instance Convertible PaymentMethod String where
    convert (CreditCard nb) = "Carte : " ++ nb
    convert Cash            = "Espèces"

-- 4. Fonction principale pour tester
main :: IO ()
main = do
    let paiement = CreditCard "4970-XXXX"
    
    -- On précise le type de destination (String) pour aider le compilateur
    let resultat :: String
        resultat = convert paiement
    
    putStrLn "--- Test de la classe Convertible ---"
    putStrLn ("Résultat de la conversion : " ++ resultat)
```

---

## Explication Détaillée

### 1. L'extension `MultiParamTypeClasses`
Par défaut, Haskell s'attend à ce qu'une classe soit définie par rapport à un seul type (ex: `Eq a`). Ici, notre fonction `convert` doit transformer un type `a` en un type `b`. La ligne `{-# LANGUAGE MultiParamTypeClasses #-}` en haut du fichier est indispensable pour autoriser `class Convertible a b`.

### 2. La conception de la classe
* **`a`** : Le type d'entrée (la source).
* **`b`** : Le type de sortie (la cible).
* La fonction **`convert :: a -> b`** est extrêmement flexible. On pourrait imaginer des instances pour convertir un `Int` en `Float`, ou une `Blockchain` en `JSON`.

### 3. L'ambiguïté du type de retour
C'est le point technique le plus délicat. Si vous écrivez simplement `print (convert paiement)`, le compilateur risque de protester : 
> *"Vers quel type 'b' dois-je convertir mon PaymentMethod ?"*

C'est pourquoi, dans le `main`, nous avons explicitement annoté `resultat :: String`. Cela indique à Haskell d'aller chercher l'instance `Convertible PaymentMethod String`.

### 4. Application à `PaymentMethod`
Dans cette instance, nous transformons les constructeurs de notre type en une représentation textuelle simple. C'est une alternative plus générique à la classe `Show` que nous avons vue précédemment.

---

## Conclusion sur les Classes de Types (HC10)
À travers ces 7 exercices, vous avez exploré tout le spectre des classes de types en Haskell :
1.  **Affichage** (`ShowSimple`, `ShowDetailed`).
2.  **Réduction** (`Summable`).
3.  **Comparaison et Égalité** (`Comparable`, `Eq`, `Box`).
4.  **Transformation Générique** (`Convertible`).

Chaque classe permet de définir un **comportement** indépendamment de la structure des données, ce qui rend le code Haskell extrêmement modulaire et sûr.
