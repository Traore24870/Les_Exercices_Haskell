HC4T4 - Tâche 4 : Réécrire spécialAnniversaire avec le pattern matching
---
Code
```haskell
-- Définition de la fonction avec correspondance de motifs (Pattern Matching)
specialBirthday :: Int -> String
specialBirthday 1  = "Premier anniversaire !"
specialBirthday 18 = "Tu es adulte !"
specialBirthday 60 = "Enfin, je peux arreter de m'interesser au nouveau jargon !"
specialBirthday _  = "Rien de special"

-- Fonction principale pour afficher les résultats
main :: IO ()
main = do
    putStrLn (specialBirthday 18)
    putStrLn (specialBirthday 1)
    putStrLn (specialBirthday 15)
    putStrLn (specialBirthday 60)
    putStrLn (specialBirthday 180)

``` 
---
## Explication du code

### 1. La définition des motifs (Patterns)

Ici, la fonction `specialBirthday` agit comme un trieur. Elle compare l'entier (`Int`) que vous lui donnez avec les valeurs inscrites à gauche du signe `=` :

* **Les cas spécifiques :** Le programme vérifie d'abord si le nombre est exactement `1`, `18` ou `60`.
* **L'ordre :** Comme pour vos exercices précédents, Haskell lit de haut en bas.
* **Le joker (`_`) :** Ce motif capture n'importe quel autre nombre (15, 180, 2, etc.). Sans cette ligne, votre programme planterait si vous lui donniez un âge non listé.

### 2. Le mécanisme interne

Le pattern matching sur les entiers est une comparaison d'égalité directe (, , etc.).

### 3. La fonction `main`

Elle exécute une série de tests en appelant la fonction avec différentes valeurs et affiche le résultat sur la console grâce à `putStrLn`.

---

## Résultat attendu (Output)

Lorsque vous lancerez ce programme, voici exactement ce qui s'affichera dans votre terminal :

```text
Tu es adulte !
Premier anniversaire !
Rien de special
Enfin, je peux arreter de m'interesser au nouveau jargon !
Rien de special

```

### Analyse de l'affichage :

1. **18** : Correspond au deuxième motif  "Tu es adulte !"
2. **1** : Correspond au premier motif  "Premier anniversaire !"
3. **15** : Ne correspond à aucun chiffre précis  tombe dans le `_` ("Rien de special")
4. **60** : Correspond au troisième motif  "Enfin, je peux arreter..."
5. **180** : Ne correspond à aucun chiffre précis  tombe dans le `_` ("Rien de special")

---
