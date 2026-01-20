HC3T7 - Tâche avancée 7 : Déterminer la saison en fonction du mois avec des gardes
---

### Code complet (Haskell)

```haskell
-- Définition de la fonction avec des gardes (guards)
saison :: Int -> String
saison mois
    | mois == 12 || mois == 1 || mois == 2 = "Hiver"
    | mois >= 3  && mois <= 5              = "Printemps"
    | mois >= 6  && mois <= 8              = "Ete"
    | mois >= 9  && mois <= 11             = "Automne"
    | otherwise                            = "Mois invalide"

-- Fonction principale pour exécuter les tests demandés
main :: IO ()
main = do
    putStrLn ("saison 3  : " ++ saison 3)
    putStrLn ("saison 7  : " ++ saison 7)
    putStrLn ("saison 11 : " ++ saison 11)

```

### Explication du fonctionnement du code

1. **Les Gardes (`|`)** : Au lieu d'utiliser des blocs `if-then-else` imbriqués, on utilise des "gardes". Chaque barre verticale `|` introduit une condition. Si la condition est vraie, Haskell exécute ce qui se trouve après le signe `=`.
2. **Opérateurs Logiques** :
* `||` (OU) : Utilisé pour l'hiver car les mois ne sont pas consécutifs dans l'ordre croissant (12, 1, 2).
* `&&` (ET) : Utilisé pour les autres saisons pour vérifier si le mois appartient à un intervalle (par exemple, entre 3 et 5 inclus pour le printemps).


3. **`otherwise`** : C'est une garde spéciale qui est toujours vraie. Elle sert de cas par défaut (comme le `else` final) si aucune des conditions précédentes n'est remplie.
4. **La fonction `main**` :
* Elle utilise `putStrLn` pour afficher les résultats.
* L'opérateur `++` permet de coller la description de l'exercice avec le résultat renvoyé par la fonction `saison`.



### Résultats des tests

En exécutant ce code, vous obtiendrez :

* `saison 3`  → **"Printemps"**
* `saison 7`  → **"Ete"**
* `saison 11` → **"Automne"**
