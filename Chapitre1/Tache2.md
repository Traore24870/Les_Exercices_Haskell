--Fonction circleArea qui calcule l'air

circleArea :: Floating a=>a->a
circleArea r= pi*r*r

main :: IO()
main = do
     print(circleArea 4)

  Code Résumé Simple
  
 circleArea :: Floating a => a -> a Type : La fonction circleArea prend un nombre à virgule (le rayon) et retourne un nombre à virgule (l'aire).

 circleArea r = pi*r*r Définition : Pour calculer l'aire, je prends le rayon (r) et je fais pi*r*r.

 main :: IO () Type : Le programme principal (main) va effectuer une action d'entrée/sortie (comme afficher quelque chose).

 main = do Début du Programme : Voici la liste des actions à effectuer, dans l'ordre :

 print(circleArea 4) Action : Affiche à l'écran le résultat du calcul de l'aire pour un rayon de 4.
