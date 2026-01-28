HC4T6 - Tâche 6 : Identifier le contenu d'une liste par pattern matching
---
### Le Code Haskell

```haskell
whatsInsideThisList :: [a] -> String
whatsInsideThisList []           = "La liste est vide."
whatsInsideThisList [x]          = "La liste contient un seul element."
whatsInsideThisList [x, y]       = "La liste contient exactement deux elements."
whatsInsideThisList (x:y:z:rest) = "La liste est longue, elle contient au moins trois elements."

main :: IO ()
main = do
    putStrLn (whatsInsideThisList [])
    putStrLn (whatsInsideThisList [42])
    putStrLn (whatsInsideThisList ["Haskell", "Ocaml"])
    putStrLn (whatsInsideThisList [1, 2, 3, 4, 5])

```

### Explications des motifs (patterns) :

1. **`[]`** : Correspond à une liste **vide**.
2. **`[x]`** : Correspond à une liste contenant **exactement un élément**. (C'est un raccourci pour `x:[]`).
3. **`[x, y]`** : Correspond à une liste contenant **exactement deux éléments**. (Raccourci pour `x:y:[]`).
4. **`(x:y:z:rest)`** :
* `x` est le 1er élément.
* `y` est le 2ème.
* `z` est le 3ème.
* `rest` est le reste de la liste (qui peut être vide ou contenir encore d'autres éléments).
* Ce motif capture donc tout ce qui a **3 éléments ou plus**.


