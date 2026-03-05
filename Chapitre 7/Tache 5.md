HC7T5 : Fonction utilisant la contrainte Num
---
### Le Code Source (Haskell)

```haskell
-- 1. Fonction avec la contrainte Num
-- 'a' doit être une instance de la classe de type Num
squareArea :: Num a => a -> a
squareArea side = side * side

-- 2. Fonction principale pour tester avec différents types numériques
main :: IO ()
main = do
    putStrLn "--- Test de la fonction squareArea ---"

    -- Test avec un Int (Entier)
    let areaInt = squareArea (5 :: Int)
    putStr "Aire avec un côté entier (5) : "
    print areaInt

    -- Test avec un Double (Nombre à virgule)
    let areaDouble = squareArea (4.5 :: Double)
    putStr "Aire avec un côté flottant (4.5) : "
    print areaDouble

    -- Test direct (Haskell infère le type automatiquement)
    putStr "Aire avec une valeur directe (10) : "
    print (squareArea 10)

```

---

### Explication Détaillée

#### 1. La Signature `Num a => a -> a`

* **`a`** : C'est notre variable de type. Elle représente le type de la longueur du côté.
* **`Num a`** : C'est la **contrainte**. Elle indique au compilateur que le type `a` doit obligatoirement implémenter les opérations mathématiques de base (comme l'addition `+` ou la multiplication `*`).
* **`a -> a`** : La fonction prend un argument de type `a` et renvoie un résultat du même type `a`.

#### 2. Le Corps de la Fonction

La formule de l'aire d'un carré est $Côté \times Côté$ (ou $Côté^2$). En Haskell, l'opérateur `*` est défini à l'intérieur de la classe `Num`. Sans la contrainte `Num a`, Haskell refuserait de compiler car il ne pourrait pas garantir que l'opération `*` existe pour le type `a`.

#### 3. Polymorphisme Ad-hoc

Grâce à cette contrainte, votre fonction est **polymorphe**. Elle n'est pas limitée aux seuls nombres entiers. C'est ce qui permet d'utiliser `squareArea` aussi bien pour calculer l'aire d'un petit carreau (entier) que celle d'un terrain précis (nombre à virgule).

---
