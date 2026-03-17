HC9T7 : Fonction pour calculer l’engagement
---
---

### Code Source (Haskell)

```haskell
-- Rappel de la structure définie en HC9T6
data Tweet = Tweet 
    { content  :: String
    , likes    :: Int
    , replies  :: [Tweet]
    } deriving (Show)

-- 1. Définition de la fonction d'engagement
-- Calcule : Likes du tweet actuel + Somme des engagements de ses réponses
engagement :: Tweet -> Int
engagement (Tweet _ lps rs) = lps + sum (map engagement rs)

-- 2. Fonction principale main()
main :: IO ()
main = do
    -- Construction d'un fil de discussion
    let subReply1 = Tweet "Totalement !" 5 []
    let subReply2 = Tweet "+1" 3 []
    
    let reply1    = Tweet "Super thread" 10 [subReply1, subReply2] -- Total: 10 + 5 + 3 = 18
    let reply2    = Tweet "Pas d'accord" 2 []                    -- Total: 2
    
    let mainTweet = Tweet "Le fonctionnel est puissant" 100 [reply1, reply2] 
    -- Total final : 100 (main) + 18 (reply1) + 2 (reply2) = 120

    putStrLn $ "Engagement du tweet principal : " ++ show (engagement mainTweet)
    putStrLn $ "Engagement de la première réponse : " ++ show (engagement reply1)
```

---

### Explication détaillée du mécanisme

#### 1. La Pensée Récursive
Le calcul de l'engagement suit une logique de "poupées russes". Pour connaître l'engagement d'un tweet, la fonction dit : *"Je prends mes propres likes, et je demande à chacun de mes commentaires de me donner leur propre score d'engagement"*.
* **Le cas de base** : Si la liste `replies` est vide, `map engagement rs` renvoie une liste vide. La fonction `sum` sur une liste vide donne `0`. Le résultat est donc juste les `likes` du tweet actuel.
* **Le cas récursif** : Si le tweet a des réponses, `engagement` s'appelle elle-même pour chaque réponse.

#### 2. Décomposition de la ligne `lps + sum (map engagement rs)`
C'est ici que la magie opère :
* **`map engagement rs`** : Applique la fonction `engagement` à chaque tweet contenu dans la liste des réponses (`rs`). Cela transforme une liste de tweets `[Tweet]` en une liste d'entiers `[Int]`.
* **`sum (...)`** : Additionne tous les entiers de cette nouvelle liste.
* **`lps + ...`** : Ajoute les likes du tweet d'origine au total obtenu par les commentaires.



#### 3. Pourquoi est-ce "élargi" et puissant ?
Cette approche est supérieure à une boucle classique (comme un `for` ou un `while`) pour plusieurs raisons :

* **Profondeur illimitée** : Que le fil de discussion ait 2 niveaux ou 200 niveaux de profondeur, le code reste strictement le même. La pile d'exécution du langage gère la descente dans l'arborescence pour vous.
* **Modularité** : La fonction est "pure". Elle ne dépend d'aucune variable globale. Elle ne fait que transformer une structure de données en un nombre.
* **Parcours d'arbre (Tree Traversal)** : En informatique, on appelle cela un parcours "Post-ordre". On calcule d'abord la valeur des feuilles (les derniers commentaires) pour remonter la valeur vers la racine (le tweet principal).

---
