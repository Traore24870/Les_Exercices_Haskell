HC3T10 - Tâche avancée 10 : Vérifier si une chaîne est un palindrome (récursion, gardes)
---
### Code complet (Haskell)

```haskell
-- Définition de la fonction avec récursion et gardes
isPalindrome :: String -> Bool
isPalindrome s
    | length s <= 1 = True
    | head s == last s = isPalindrome (init (tail s))
    | otherwise = False

-- Fonction principale pour les tests
main :: IO ()
main = do
    putStrLn ("'racecar' est un palindrome ? " ++ show (isPalindrome "racecar"))
    putStrLn ("'haskell' est un palindrome ? " ++ show (isPalindrome "haskell"))
    putStrLn ("'madam'   est un palindrome ? " ++ show (isPalindrome "madam"))

```

---

### Explication du fonctionnement

La logique de cette fonction suit un processus de "réduction" de la chaîne de caractères :

1. **Cas de base (`length s <= 1`)** : Si la chaîne est vide ou n'a qu'une seule lettre, elle est techniquement un palindrome. On retourne `True`.
2. **Comparaison des extrémités (`head s == last s`)** :
* `head s` récupère le premier caractère.
* `last s` récupère le dernier caractère.
* Si ils sont identiques, on "épluche" la chaîne : `tail s` enlève le premier caractère et `init` enlève le dernier caractère. On appelle ensuite `isPalindrome` sur ce qui reste (le milieu).


3. **Cas d'échec (`otherwise`)** : Si le premier et le dernier caractère sont différents, ce n'est pas un palindrome, donc on retourne `False`.

---

### Analyse des tests demandés

| Chaîne | Processus récursif | Résultat final |
| --- | --- | --- |
| **"racecar"** | 'r'=='r' → "aceca" → 'a'=='a' → "cec" → 'c'=='c' → "e" → **True** | **True** |
| **"haskell"** | 'h' == 'l' ? **Non** | **False** |
| **"madam"** | 'm'=='m' → "ada" → 'a'=='a' → "d" → **True** | **True** |
---
