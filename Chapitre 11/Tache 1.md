HC11T1 : Instance WeAccept pour Box
---
---

## 1. Code Source (`BoxFilter.hs`)

```haskell
-- 1. Définition du type de données Box
data Box = Box { 
    label  :: String, 
    weight :: Double 
} deriving (Show)

-- 2. Définition du type pour le critère d'acceptation
-- C'est l'équivalent fonctionnel de l'interface "WeAccept"
type WeAccept a = a -> Bool

-- 3. Fonction qui filtre et retourne la liste des boîtes acceptées
getAcceptedBoxes :: [Box] -> WeAccept Box -> [Box]
getAcceptedBoxes boxes criterion = filter criterion boxes

-- 4. Fonction principale (Main)
main :: IO ()
main = do
    -- Création d'une liste de boîtes (notre inventaire)
    let inventory = [ Box "Petite" 2.5
                    , Box "Lourde" 15.0
                    , Box "Moyenne" 7.2
                    , Box "Fragile" 1.0
                    ]

    -- Instance du critère : on accepte les boîtes dont le poids > 5.0
    -- En Haskell, une "instance" ici est simplement une fonction de type (Box -> Bool)
    let heavyCriterion :: WeAccept Box
        heavyCriterion b = weight b > 5.0

    -- Application du filtrage
    let result = getAcceptedBoxes inventory heavyCriterion

    -- Affichage des résultats
    putStrLn "--- Boîtes acceptées (> 5kg) ---"
    mapM_ print result
```

---

## 2. Explication Détaillée

### Le type de données `Box`
Nous utilisons la syntaxe **Record Syntax** (`data Box = Box { ... }`). Cela génère automatiquement des fonctions d'accès comme `weight :: Box -> Double`, ce qui rend le code très lisible lorsqu'on manipule les propriétés de la boîte.

### Le concept `WeAccept`
En Haskell, point besoin d'interfaces complexes pour ce cas de figure. Nous définissons un **alias de type** :
`type WeAccept a = a -> Bool`
Cela signifie que `WeAccept` est une fonction qui prend n'importe quel type `a` et renvoie un `Bool`. C'est l'essence même d'un filtre.

### La fonction `getAcceptedBoxes`
Cette fonction prend deux arguments :
1. Une liste de boîtes `[Box]`.
2. Une fonction de critère `WeAccept Box`.

Elle utilise la fonction prédéfinie `filter` de Haskell. La signature de `filter` est exactement ce dont nous avons besoin : elle prend un prédicat et une liste, puis renvoie une nouvelle liste contenant uniquement les éléments validant le prédicat.

### L'Instance et le `Main`
* **L'instance logique :** `heavyCriterion` est notre implémentation concrète de la règle. Notez la simplicité : on définit juste la condition mathématique.
* **`mapM_ print result` :** C'est la manière idiomatique en Haskell d'afficher chaque élément d'une liste sur une nouvelle ligne. `mapM_` applique la fonction `print` à chaque boîte du résultat dans le contexte de l'entrée/sortie (IO).

---

