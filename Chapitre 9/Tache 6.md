HC9T6 : Définir un type de données récursif
---
---

### Code Source (Haskell)

```haskell
-- 1. Définition du type de données récursif Tweet
data Tweet = Tweet 
    { content  :: String      -- Le texte du tweet
    , likes    :: Int         -- Le nombre de mentions "J'aime"
    , replies  :: [Tweet]     -- RÉCURSIVITÉ : Une liste de Tweets (commentaires)
    } deriving (Show)

-- 2. Fonction pour afficher un tweet et ses réponses avec indentation
displayTweet :: Int -> Tweet -> IO ()
displayTweet indent (Tweet msg lps rs) = do
    let space = replicate (indent * 4) ' '
    putStrLn $ space ++ "Tweet: \"" ++ msg ++ "\" (" ++ show lps ++ " likes)"
    -- Appel récursif pour chaque réponse
    mapM_ (displayTweet (indent + 1)) rs

-- 3. Fonction principale main()
main :: IO ()
main = do
    -- Création d'une structure imbriquée
    let subReply = Tweet "D'accord avec toi !" 2 []
    let reply1   = Tweet "Super thread, merci !" 10 [subReply]
    let reply2   = Tweet "Pas sûr pour le point n°2..." 1 []
    
    let mainTweet = Tweet "Le fonctionnel, c'est génial." 150 [reply1, reply2]

    putStrLn "--- Fil de discussion ---"
    displayTweet 0 mainTweet
```

---

### Explication détaillée du code

* **La Récursivité (`[Tweet]`)** : C'est le point clé. Le champ `replies` est une liste de type `Tweet`. Cela signifie qu'un tweet peut contenir une liste d'autres tweets, qui eux-mêmes peuvent contenir d'autres listes, et ainsi de suite à l'infini.
* **Le Cas de Base (Implicit)** : Pour qu'une structure récursive ne soit pas infinie, il faut un "cas d'arrêt". Ici, c'est la **liste vide `[]`**. Un tweet sans commentaires marque la fin d'une branche de la discussion.
* **La Fonction `displayTweet`** : Elle illustre comment on traite une structure récursive. On affiche le tweet actuel, puis on demande à la fonction de s'appeler elle-même pour chaque élément de la liste `replies`.
* **Modélisation en Arbre** : Ce type de structure transforme vos données en un **arbre**. Le `mainTweet` est la racine, et chaque commentaire est un nœud ou une feuille.

---

### Pourquoi utiliser la récursivité ici ?
Sans récursivité, vous seriez obligé de définir des types différents pour chaque niveau (ex: `Tweet`, `Commentaire`, `SousCommentaire`), ce qui limiterait la profondeur de la discussion. Avec ce type `Tweet`, votre application peut gérer des fils de discussion d'une profondeur illimitée avec une seule et même logique de code.
