HC4T1 - Tâche 1 : définir une fonction WeatherReport
---
Le code source

```haskell
-- Définition de la fonction avec la correction du cas par défaut
weatherReport :: String -> String
weatherReport "sunny"    = "Il fait beau et ensoleillé !"
weatherReport "pluvieux" = "N'oublie pas ton parapluie !"
weatherReport "nuageux"  = "Un peu gris, mais pas de pluie pour l'instant !"
weatherReport _          = "Météo inconnue" -- Utilisation du joker '_'

-- Fonction principale pour tester les différents cas
main :: IO ()
main = do
   putStrLn (weatherReport "sunny")
   putStrLn (weatherReport "nuageux")
   putStrLn (weatherReport "pluvieux")
   putStrLn (weatherReport "soleil") -- Retournera "Météo inconnue"

```

---

## Améliorations apportées

### 1. Le symbole Joker `_` (Wildcard)

Dans votre code, vous avez écrit `weatherReport matching`. Ici, `matching` est interprété par le langage comme une **variable**. Cela fonctionne, mais la convention en pattern matching est d'utiliser le tiret bas (`_`).

* Le `_` indique explicitement au compilateur : "Je reçois une valeur ici, mais je n'ai pas besoin de lui donner un nom car je ne vais pas la réutiliser, je veux juste renvoyer un message par défaut".

### 2. La Cohérence des entrées

Dans votre `main`, vous testez `"soleil"`, mais dans votre fonction, vous avez défini le cas `"sunny"`. Comme le pattern matching est **strict**, il ne fera pas le lien entre les deux. J'ai donc ajouté un test pour `"pluvieux"` afin que vous puissiez voir tous vos messages s'afficher.

---

## Explication du fonctionnement

Le pattern matching fonctionne comme un entonnoir avec plusieurs filtres successifs :

1. **Le test d'égalité :** Quand vous appelez `weatherReport "sunny"`, le programme compare la chaîne fournie avec la première ligne. S'il y a correspondance (match), il exécute la partie après le `=`.
2. **La descente :** Si la première ligne ne correspond pas, il passe à la deuxième, puis à la troisième.
3. **Le filet de sécurité :** La dernière ligne `_` est cruciale. Sans elle, si vous passiez une météo non définie (comme "neige"), le programme planterait avec une erreur de type "Non-exhaustive patterns" (motifs non exhaustifs). Le `_` garantit que la fonction a toujours une réponse, quoi qu'il arrive.

---
