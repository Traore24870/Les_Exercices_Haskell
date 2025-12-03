-- --------------------------------------------------------------------------
-- ⏫ Tâche 8 : Fonctions d'ordre supérieur (applyTwice)
-- --------------------------------------------------------------------------
applyTwice :: (a -> a) -> a -> a
applyTwice f x = f (f x)

-- Fonction utilitaire pour le test : Incrémenter de 1
increment :: Int -> Int
increment n = n + 1
-- --------------------------------------------------------------------------
-- ⚙ Fonction Main pour la Tâche 8
-- --------------------------------------------------------------------------
main :: IO ()
main = do
    putStrLn "\n--- ⏫ Tâche 8 : applyTwice ---"
    -- Test 1 : Application de l'incrémentation (increment) deux fois à 5
    let startInc = 5
        resultInc = applyTwice increment startInc
        -- 5 -> increment (5) = 6 -> increment (6) = 7
    putStrLn $ "Appliquer 'increment' deux fois à " ++ show startInc ++ " donne : " ++ show resultInc

    -- Test 2 : Application d'une fonction anonyme (* 10) deux fois à 2
    let startMul = 2
        resultMul = applyTwice (* 10) startMul
        -- 2 -> (* 10) = 20 -> (* 10) = 200
    putStrLn $ "Appliquer '(* 10)' deux fois à " ++ show startMul ++ " donne : " ++ show resultMul

    =======Explication des ligne code=========

 applyTwice :: (a -> a) -> a -> a Signature de Type Indique la structure de la fonction : elle prend une fonction (a -> a) (une fonction qui prend un type a et retourne le même type a), puis une valeur a, et retourne finalement une valeur a.
 
 applyTwice f x = f (f x) Définition Définit le calcul. f est la fonction et x est la valeur initiale. Le corps f (f x) signifie : appliquer f à x, puis appliquer f au résultat obtenu.

increment :: Int -> Int Fonction de Test Une simple fonction qui prend un entier (Int) et retourne cet entier plus un. Utilisée comme argument pour applyTwice.

 increment n = n + 1 Définition Met en œuvre l'opération d'ajout de 1.
 
 main :: IO () Fonction Principale Le point d'entrée du programme. IO () indique qu'elle effectue des actions d'entrée/sortie (affichage) et ne retourne pas de valeur significative.
 
 let startInc = 5 Test (Variable) Crée la variable locale startInc et lui assigne la valeur de départ 5 pour le premier test.
 
 resultInc = applyTwice increment startInc Test (Appel) Appelle applyTwice. L'opération est : increment appliqué deux fois à 5, ce qui donne 7.
 
 putStrLn $ "Appliquer 'increment'..." Affichage Affiche le résultat du Test 1. $ show resultInc convertit le nombre 7 en texte pour l'affichage.
 
 resultMul = applyTwice (* 10) startMul Test (Lambda) Utilise applyTwice avec une fonction anonyme ((* 10)), qui multiplie par 10. Le résultat de l'application double à 2 est 200.
 
 putStrLn $ "Appliquer '(* 10)'..." Affichage Affiche le résultat du Test 2.

 
    
