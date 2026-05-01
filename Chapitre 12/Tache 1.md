
HC12T1 : Afficher un message de bienvenue
---

### Code Source (Main.hs)

```haskell
-- Définition de la fonction principale
main :: IO ()
main = do
    putStrLn "Bienvenue dans la programmation Haskell !"
```

---

### Explication détaillée

Pour bien comprendre ce programme, il faut décomposer les trois éléments clés qui le constituent :

#### 1. La signature de type `main :: IO ()`
En Haskell, chaque fonction possède un type. 
*   **`main`** : C'est le point d'entrée standard de tout programme exécutable.
*   **`IO`** : Cela signifie "Input/Output" (Entrées/Sorties). Haskell est un langage purement fonctionnel, ce qui signifie que les fonctions ne sont pas censées avoir d'effets secondaires. Pour interagir avec le monde réel (afficher du texte, lire un fichier), on utilise le type `IO`.
*   **`()`** : On appelle cela "Unit". Cela indique que la fonction ne retourne aucune valeur utile après avoir terminé son action, un peu comme le `void` en C ou en Java.

#### 2. Le mot-clé `do`
Le bloc `do` est utilisé pour enchaîner plusieurs actions d'entrées/sorties de manière séquentielle. Bien qu'ici nous n'ayons qu'une seule ligne, l'utilisation du `do` est une excellente pratique dès que l'on manipule des actions `IO` dans le `main`.

#### 3. La fonction `putStrLn`
C'est la fonction standard pour l'affichage :
*   **`putStr`** : Signifie "put string" (afficher la chaîne).
*   **`Ln`** : Signifie "Line". Elle ajoute automatiquement un saut de ligne à la fin du message, de sorte que le curseur du terminal passe à la ligne suivante.

---

### Comment tester le programme ?

1.  **Avec GHCi (Interpréteur) :**
    Ouvrez votre terminal et tapez `ghci Main.hs`. Une fois chargé, tapez simplement `main` et appuyez sur Entrée.

2.  **En compilation directe :**
    Utilisez le compilateur GHC :
    ```bash
    ghc Main.hs -o bienvenue
    ./bienvenue
    ```

3.  **Avec RunHaskell :**
    Pour un test rapide sans créer de fichiers temporaires :
    ```bash
    runhaskell Main.hs
    ```
```
