HC9T1 : Définir un synonyme de type paramétrique
---
---

### Code Source (Haskell)

```haskell
-- 1. Définition du synonyme de type paramétrique
-- Ici, 'Entity a' est un alias pour un tuple contenant l'entité (a) et son adresse (String)
type Entity a = (a, String)

-- 2. Fonction pour afficher les informations
displayEntity :: Show a => Entity a -> IO ()
displayEntity (content, address) = do
    putStrLn $ "Contenu : " ++ show content
    putStrLn $ "Adresse : " ++ address
    putStrLn "---"

-- 3. Fonction principale main()
main :: IO ()
main = do
    -- Utilisation avec un type String (ex: un nom de magasin)
    let shop = ("Boulangerie Patachou", "12 rue de la Paix") :: Entity String
    
    -- Utilisation avec un type Integer (ex: un numéro d'identifiant)
    let user = (42, "Avenue des Champs-Élysées") :: Entity Int
    
    putStrLn "Affichage des entités :"
    displayEntity shop
    displayEntity user

```

---

### Explication du code

* **`type Entity a = (a, String)`** : C'est le cœur de votre demande. Le mot-clé `type` crée un synonyme. Le paramètre `a` est une **variable de type**. Cela signifie que `Entity` peut encapsuler n'importe quoi : un entier, une chaîne de caractères, ou même un objet complexe, tant qu'il est accompagné d'une `String` pour l'adresse.
* **La polyvalence** : Contrairement à un type fixe, `Entity a` est réutilisable. Dans le `main`, on voit que `shop` utilise `Entity String` alors que `user` utilise `Entity Int`.
* **Le tuple `(a, String)**` : Nous avons choisi d'utiliser un tuple pour l'implémentation la plus simple, liant directement la donnée à sa localisation géographique.
* **La fonction `displayEntity**` : Elle montre que le code peut traiter n'importe quelle `Entity a` de manière uniforme, à condition que le type `a` soit "affichable" (`Show a`).

---

### Pourquoi l'utiliser ?

L'intérêt principal est la **clarté du code**. Au lieu d'écrire partout des structures de données complexes, vous utilisez un nom qui a du sens métier (`Entity`), tout en gardant la flexibilité de changer ce qu'est une "entité" sans modifier toute la logique de votre application.

