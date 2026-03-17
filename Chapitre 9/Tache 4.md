HC9T4 : Extraire une valeur d’une Box
---
---

### Code Source (Haskell)

```haskell
-- Définition du type Box
data Box a = Empty | Has a 
    deriving (Show)

-- 1. Définition de la fonction extract
-- Elle prend une valeur par défaut (d) et une Box (b)
extract :: a -> Box a -> a
extract d Empty   = d  -- Si la boîte est vide, on renvoie la valeur par défaut
extract d (Has x) = x  -- Si elle contient x, on renvoie directement x

-- 2. Fonction principale main()
main :: IO ()
main = do
    let defaultVal = 0
    
    let fullBox  = Has 42
    let emptyBox = Empty :: Box Int

    -- Test 1 : Extraction d'une boîte pleine
    let res1 = extract defaultVal fullBox
    putStrLn $ "Résultat boîte pleine : " ++ show res1

    -- Test 2 : Extraction d'une boîte vide
    let res2 = extract defaultVal emptyBox
    putStrLn $ "Résultat boîte vide   : " ++ show res2
    
    -- Exemple avec des chaînes de caractères
    let msg = extract "Inconnu" (Has "Alice")
    putStrLn $ "Nom de l'utilisateur  : " ++ msg
```

---

### Explication détaillée du code

#### La signature `a -> Box a -> a`
* **`a`** : Le premier argument est la valeur par défaut. Elle doit être du même type que ce que la boîte est censée contenir.
* **`Box a`** : Le deuxième argument est la boîte à inspecter.
* **`-> a`** : La fonction ne renvoie plus une `Box`, mais directement une valeur brute de type `a`.

#### Le mécanisme d'extraction
La fonction utilise le **pattern matching** pour décider quelle valeur fournir au programme :
1.  **Cas `Empty`** : Le programme "voit" que la boîte ne contient rien. Il ignore le contenu (inexistant) et renvoie immédiatement la valeur `d` fournie en premier argument.
2.  **Cas `Has x`** : Le programme "ouvre" la boîte, capture la valeur interne sous le nom `x` et la renvoie, ignorant totalement la valeur par défaut.

#### Pourquoi est-ce une bonne pratique ?
Cette fonction est le point final de la manipulation d'un type optionnel. Elle permet de :
* **Éviter les crashs** : Vous ne tentez jamais d'accéder à une mémoire vide.
* **Gérer les cas d'erreur proprement** : Vous définissez explicitement ce qui doit se passer si une donnée est manquante (ex: afficher "Utilisateur anonyme" si le nom est absent).

---

