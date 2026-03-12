HC9T2 : Implémenter un type de données paramétrique
---
---

### Code Source (Haskell)

```haskell
-- 1. Définition du type de données paramétrique
-- 'a' est la variable de type (le contenu de la boîte)
data Box a = Empty | Has a 
    deriving (Show) -- Permet d'afficher le contenu dans la console

-- 2. Une fonction qui manipule la boîte de manière sécurisée
describeBox :: Show a => Box a -> String
describeBox Empty   = "La boite est vide."
describeBox (Has x) = "La boite contient : " ++ show x

-- 3. Fonction principale main()
main :: IO ()
main = do
    -- Création d'une boîte vide pour des entiers
    let myEmptyBox = Empty :: Box Int
    
    -- Création d'une boîte contenant une chaîne de caractères
    let myFullBox = Has "Un trésor"
    
    -- Affichage des résultats
    putStrLn $ "Test 1 : " ++ describeBox myEmptyBox
    putStrLn $ "Test 2 : " ++ describeBox myFullBox
    
    -- Exemple d'utilisation dans un calcul
    let smartBox = Has 100
    putStrLn $ "Valeur dans la boite : " ++ show smartBox

```

---

### Explication détaillée

#### 1. La déclaration `data Box a`

* **`data`** : Ce mot-clé indique que nous créons un nouveau type de données original, et non un simple alias.
* **`Box`** : C'est le nom de notre type (le "Constructeur de Type").
* **`a`** : C'est le paramètre de type. Il permet à la `Box` d'être générique. Elle peut devenir une `Box Int`, `Box String`, etc.

#### 2. Les Constructeurs de Données

Le type possède deux états possibles séparés par le symbole `|` (OU) :

* **`Empty`** : Un constructeur sans argument. Il représente l'absence de valeur.
* **`Has a`** : Un constructeur qui prend un argument de type `a`. C'est lui qui "emballe" la valeur.

#### 3. Le Pattern Matching (Filtrage de motif)

Dans la fonction `describeBox`, on utilise le pattern matching :

* Si le programme voit `Empty`, il exécute la première ligne.
* Si le programme voit `Has x`, il "déballe" la valeur `x` pour l'utiliser. C'est la manière la plus sûre de gérer des valeurs potentiellement nulles sans risquer d'erreur de type "NullPointerException".

#### 4. Le `deriving (Show)`

Haskell ne sait pas par défaut comment transformer un nouveau type en texte pour l'afficher. `deriving (Show)` demande au compilateur de générer automatiquement le code nécessaire pour que `print` ou `show` fonctionne sur notre `Box`.

---

### Pourquoi est-ce utile ?

Ce modèle est fondamental en programmation fonctionnelle pour **gérer l'optionnalité**. Au lieu de renvoyer une erreur ou un pointeur nul, une fonction renvoie une `Box`. Cela force le développeur à gérer explicitement le cas `Empty`, rendant le code extrêmement robuste.
