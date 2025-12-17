HC2T5 - Tâche 5 : Définir et utiliser des fonctions
---

```haskell
-- Fichier : Geometry.hs

-- Définition 1 : Fonction pour calculer l'aire d'un cercle (A = πr²)
-- Signature de type : prend un Float (rayon) et retourne un Float (aire)
circleArea :: Float -> Float
circleArea radius = pi * radius * radius

-- Définition 2 : Fonction pour trouver le maximum de trois entiers
-- Signature de type : prend trois Int et retourne un Int
maxOfThree :: Int -> Int -> Int -> Int
-- Utilise la fonction prédéfinie 'max' pour la composition
maxOfThree a b c = max a (max b c)

-- Fonction principale pour les tests et l'exécution
main :: IO ()
main = do
    putStrLn "--- Test des Fonctions Pures ---"

    -- 🧪 Tests de circleArea
    putStrLn "\n[1] Test de circleArea (Aire du Cercle) :"
    putStr "Aire pour le rayon 1.0 (Attendu: 3.141...) : "
    print (circleArea 1.0)
    
    putStr "Aire pour le rayon 5.0 (Attendu: 78.539...) : "
    print (circleArea 5.0)

    -- 🧪 Tests de maxOfThree
    putStrLn "\n[2] Test de maxOfThree (Maximum de Trois Nombres) :"
    putStr "Max de (5, 12, 8) (Attendu: 12) : "
    print (maxOfThree 5 12 8)
    
    putStr "Max de (20, 10, 3) (Attendu: 20) : "
    print (maxOfThree 20 10 3)
    
    putStr "Max de (-5, -2, -8) (Attendu: -2) : "
    print (maxOfThree (-5) (-2) (-8))

```

##2. Explication Détaillée du Code
---

A. Fonction `circleArea`Cette fonction met en œuvre la formule géométrique pour l'aire d'un cercle, A = \pi r^2.

| Élément | Code | Explication |
| --- | --- | --- |
| **Signature** | `circleArea :: Float -> Float` | La fonction prend un argument de type `Float` (le rayon) et retourne un `Float` (l'aire). La flèche (`->`) est le séparateur d'arguments en Haskell (curryfication). |
| **Implémentation** | `pi * radius * radius` | Utilise la constante `pi`, disponible par défaut dans le `Prelude` pour les types flottants, et l'opérateur de multiplication infixe `*`. |
| **Pureté** | N/A | Le résultat est garanti pour un rayon donné, sans dépendre du temps, d'une variable globale ou de l'état du système. |

B. Fonction `maxOfThree`Cette fonction utilise la **composition** pour trouver le plus grand de trois nombres en réutilisant la fonction `max` existante.

| Élément | Code | Explication |
| --- | --- | --- |
| **Signature** | `maxOfThree :: Int -> Int -> Int -> Int` | Elle prend trois arguments `Int` et retourne le `Int` le plus grand. |
| **Implémentation** | `max a (max b c)` | C'est un excellent exemple de composition : on calcule d'abord `max b c`, puis on passe ce résultat comme deuxième argument à `max a`. Cela permet d'éviter l'utilisation de `if/else` complexes. |
| **Curryfication** | `a b c` | La fonction n'est pas appelée avec une virgule (ex: `(a, b, c)`), mais prend les arguments séquentiellement. Ceci permet une application partielle (concept non utilisé ici, mais fondamental en Haskell). |

---

