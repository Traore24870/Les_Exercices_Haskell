HC4T5 - Tâche 5 : Ajouter un cas générique avec un message personnalisé
---
### Le Code Haskell

```haskell
specialBirthday :: Int -> String
specialBirthday 1  = "Premier anniversaire !"
specialBirthday 18 = "Tu es adulte !"
specialBirthday 60 = "Enfin, je peux arrêter de m'inquiéter !"
specialBirthday age = "Rien de spécial, tu as juste " ++ show age ++ " ans."

main :: IO ()
main = do
    putStrLn (specialBirthday 18)
    putStrLn (specialBirthday 1)
    putStrLn (specialBirthday 15)
    putStrLn (specialBirthday 60)
    putStrLn (specialBirthday 80)

```

---

### Explications détaillées

1. **La Signature (`Int -> String`)** :
Cette ligne indique que la fonction `specialBirthday` prend un entier (`Int`) en entrée et renvoie une chaîne de caractères (`String`) en sortie.
2. **Le Pattern Matching (Filtrage par motif)** :
* Haskell lit les définitions de haut en bas.
* Si vous lui donnez `1`, `18` ou `60`, il s'arrête immédiatement sur la ligne correspondante et renvoie le texte associé.


3. **Le Cas "Par Défaut" (Ligne 5)** :
* La variable `age` à la ligne 5 est ce qu'on appelle un "catch-all". Si le nombre n'est ni 1, ni 18, ni 60, il tombe dans cette catégorie.
* `show age` : Comme `age` est un nombre, on doit utiliser la fonction `show` pour le transformer en texte afin de pouvoir l'assembler avec le reste de la phrase.
* L'opérateur `++` sert à coller (concaténer) les morceaux de texte ensemble.


4. **Le bloc `main**` :
C'est le point d'entrée du programme. Le mot-clé `do` permet d'enchaîner les actions (ici, l'affichage de plusieurs lignes dans la console via `putStrLn`).

---
