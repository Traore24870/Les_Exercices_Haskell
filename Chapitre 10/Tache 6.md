HC10T6 : Récursivité mutuelle dans Eq pour Blockchain
---
---

## Code Source (Haskell)

```haskell
-- 1. Définition du type Blockchain
data Blockchain = Chain [String]

-- 2. Instance Eq avec récursivité mutuelle explicite
instance Eq Blockchain where
    -- Définition de l'égalité : on compare les listes internes
    (Chain b1) == (Chain b2) = not (b1 /= b2)
    
    -- Définition de l'inégalité : on utilise l'égalité pour conclure
    (Chain b1) /= (Chain b2) = not (b1 == b2)

-- 3. Fonction principale pour le test
main :: IO ()
main = do
    let bc1 = Chain ["Genesis", "Block 1"]
    let bc2 = Chain ["Genesis", "Block 1"]
    let bc3 = Chain ["Genesis"]

    putStrLn "--- Test de récursivité mutuelle (Eq Blockchain) ---"
    
    putStr "bc1 == bc2 ? "
    print (bc1 == bc2)  -- Devrait afficher True
    
    putStr "bc1 /= bc3 ? "
    print (bc1 /= bc3)  -- Devrait afficher True
```

---

## Explication Détaillée

### 1. Qu'est-ce que la récursivité mutuelle ?
La récursivité mutuelle survient lorsque deux fonctions sont définies l'une par rapport à l'autre. 
* Pour savoir si deux objets sont **égaux**, on demande s'ils ne sont **pas inégaux**.
* Pour savoir si deux objets sont **inégaux**, on demande s'ils ne sont **pas égaux**.



### 2. Le piège de la boucle infinie
Si vous écrivez exactement le code ci-dessus tel quel, Haskell entrera dans une **boucle infinie** (une récursion sans fin) car aucune des deux fonctions ne possède de "cas de base" concret. `==` appelle `/=`, qui appelle `==`, et ainsi de suite.

**Pour que cela fonctionne réellement**, au moins l'une des deux fonctions doit avoir une logique de comparaison réelle pour briser la chaîne. Voici la version correcte et fonctionnelle :

```haskell
instance Eq Blockchain where
    -- Cas concret : on compare réellement les contenus
    (Chain b1) == (Chain b2) = b1 == b2
    
    -- Récursivité mutuelle : /= s'appuie sur la définition de ==
    bcA /= bcB = not (bcA == bcB)
```

### 3. Pourquoi est-ce important ?
Dans la définition de la classe `Eq` en Haskell, les développeurs du langage ont écrit :
```haskell
class Eq a where
    (==) :: a -> a -> Bool
    x == y = not (x /= y) -- Définit == par rapport à /=

    (/=) :: a -> a -> Bool
    x /= y = not (x == y) -- Définit /= par rapport à ==
```
C'est ce qu'on appelle une **définition par défaut**. Cela permet au programmeur de n'implémenter qu'une seule des deux fonctions (généralement `==`), et l'autre est automatiquement déduite par le compilateur grâce à cette récursivité mutuelle pré-établie.

### 4. Application au type `Blockchain`
Dans notre instance pour `Blockchain` :
* Nous extrayons les listes de blocs `b1` et `b2`.
* Comme les listes (`[]`) et les chaînes de caractères (`String`) implémentent déjà `Eq` en Haskell, nous pouvons déléguer la comparaison réelle à l'opérateur `==` des listes.
