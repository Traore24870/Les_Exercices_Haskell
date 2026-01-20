HC3T8 - Tâche avancée 8 : Calculer l'IMC et retourner la catégorie avec où
---
### Code complet (Haskell)

```haskell
-- Définition de la fonction avec gardes et clause 'where'
bmiCategory :: Float -> Float -> String
bmiCategory poids taille
    | bmi < 18.5  = "Insuffisance ponderale"
    | bmi < 25.0  = "Normal"
    | bmi < 30.0  = "Surpoids"
    | otherwise   = "Obesite"
    where bmi = poids / (taille^2)

-- Fonction principale pour tester les cas demandés
main :: IO ()
main = do
    putStrLn ("Test 70kg, 1.75m : " ++ bmiCategory 70 1.75)
    putStrLn ("Test 90kg, 1.80m : " ++ bmiCategory 90 1.8)

```

### Explication du fonctionnement

1. **La clause `where**` : C'est l'élément central de cet exercice. Elle permet de calculer la variable `bmi` une seule fois à la fin de la fonction. Cette variable devient alors disponible pour toutes les "gardes" situées au-dessus. Cela évite de réécrire `poids / taille^2` à chaque ligne de test.
2. **La logique des gardes** :
* Haskell teste les conditions de haut en bas.
* Si `bmi < 18.5` est faux, on passe à `bmi < 25.0`. Puisque l'on sait déjà que le score est supérieur à 18.5, cette garde couvre naturellement l'intervalle .


3. **Le type `Float**` : Contrairement aux exercices précédents utilisant `Int` (entiers), nous utilisons ici `Float` pour permettre les nombres à virgule (nécessaires pour la taille et le résultat de l'IMC).

### Résultats des tests

En exécutant le `main`, vous obtiendrez ces résultats :

* **70kg / 1.75m** : L'IMC est d'environ . Le programme affichera **"Normal"**.
* **90kg / 1.80m** : L'IMC est d'environ . Le programme affichera **"Surpoids"**.

