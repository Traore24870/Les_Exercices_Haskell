HC9T9 : Vérifier la présence d’un élément dans une Sequence
---
---

### Code Source (Haskell)

```haskell
-- Rappel de la structure Sequence définie en HC9T8
data Sequence a 
    = End 
    | Node a (Sequence a) 
    deriving (Show)

-- 1. Définition de la fonction elemSeq
-- La contrainte Eq a est nécessaire pour utiliser l'opérateur de comparaison (==)
elemSeq :: Eq a => a -> Sequence a -> Bool
elemSeq _ End = False                      -- Cas de base 1 : fin de séquence, non trouvé
elemSeq target (Node x next)
    | target == x = True                   -- Cas de base 2 : trouvé dans le nœud actuel
    | otherwise   = elemSeq target next    -- Cas récursif : chercher dans la suite

-- 2. Fonction principale main()
main :: IO ()
main = do
    let mySeq = Node 10 (Node 20 (Node 30 End))
    
    putStrLn $ "Séquence : " ++ show mySeq
    
    -- Test 1 : Élément présent
    print $ "Est-ce que 20 est là ? " ++ show (elemSeq 20 mySeq)
    
    -- Test 2 : Élément absent
    print $ "Est-ce que 50 est là ? " ++ show (elemSeq 50 mySeq)
```

---

### Explication détaillée du code

#### La contrainte `Eq a`
C'est un point crucial. Puisque nous utilisons un type paramétrique `a`, Haskell ne sait pas par défaut si les éléments peuvent être comparés (certains types, comme les fonctions, ne sont pas comparables). En ajoutant `Eq a`, nous garantissons que le type `a` possède une implémentation de l'égalité `(==)`.

#### Le fonctionnement de la récursion
La fonction `elemSeq` traite trois scénarios possibles :

1.  **L'échec (`End`)** : Si la fonction atteint le constructeur `End`, cela signifie qu'elle a parcouru toute la chaîne sans trouver de correspondance. Elle renvoie donc `False`.
2.  **Le succès (`target == x`)** : Si la valeur stockée dans le nœud actuel (`x`) est égale à la cible (`target`), la recherche s'arrête immédiatement et renvoie `True`.
3.  **La poursuite (`otherwise`)** : Si ce n'est ni la fin, ni une correspondance, la fonction s'appelle elle-même avec le reste de la séquence (`next`).

#### Analyse de performance
Dans le pire des cas (si l'élément est à la fin ou absent), la fonction doit visiter chaque nœud. On dit que la complexité temporelle est de **$O(n)$**, où $n$ est le nombre d'éléments dans la séquence.

---
