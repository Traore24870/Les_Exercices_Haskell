--Multiplier un nombre par 2
double :: Int -> Int
double x = x * 2

--Incementer un nombre de 1
increment :: Int -> Int
increment x = x + 1

--Double un nombre puis l'incrementer
doubleThenIncrement :: Int -> Int
doubleThenIncrement = increment . double

--La fonction principale
main :: IO ()
main = do
      putStrLn  "****Test double incrementation****"
      print $ double 9
      print $ increment 19
      print $ doubleThenIncrement 52

=====Explication du code==========
      
Bloc de Code Fonction

double x = x * 2 Double : Multiplie l'entrée par 2.

increment x = x + 1 Increment : Ajoute 1 à l'entrée.

doubleThenIncrement = increment . double Composition : Applique double puis increment au résultat.

Bloc de Code Fonction

main = do ... Exécution : Lance les tests d'affichage.

print $ double 9 Affiche le double de 9 (→ 18).

print $ increment 19 Affiche l'incrément de 19 (→ 20).

print $ doubleThenIncrement 52 Affiche double puis incrément de 52 (→ 105).
