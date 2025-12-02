
-- Fonction qui génère une liste infinie de nombres entiers,
-- en commençant implicitement à 1 (ou 0 si non spécifié, mais 1 est courant).
-- La liste [1..] est une syntaxe standard pour une séquence infinie.
infiniteNumbers :: [Int]
infiniteNumbers = [1..]

-- Fonction principale pour tester et extraire les 10 premiers nombres
main :: IO ()
main = do
    putStrLn "--- Tâche 5 : Paresse (Liste Infinie) ---"
    
    -- 'take' est Utilise pour  prendre que les N premiers éléments de la liste infinie.
    let n = 10
    let premiersNombres = take n infiniteNumbers
    
    putStrLn $ "Les " ++ show n ++ " premiers nombres de la liste infinie :"
    print premiersNombres


 Résumé Simple de chaque ligne decommande Ligne

 infiniteNumbers :: [Int] Type : infiniteNumbers est une liste d'entiers ([Int]).
 
 infiniteNumbers = [1..] Définition : C'est la liste infinie qui commence à 1.
 
 main :: IO () Type : Le programme principal effectuera une action (affichage).
 
 let n = 10 Variable : Je définis n (le nombre d'éléments à prendre) à 10.
 
 let premiersNombres = take n infiniteNumbers Action : Je prends (take) les 10 premiers éléments de la liste infinie.
 
 putStrLn $ "Les " ++ ... Affichage 1 : J'affiche une phrase pour expliquer le résultat.
 
 print premiersNombres Affichage 2 : J'affiche la liste : [1, 2, ..., 10].

