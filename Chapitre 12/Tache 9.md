HC12T9 : Lire et afficher le contenu d’un fichier
---
### Code Source (Main.hs)

```haskell
import System.IO
import System.Directory (doesFileExist)

-- Fonction pour lire et afficher le fichier
readFileContent :: FilePath -> IO ()
readFileContent path = do
    fileExists <- doesFileExist path
    if fileExists
        then do
            -- Lecture complète du fichier
            contenu <- readFile path
            putStrLn "--- Contenu du fichier ---"
            putStrLn contenu
            putStrLn "--------------------------"
        else do
            putStrLn $ "Erreur : Le fichier '" ++ path ++ "' est introuvable."

main :: IO ()
main = do
    putStrLn "Entrez le nom du fichier à lire (ex: test.txt) :"
    nomFichier <- getLine
    readFileContent nomFichier
```

---

### Explication détaillée

#### 1. Les imports
*   **`System.IO`** : Contient les fonctions de base pour les fichiers comme `readFile`.
*   **`System.Directory`** : Nous permet d'utiliser `doesFileExist`, ce qui est la manière la plus propre de vérifier la présence d'un fichier avant d'essayer de l'ouvrir.

#### 2. Le type `FilePath`
En Haskell, `FilePath` est simplement un alias (un synonyme) de `String`. Cela rend le code plus lisible en indiquant explicitement que la chaîne de caractères attendue représente un chemin vers un fichier.

#### 3. La fonction `readFile`
Cette fonction lit l'intégralité du fichier de manière **paresseuse** (*lazy*). Cela signifie que Haskell ne chargera en mémoire que les parties nécessaires au moment de l'affichage, ce qui est très efficace pour les gros fichiers.

#### 4. Gestion des erreurs
Plutôt que de laisser le programme "planter" avec une exception système illisible, nous utilisons une structure `if then else` basée sur le résultat de `doesFileExist` :
*   Si le fichier existe, on affiche son contenu.
*   Sinon, on affiche un message d'erreur personnalisé et amical.

---

### Comment tester ce programme ?

1.  **Créez un fichier de test** : Dans le même dossier que votre code, créez un fichier nommé `info.txt` et écrivez-y quelques phrases.
2.  **Lancez le programme** :
    ```bash
    runhaskell Main.hs
    ```
3.  **Testez les deux cas** :
    *   Entrez `info.txt` pour voir le texte s'afficher.
    *   Entrez `introuvable.txt` pour voir comment le programme gère l'erreur.
