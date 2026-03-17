HC9T8 : Définir un type récursif Sequence
---
---

### Code Source (Haskell)

```haskell
-- 1. Définition du type de données récursif Sequence
-- 'a' est le type paramétrique de la valeur stockée
data Sequence a 
    = End                   -- Cas de base : la séquence est terminée (vide)
    | Node a (Sequence a)   -- Cas récursif : une valeur et la suite de la séquence
    deriving (Show)

-- 2. Fonction pour transformer une liste standard en notre type Sequence
fromList :: [a] -> Sequence a
fromList []     = End
fromList (x:xs) = Node x (fromList xs)

-- 3. Fonction principale main()
main :: IO ()
main = do
    -- Création manuelle d'une séquence : 10 -> 20 -> End
    let manualSeq = Node 10 (Node 20 End)
    
    -- Création via une liste : "A" -> "B" -> "C" -> End
    let listSeq = fromList ["A", "B", "C"]
    
    putStrLn "Séquence manuelle (Entiers) :"
    print manualSeq
    
    putStrLn "\nSéquence générée (Strings) :"
    print listSeq
```

---

### Explication détaillée du code

#### 1. La structure récursive
Le type `Sequence a` possède deux constructeurs :
* **`End`** : C'est l'équivalent du pointeur `NULL` ou d'une liste vide. C'est indispensable pour arrêter la récursion, sinon la séquence serait infinie.
* **`Node a (Sequence a)`** : C'est le cœur du concept. Un nœud contient une valeur de type `a` et **un autre objet de type `Sequence a`**. C'est cette auto-référence qui crée le chaînage.



#### 2. Le paramètre de type `a`
L'utilisation de `a` rend votre séquence **générique**. Vous définissez la structure une seule fois, mais vous pouvez l'utiliser pour stocker des entiers (`Sequence Int`), des messages (`Sequence String`), ou même d'autres séquences.

#### 3. Analogie avec la mémoire
Imaginez une chasse au trésor :
* `Node` est une boîte contenant un objet et un indice vers la boîte suivante.
* `End` est une boîte vide indiquant que le trésor a été trouvé (fin de la piste).

#### 4. Avantages de cette structure
* **Immuabilité** : En programmation fonctionnelle, pour ajouter un élément au début, on crée simplement un nouveau `Node` qui pointe vers l'ancienne séquence. On ne modifie jamais les données existantes.
* **Flexibilité** : Contrairement à un tableau (array) de taille fixe, une `Sequence` peut s'agrandir indéfiniment tant qu'il y a de la mémoire disponible.

---
