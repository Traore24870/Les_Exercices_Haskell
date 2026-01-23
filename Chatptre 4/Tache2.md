HC4T2 - Tâche 2 : définir une fonction dayType
---

## Le Code (Haskell)

```haskell
dayType :: String -> String
-- On définit d'abord les cas spécifiques du week-end
dayType "Samedi"   = "C'est le week-end !"
dayType "Dimanche" = "C'est le week-end !"

-- On liste les jours de la semaine
dayType "Lundi"    = "C'est un jour de semaine."
dayType "Mardi"    = "C'est un jour de semaine."
dayType "Mercredi" = "C'est un jour de semaine."
dayType "Jeudi"    = "C'est un jour de semaine."
dayType "Vendredi" = "C'est un jour de semaine."

-- Le "catch-all" pour tout ce qui n'est pas un jour valide
dayType _          = "Jour invalide"

main :: IO ()
main = do
    putStrLn (dayType "Samedi")   -- Devrait afficher: C'est le week-end !
    putStrLn (dayType "Lundi")    -- Devrait afficher: C'est un jour de semaine.
    putStrLn (dayType "Octobre")  -- Devrait afficher: Jour invalide

```

---

## Explications techniques

### 1. La hiérarchie du Pattern Matching

Le secret ici est l'**ordre des définitions**. Le programme vérifie les motifs du haut vers le bas.

* **Priorité 1 (Week-end) :** On vérifie d'abord si c'est Samedi ou Dimanche.
* **Priorité 2 (Semaine) :** On vérifie ensuite les 5 jours de semaine. Si vous aviez simplement mis un joker `_` après Samedi et Dimanche, vous ne pourriez pas distinguer un "Lundi" d'un mot invalide comme "Bonjour".
* **Priorité 3 (Erreur) :** Le `_` à la toute fin sert de filet de sécurité pour capturer les fautes de frappe ou les entrées qui ne sont pas des jours.

### 2. Le défi de la redondance

Vous remarquerez que pour "Lundi" à "Vendredi", on répète la même phrase. En programmation fonctionnelle, on essaie souvent d'éviter cela.

**Astuce d'expert :** Une autre façon de l'écrire (plus avancée) serait d'utiliser des listes ou des gardes, mais pour votre exercice **HC4T2**, le pattern matching explicite ci-dessus est exactement ce qui est attendu pour démontrer que vous comprenez comment filtrer chaque cas.


Haskell est très strict :

* `"samedi"` (minuscule) ne correspondra pas à `"Samedi"` (majuscule).
* `"Mardi "` (avec un espace) ne correspondra pas non plus.
