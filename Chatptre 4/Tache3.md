HC4T3 - Tâche 3 : définir une fonction gradeComment
---

## Le Code avec `case` (Pattern Matching indirect)

```haskell
gradeComment :: Int -> String
gradeComment n = case (n >= 90 && n <= 100, n >= 70 && n <= 89, n >= 50 && n <= 69, n >= 0 && n <= 49) of
    (True, _, _, _) -> "Excellent !"
    (_, True, _, _) -> "Bon travail !"
    (_, _, True, _) -> "Tu as réussi."
    (_, _, _, True) -> "Peut-être mieux faire."
    _               -> "Note invalide."

main :: IO ()
main = do
    putStrLn (gradeComment 85)
    putStrLn (gradeComment 50)
    putStrLn (gradeComment 15)
    putStrLn (gradeComment 134)

```

---

1. **L'infinité des valeurs :** Le pattern matching est parfait quand on a une liste finie de cas (comme les jours de la semaine). Pour les nombres, il y a une infinité de possibilités entre 0 et 100 si on compte les décimaux (même si ici on utilise des `Int`).
2. **La syntaxe :** Écrire `gradeComment 90 = ...`, `gradeComment 91 = ...` jusqu'à 100 serait interminable.
3. **La sémantique :** Les "Guards" ont été inventés précisément pour pallier cette limite du pattern matching. Ils permettent de garder la clarté du filtrage tout en ajoutant de la logique mathématique.

### En résumé :

* **Pattern Matching :** Pour les structures de données et les valeurs fixes (`"Lundi"`, `True`, `Nothing`).
* **Guards :** Pour les comparaisons de grandeurs (`>`, `<`, `==`).
---
### Resulat attendue
* Bon travail !
* Tu as réussi.
* Peut-être mieux faire.
* Note invalide.
---
