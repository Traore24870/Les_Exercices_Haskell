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
      putStrLn  "********Test double incrementation********"
      print $ double 9
      print $ increment 19
      print $ doubleThenIncrement 52
      
