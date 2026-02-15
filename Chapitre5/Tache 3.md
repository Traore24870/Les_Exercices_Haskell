HC5T3 : Vérifier la présence de majuscules
---
### Code source (Haskell)

```haskell
import Data.Char (isUpper)

-- 1. Signature de la fonction
-- Prend une liste de chaînes de caractères (String) et renvoie un Booléen
contientMajuscule :: [String] -> Bool
contientMajuscule listeDeMots = any commenceParMajuscule listeDeMots
  where
    -- Fonction locale pour vérifier le premier caractère d'un mot
    commenceParMajuscule [] = False -- Cas d'un mot vide
    commenceParMajuscule (premierCarac:_) = isUpper premierCarac

-- 2. Fonction principale pour le test
main :: IO ()
main = do
    let mesMots = ["pomme", "Banane", "cerise"]
    
    let resultat = contientMajuscule mesMots
    
    putStrLn "La liste contient-elle un mot commençant par une majuscule ?"
    print resultat

```

---

### Explication détaillée

#### 1. L'importation `Data.Char (isUpper)`

Haskell ne devine pas tout seul ce qu'est une majuscule. On importe donc `isUpper`, une fonction prédéfinie qui renvoie `True` si un caractère est une majuscule (A-Z) et `False` sinon.

#### 2. La fonction `any`

C'est le cœur de l'exercice. Sa signature est :

`any :: (a -> Bool) -> [a] -> Bool`

* **Son rôle** : Elle parcourt la liste et applique un test à chaque élément.
* **Son comportement** : Dès qu'elle trouve **un seul** élément qui répond `True`, elle s'arrête et renvoie `True`. Si elle arrive à la fin de la liste sans rien trouver, elle renvoie `False`.

#### 3. La fonction auxiliaire `commenceParMajuscule`

Comme nous avons une liste de *mots* (donc une liste de listes de caractères), nous devons dire à `any` comment tester chaque mot :

* `(premierCarac:_)` : C'est du **pattern matching**. On sépare le premier caractère du reste du mot.
* `isUpper premierCarac` : On vérifie uniquement ce premier caractère.

#### 4. Le fonctionnement dans le `main`

Dans l'exemple `["pomme", "Banane", "cerise"]` :

1. `any` teste "pomme" : commence par 'p' (minuscule) -> `False`.
2. `any` teste "Banane" : commence par 'B' (Majuscule) -> `True`.
3. **STOP** : `any` a trouvé un résultat positif, elle renvoie immédiatement `True` sans même regarder "cerise".

---
