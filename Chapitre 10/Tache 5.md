HC10T5 : Classe de type ShowDetailed
---
---

## Code Source (Haskell)

```haskell
-- 1. Définition du type de données User
-- Un utilisateur possède un ID (Int), un Nom (String) et un Rôle (String)
data User = User Int String String

-- 2. Définition de la classe de type ShowDetailed
class ShowDetailed a where
    showDetailed :: a -> String

-- 3. Implémentation de l'instance pour User
instance ShowDetailed User where
    showDetailed (User id name role) = 
        "=== FICHE UTILISATEUR ===\n" ++
        "ID    : " ++ show id ++ "\n" ++
        "Nom   : " ++ name ++ "\n" ++
        "Rôle  : " ++ role ++ "\n" ++
        "--------------------------"

-- 4. Fonction principale pour le test
main :: IO ()
main = do
    let admin = User 101 "Alice" "Administrateur"
    let guest = User 505 "Bob" "Invité"
    
    putStrLn "Affichage des détails :\n"
    putStrLn (showDetailed admin)
    putStrLn "" -- Saut de ligne
    putStrLn (showDetailed guest)
```

---

## Explication Détaillée

### 1. Le Type `User`
Nous utilisons un constructeur de produit `User` qui regroupe trois champs. Contrairement aux exercices précédents, nous avons ici un mélange de types (`Int` et `String`), ce qui rend l'affichage plus intéressant.

### 2. La Classe `ShowDetailed`
Cette classe suit la même logique que `ShowSimple` (HC10T1), mais son nom suggère une intention différente : fournir une représentation textuelle **verbeuse** ou **esthétique**, souvent destinée à un rapport ou une interface utilisateur en console.

### 3. L'Instance et la Gestion des Types
C'est dans l'implémentation de `showDetailed` que le travail de formatage a lieu :
* **Le saut de ligne (`\n`)** : Il permet de structurer l'affichage sur plusieurs lignes pour une meilleure lisibilité.
* **L'utilisation de `show id`** : Puisque le champ `id` est un `Int`, nous ne pouvons pas le concaténer directement avec des `String`. Nous devons utiliser la fonction standard `show` pour convertir l'entier en texte avant de l'assembler.
* **Concaténation** : Nous utilisons l'opérateur `++` pour construire la chaîne finale bloc par bloc.

### 4. Résultat dans la Console
Lorsque vous exécutez le `main`, le résultat est propre et structuré :
```text
=== FICHE UTILISATEUR ===
ID    : 101
Nom   : Alice
Rôle  : Administrateur
--------------------------
```

---

## Comparaison des Approches

| Classe | Usage Typique |
| :--- | :--- |
| `Show` (Standard) | Debugging (ex: `User 101 "Alice" "Admin"`) |
| `ShowSimple` | Identifiant court (ex: `Alice (ID: 101)`) |
| `ShowDetailed` | Rapport complet (multi-lignes avec étiquettes) |

Cette approche permet de respecter le principe de **responsabilité unique** : votre type `User` stocke les données, et chaque classe de type définit une manière spécifique de les transformer en fonction du contexte.
