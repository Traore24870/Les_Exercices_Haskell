
-- Déclaration de type (Type Signature) : 
-- La fonction prend un Int, puis un autre Int, et retourne un Int.
additionneNombres :: Int -> Int -> Int

-- Définition de la fonction :
-- Elle prend les arguments 'a' et 'b' et retourne leur somme.
additionneNombres a b = a + b

-- Fonction principale pour tester
main :: IO ()
main = do
    putStrLn "\n--- Tâche 6 : Signature de Type (Addition) ---"
    let resultat = additionneNombres 16 27
    let reponse =additionneNombres 56 74
    putStrLn ("Additionne 16 + 27 =")
    print (resultat)
    putStrLn ("Additione  de 56 + 74 =")
    print(reponse)
    

 Résumé de chaque Ligne de code

 
 additionneNombres :: Int -> Int -> Int Type : La fonction prend un Entier, puis un autre Entier, et retourne un Entier.
 
 additionneNombres a b = a + b Définition : Je prends a et b et je retourne leur somme.
 
 main2 :: IO () Type : Le programme de test pour cette fonction.
 
 let resultat = additionneNombres 15 27 Action : Je calcule 16 + 27 (ce qui donne 43) et stocke le résultat.
 
 putStrLn "Additionne 15 et 27 :" Affichage 1 : J'affiche un label.
 
 print resultat Affichage 2 : J'affiche le résultat du calcul (43).
