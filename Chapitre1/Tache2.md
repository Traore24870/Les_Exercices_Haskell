## 📐 Fonction Pure `circleArea`

```haskell
-- Pour utiliser la constante 'pi', nous devons importer le module Data.
import Data.Maybe

-- Définition de la fonction circleArea.
-- Elle prend un type a (qui doit être une instance de Floating pour la multiplication et pi)
-- et retourne un résultat du même type.
circleArea :: Floating a => a -> a
circleArea r = pi * r * r
-- Alternativement, on peut utiliser l'opérateur d'élévation à la puissance (**) :
-- circleArea r = pi * (r ** 2)

-- Bloc main pour tester la fonction
main :: IO ()
main = do
    let rayon1 = 5.0 :: Double
    let rayon2 = 12.5 :: Float
    
    putStrLn "--- Calcul de l'Aire d'un Cercle (Fonction Pure) ---"
    
    putStrLn $ "Rayon 5.0 (Double) | Aire = " ++ show (circleArea rayon1)
    putStrLn $ "Rayon 12.5 (Float) | Aire = " ++ show (circleArea rayon2)
```

-----

## 🔬 Explication de la Pureté

La fonction `circleArea` est un exemple classique de **fonction pure** en Haskell pour les raisons suivantes :

1.  **Absence d'Effets Secondaires (No Side Effects) :**

      * La fonction se contente de calculer et de retourner une valeur.
      * Elle **ne modifie pas** l'état du programme (par exemple, elle n'écrit pas dans un fichier, ne met pas à jour une base de données, et n'effectue aucune opération d'entrée/sortie comme `putStrLn`).

2.  **Dépendance Exclusive aux Entrées (Input Dependency) :**

      * Le résultat de `circleArea` dépend **uniquement** de son argument d'entrée, le rayon `r`.
      * **Aucune dépendance externe :** Elle n'accède à aucune variable globale, à aucune heure système, ni à aucune entrée utilisateur pour déterminer son résultat.
      * **Transparence Référentielle :** Si vous appelez `circleArea 5.0` dix fois, vous obtiendrez **toujours** le même résultat exact.

### Signature de Type : `Floating a => a -> a`

  * **`Floating a`** : Indique que le type `a` doit appartenir à la classe de types `Floating` (nombres à virgule flottante), car l'opération utilise la constante **$\pi$** et nécessite des multiplications de nombres non entiers.
  * **`a -> a`** : La fonction prend une valeur de type `a` (le rayon) et retourne une valeur du même type `a` (l'aire).

