HC9T10 : Type d’arbre binaire de recherche (BST)
---
---

### Code Source (Haskell)

```haskell
-- 1. Définition du type de données récursif BST
-- 'a' est le type paramétrique (Int, String, etc.)
data BST a 
    = Empty                   -- Représente un arbre vide ou une fin de branche
    | Node a (BST a) (BST a)  -- Un nœud contient : une valeur, le fils gauche, le fils droit
    deriving (Show, Eq)

-- 2. Fonction utilitaire pour créer une "feuille" (un nœud sans enfants)
leaf :: a -> BST a
leaf x = Node x Empty Empty

-- 3. Fonction principale main()
main :: IO ()
main = do
    -- Construction manuelle d'un arbre structuré pour la recherche :
    --        10
    --       /  \
    --      5   15
    let myTree = Node 10 
                    (leaf 5) 
                    (leaf 15)

    putStrLn "Représentation de l'arbre binaire (BST) :"
    print myTree
    
    -- Exemple d'un arbre avec des chaînes de caractères
    let alphaTree = Node "M" 
                        (leaf "A") 
                        (Node "S" Empty (leaf "Z"))
    
    putStrLn "\nArbre alphabétique :"
    print alphaTree
```

---

### Explication Logique (Approche Conceptuelle)

#### 1. La Structure à "Trois Compartiments"
Contrairement aux structures précédentes, le constructeur `Node` fonctionne comme un centre de tri. Il ne pointe pas vers une seule suite, mais possède **trois responsabilités** :
* **La Valeur (`a`)** : C'est la donnée stockée au niveau actuel (le pivot).
* **Le Sous-Arbre Gauche (`BST a`)** : Une branche complète qui, par convention de recherche, contiendra des éléments **plus petits** que la valeur actuelle.
* **Le Sous-Arbre Droit (`BST a`)** : Une branche complète qui contiendra des éléments **plus grands**.

#### 2. La Double Récursion
C'est la caractéristique la plus puissante du `BST`. Le type est défini par lui-même de deux côtés à la fois. Cela signifie que chaque "enfant" d'un nœud est lui-même un arbre entier. Cette structure permet de représenter des hiérarchies complexes où chaque embranchement est une nouvelle opportunité de diviser les données.

#### 3. Le Rôle du Constructeur `Empty`
Dans un arbre, `Empty` n'est pas seulement "rien". C'est le signal d'arrêt pour les algorithmes de parcours. Sans lui, l'arbre serait infini. Il représente les feuilles mortes de l'arbre : là où le chemin s'arrête parce qu'il n'y a plus de données à comparer.

#### 4. L'Efficacité de la Recherche
Imaginez que vous cherchez un nombre dans une séquence de 1 000 éléments. Dans le pire des cas, vous faites 1 000 vérifications. Avec le `BST`, grâce à sa structure séparée en "Gauche/Droite", vous éliminez la moitié des possibilités à chaque nœud. Vous trouvez votre cible en seulement **10 vérifications** environ ($log_2(1000)$). C'est la raison pour laquelle cette structure est utilisée pour les index de bases de données.

---
