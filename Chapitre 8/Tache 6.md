HC8T6 : Syntaxe d’enregistrement pour variantes Shape
---
### Le Code Haskell

```haskell
-- 1. Définition du type Shape avec variantes et syntaxe d'enregistrement
data Shape 
    = Circle { 
        center :: (Float, Float), 
        color  :: String, 
        radius :: Float 
      }
    | Rectangle { 
        center :: (Float, Float), -- On peut aussi donner un centre au rectangle
        width  :: Float, 
        height :: Float, 
        color  :: String 
      }
    deriving (Show)

-- 2. Création d'une instance de Cercle
monCercle :: Shape
monCercle = Circle { 
    center = (0.0, 0.0), 
    color = "Rouge", 
    radius = 15.5 
}

-- 3. Création d'une instance de Rectangle
monRectangle :: Shape
monRectangle = Rectangle { 
    center = (10.0, 5.0), 
    width = 100.0, 
    height = 50.0, 
    color = "Bleu" 
}

main :: IO ()
main = do
    print monCercle
    print monRectangle

```

---

### Explication détaillée

#### 1. Structure Multi-Constructeurs

Le type `Shape` utilise ici ce qu'on appelle des **Sommes de Records**.

* Si vous créez un `Circle`, Haskell s'attend aux champs `center`, `color` et `radius`.
* Si vous créez un `Rectangle`, il s'attend à `center`, `width`, `height` et `color`.

#### 2. Champs Partagés

Remarquez que `color` et `center` apparaissent dans les deux constructeurs. C'est tout à fait autorisé ! Cela permet d'utiliser la fonction d'accès `color` sur n'importe quelle `Shape`, qu'il s'agisse d'un cercle ou d'un rectangle :

```haskell
-- Cette fonction fonctionne pour les deux variantes
getColor :: Shape -> String
getColor s = color s

```

#### 3. Le Tuple pour le Centre

Le champ `center :: (Float, Float)` utilise un **tuple**. C'est la manière la plus concise en Haskell de représenter des coordonnées $(x, y)$ sans avoir à créer un type dédié.

#### 4. Sécurité des Types

Si vous essayez d'accéder au champ `radius` sur `monRectangle`, Haskell lancera une erreur à l'exécution (ou un avertissement à la compilation selon les options). C'est pourquoi, avec ce genre de structure, on utilise souvent le **Pattern Matching** pour être sûr de ne manipuler que les champs existants pour la variante donnée.

---
