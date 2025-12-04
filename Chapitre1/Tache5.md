## ♾️ HC1T5 - Tâche 5 : Paresse en Haskell

```haskell
-- 1. Définition de la fonction 'infiniteNumbers'
-- Utilise la notation de la plage (range notation) pour générer une liste
-- commençant à 1 et s'étendant à l'infini (sans limite supérieure explicite).
infiniteNumbers :: [Integer]
infiniteNumbers = [1..]

-- 2. Fonction pour extraire les n premiers éléments
-- Elle prend un entier (n) et la liste infinie, et retourne les n premiers.
-- Remarque : 'take' est l'opération qui permet de ne calculer que ce qui est nécessaire.
getNFirstNumbers :: Int -> [a] -> [a]
getNFirstNumbers n liste = take n liste

-- Fonction combinée pour une démonstration directe
-- Prend n et retourne les n premiers nombres de la liste infinie
extractNFromInfinite :: Int -> [Integer]
extractNFromInfinite n = take n infiniteNumbers

-- Bloc principal pour tester les fonctions
main :: IO ()
main = do
    let n1 = 10
    let n2 = 5
    
    putStrLn "--- Listes Infinies et Évaluation Paresseuse ---"
    
    -- Test 1 : Extraction des 10 premiers nombres
    let premiersDix = extractNFromInfinite n1
    putStrLn $ "Les " ++ show n1 ++ " premiers nombres : " ++ show premiersDix
    -- Résultat : [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
    
    -- Test 2 : Extraction des 5 premiers nombres
    let premiersCinq = extractNFromInfinite n2
    putStrLn $ "Les " ++ show n2 ++ " premiers nombres : " ++ show premiersCinq
    -- Résultat : [1, 2, 3, 4, 5]
```

-----

## 💡 Explication Détaillée

### 1\. La Liste Infinie (`infiniteNumbers`)

```haskell
infiniteNumbers :: [Integer]
infiniteNumbers = [1..]
```

  * **`[1..]`** : C'est la syntaxe simple de Haskell pour une liste commençant à $1$ et dont l'étape par défaut est $1$ (c'est-à-dire $1, 2, 3, 4, \dots$) sans borne supérieure.
  * **Pureté** : La définition de cette liste est une simple déclaration. La liste elle-même n'est **jamais entièrement calculée** en mémoire.

### 2\. L'Évaluation Paresseuse (Lazy Evaluation)

C'est le concept clé ici. En Haskell, les listes infinies sont possibles grâce à l'**évaluation paresseuse** :

  * La liste `infiniteNumbers` est une simple *recette* pour générer des nombres.
  * Les nombres ne sont produits que **lorsqu'ils sont demandés**.
  * Si le programme n'a besoin que des 10 premiers éléments, seuls ces 10 éléments seront calculés. Le reste de la liste, bien que théoriquement infini, reste une promesse non réalisée.

### 3\. L'Extraction (`take`)

```haskell
getNFirstNumbers :: Int -> [a] -> [a]
getNFirstNumbers n liste = take n liste
```

  * La fonction standard **`take`** est essentielle pour travailler avec des structures de données paresseuses.
  * **`take n`** est l'opération qui "force" le calcul des $n$ premiers éléments de la liste fournie et ignore tout le reste.

### 4\. La Fonction Composée (`extractNFromInfinite`)

```haskell
extractNFromInfinite :: Int -> [Integer]
extractNFromInfinite n = take n infiniteNumbers
```

Cette fonction encapsule la logique : elle prend le nombre d'éléments à extraire (`n`) et applique `take n` directement à la liste infinie `infiniteNumbers`.

