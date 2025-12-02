--Verifion si un nombre est superieuw a 18

greaterThan18 :: Int -> Bool
greaterThan18 k = k > 18

main :: IO()
main=do
 print(greaterThan18 5)
 print(greaterThan18 27)
 print(greaterThan18 18)
 print(greaterThan18 2)

 Code Explication Détaillée

 
 greaterThan18 :: Int -> Bool Déclaration de type : La fonction greaterThan18 prend un entier (Int) en entrée et retourne un booléen (Bool) en sortie. Un booléen est une valeur qui ne peut être que True (Vrai) ou False (Faux).
 
 greaterThan18 k = k > 18 Définition : Elle prend un argument k et retourne le résultat de la comparaison k > 18.Si k est plus grand que 18, la fonction retourne True.Sinon (si k est 18 ou moins), elle retourne False.

 main :: IO() Déclaration de type : Le point d'entrée du programme, qui effectue des actions d'entrée/sortie (IO).
 
 main=do Début du Programme : Le mot-clé do indique une séquence d'actions à exécuter.
 
print(greaterThan18 5) Action 2 : Affiche le résultat avec k=5. (5 > 18) → False

 print(greaterThan18 27) Action 3 : Affiche le résultat avec k=27. (27 > 18) → True
 
 print(greaterThan18 18) Action 4 : Affiche le résultat avec k=18. (18 > 18) → False (car 18 n'est pas strictement supérieur à 18)
 
 print(greaterThan18 2) Action 5 : Affiche le résultat avec k=2. (2 > 18) → False

 
