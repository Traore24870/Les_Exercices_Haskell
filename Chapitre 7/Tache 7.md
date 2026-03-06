HC7T7 : Utiliser Bounded et Enum
---

### Le Code Source (Haskell)

```haskell
-- 1. Définition du type avec les dérivations automatiques nécessaires
-- Enum permet d'utiliser succ et pred
-- Bounded permet d'utiliser minBound et maxBound
data Color = Red | Green | Blue 
    deriving (Eq, Show, Enum, Bounded)

-- 2. Fonction nextColor
nextColor :: Color -> Color
nextColor c 
    | c == maxBound = minBound  -- Si c'est la dernière (Blue), on revient à la première (Red)
    | otherwise     = succ c    -- Sinon, on prend la suivante (successive)

-- 3. Fonction principale de test
main :: IO ()
main = do
    putStrLn "--- Test de la fonction nextColor ---"
    
    let c1 = Red
    let c2 = Green
    let c3 = Blue

    putStr "Après Red : "
    print (nextColor c1)  -- Devrait afficher Green
    
    putStr "Après Green : "
    print (nextColor c2)  -- Devrait afficher Blue
    
    putStr "Après Blue (Boucle) : "
    print (nextColor c3)  -- Devrait afficher Red

```

---

### Explication Détaillée

#### 1. La puissance de `deriving (Enum, Bounded)`

En ajoutant ces deux classes à notre `data Color`, Haskell génère automatiquement des fonctionnalités essentielles :

* **`Enum`** : Associe chaque constructeur à un entier (Red=0, Green=1, Blue=2). Cela nous donne accès à la fonction `succ` (successor), qui renvoie l'élément suivant.
* **`Bounded`** : Définit une borne inférieure (`minBound`) et une borne supérieure (`maxBound`). Pour notre type, `minBound` est `Red` et `maxBound` est `Blue`.

#### 2. La logique de `nextColor`

La fonction utilise des **guards** (`|`) pour gérer la logique circulaire :

1. **Cas limite :** On vérifie si la couleur actuelle `c` est égale à `maxBound`. Si oui, on "recommence la boucle" en renvoyant `minBound`.
2. **Cas général :** Pour toutes les autres couleurs (`otherwise`), on appelle simplement `succ c`.

#### 3. Pourquoi ne pas faire `succ Blue` ?

Si vous appelez `succ Blue` sans vérification préalable, Haskell déclenchera une erreur d'exécution (exception) car il n'y a rien après `Blue` dans l'énumération. L'utilisation de `Bounded` combinée à une garde permet de rendre votre code **robuste** et d'éviter les crashs.

---

### Résumé technique

| Classe | Fonction utilisée | Rôle |
| --- | --- | --- |
| **`Enum`** | `succ` | Récupérer l'élément suivant dans la liste. |
| **`Bounded`** | `maxBound` / `minBound` | Identifier dynamiquement la fin et le début du type. |
| **`Eq`** | `==` | Comparer la couleur actuelle à la borne maximale. |

