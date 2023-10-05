Лабораторная работа №2
================
Шабанов Р.В.

## Цель Работы

1.  Зекрепить практические навыки использования языка программирования R
    для обработки данных
2.  Закрепить знания основных функций обработки данных экосистемы
    tidyverse языка R
3.  Развить пркатические навыки использования функций обработки данных
    пакета dplyr – функции select(), filter(), mutate(), arrange(),
    group_by()

## Задание роанализировать встроенный в пакет dplyr набор данных starwars с помощью языка R и ответить на вопросы:

## Ход работы

## Задание 1

### Сколько строк в датафрейме?

``` r
library('dplyr')
```


    Присоединяю пакет: 'dplyr'

    Следующие объекты скрыты от 'package:stats':

        filter, lag

    Следующие объекты скрыты от 'package:base':

        intersect, setdiff, setequal, union

``` r
starwars %>% nrow()
```

    [1] 87

### Ответ: 87

## Задание 2

### Сколько столбцов в датафрейме?

``` r
starwars %>% ncol()
```

    [1] 14

### Ответ: 14

## Задание 3

### Как просмотреть примерный вид датафрейма?

``` r
glimpse(starwars)
```

    Rows: 87
    Columns: 14
    $ name       <chr> "Luke Skywalker", "C-3PO", "R2-D2", "Darth Vader", "Leia Or…
    $ height     <int> 172, 167, 96, 202, 150, 178, 165, 97, 183, 182, 188, 180, 2…
    $ mass       <dbl> 77.0, 75.0, 32.0, 136.0, 49.0, 120.0, 75.0, 32.0, 84.0, 77.…
    $ hair_color <chr> "blond", NA, NA, "none", "brown", "brown, grey", "brown", N…
    $ skin_color <chr> "fair", "gold", "white, blue", "white", "light", "light", "…
    $ eye_color  <chr> "blue", "yellow", "red", "yellow", "brown", "blue", "blue",…
    $ birth_year <dbl> 19.0, 112.0, 33.0, 41.9, 19.0, 52.0, 47.0, NA, 24.0, 57.0, …
    $ sex        <chr> "male", "none", "none", "male", "female", "male", "female",…
    $ gender     <chr> "masculine", "masculine", "masculine", "masculine", "femini…
    $ homeworld  <chr> "Tatooine", "Tatooine", "Naboo", "Tatooine", "Alderaan", "T…
    $ species    <chr> "Human", "Droid", "Droid", "Human", "Human", "Human", "Huma…
    $ films      <list> <"The Empire Strikes Back", "Revenge of the Sith", "Return…
    $ vehicles   <list> <"Snowspeeder", "Imperial Speeder Bike">, <>, <>, <>, "Imp…
    $ starships  <list> <"X-wing", "Imperial shuttle">, <>, <>, "TIE Advanced x1",…

## Задание 4

### Cколько уникальных рас персонажей (species) представлено в данных?

``` r
starwars$species
```

     [1] "Human"          "Droid"          "Droid"          "Human"         
     [5] "Human"          "Human"          "Human"          "Droid"         
     [9] "Human"          "Human"          "Human"          "Human"         
    [13] "Wookiee"        "Human"          "Rodian"         "Hutt"          
    [17] "Human"          "Human"          "Yoda's species" "Human"         
    [21] "Human"          "Droid"          "Trandoshan"     "Human"         
    [25] "Human"          "Mon Calamari"   "Human"          "Human"         
    [29] "Ewok"           "Sullustan"      "Human"          "Neimodian"     
    [33] "Human"          "Gungan"         "Gungan"         "Gungan"        
    [37] NA               "Toydarian"      "Dug"            NA              
    [41] "Human"          "Zabrak"         "Twi'lek"        "Twi'lek"       
    [45] "Vulptereen"     "Xexto"          "Toong"          "Human"         
    [49] "Cerean"         "Nautolan"       "Zabrak"         "Tholothian"    
    [53] "Iktotchi"       "Quermian"       "Kel Dor"        "Chagrian"      
    [57] "Human"          "Human"          "Human"          "Geonosian"     
    [61] "Mirialan"       "Mirialan"       "Human"          "Human"         
    [65] "Human"          "Human"          "Clawdite"       "Besalisk"      
    [69] "Kaminoan"       "Kaminoan"       "Human"          "Aleena"        
    [73] "Droid"          "Skakoan"        "Muun"           "Togruta"       
    [77] "Kaleesh"        "Wookiee"        "Human"          NA              
    [81] "Pau'an"         "Human"          "Human"          "Human"         
    [85] "Droid"          NA               "Human"         

### Ответ: 85

## Задание 5

### Найти самого высокого персонажа

``` r
a<-filter(starwars, height != 'NA')
max(a$height)
```

    [1] 264

### Ответ: 264

## Задание 6

### Найти всех персонажей ниже 170

``` r
a<-filter(starwars, height < 170)
a$height
```

     [1] 167  96 150 165  97  66 150  88 160 137 112 163  94 122 163 157 166 165 168
    [20] 167  79  96 165

### Ответ: Кол-во 23

## Задание 7

### Подсчитать ИМТ (индекс массы тела) для всех персонажей. ИМТ подсчитать по формуле 𝐼 = 𝑚ℎ2 , где 𝑚– масса (weight), а ℎ – рост (height).

``` r
a<-filter(starwars, height != 'NA', mass != 'NA')
a$mass*a$height^2
```

     [1]  2277968  2091675   294912  5549344  1102500  3802080  2041875   301088
     [9]  2813076  2550548  2968896  5822208  2592000  2214746 41588750  2225300
    [17]  3564000    74052  2167500  2618840  5600000  4079300  2474991  2419375
    [25]  2689200   154880  1740800  3315161  3283290  2535456  4114432   501760
    [33]  2450000  1742620   397620  1726985  2968896  3214728  3342192  1692800
    [41]  2827520  2909125  2679120  1624180  1377800  2979920  2645631  1552320
    [49]  3998808  4614808    93615  1787952  1805988  7418304  7446816  2792176
    [57]  1520832  3394880  1225125

## Задание 8

### Найти 10 самых “вытянутых” персонажей. “Вытянутость” оценить по отношению массы (mass) к росту (height) персонажей

``` r
a<-filter(starwars, height != 'NA', mass != 'NA')
b <- a$mass/a$height
c <- sort(b, decreasing = TRUE)
c[1:10]
```

     [1] 7.7600000 0.7361111 0.7000000 0.6741573 0.6732673 0.6111111 0.5947368
     [8] 0.5811966 0.5151515 0.4912281

## Задание 9

### Найти средний возраст персонажей каждой расы вселенной Звездных войн.

``` r
a <- filter(starwars, species != 'NA', birth_year != 'NA')
b <- select(a, species, birth_year)
c <- group_by(b,species)
d <- summarize(c, delay = mean(birth_year, na.rm = TRUE))
d
```

    # A tibble: 15 × 2
       species        delay
       <chr>          <dbl>
     1 Cerean          92  
     2 Droid           53.3
     3 Ewok             8  
     4 Gungan          52  
     5 Human           53.4
     6 Hutt           600  
     7 Kel Dor         22  
     8 Mirialan        49  
     9 Mon Calamari    41  
    10 Rodian          44  
    11 Trandoshan      53  
    12 Twi'lek         48  
    13 Wookiee        200  
    14 Yoda's species 896  
    15 Zabrak          54  

## Задание 10

### Найти самый распространенный цвет глаз персонажей вселенной Звездных войн.

``` r
a <-filter(starwars, eye_color != 'NA')
b <- group_by(a, eye_color)
c <- count(b,eye_color)
d <- arrange(c,desc(n))
```

### Ответ: Brown(21)

## Задание 11

### Подсчитать среднюю длину имени в каждой расе вселенной Звездных войн.

``` r
a <- filter(starwars, name != 'NA', species != 'NA')
b <- select(a, name, species)
c <- group_by(b, species)
d <- summarize(c, delay = mean(nchar(name)))
d
```

    # A tibble: 37 × 2
       species   delay
       <chr>     <dbl>
     1 Aleena    13   
     2 Besalisk  15   
     3 Cerean    12   
     4 Chagrian  10   
     5 Clawdite  10   
     6 Droid      4.83
     7 Dug        7   
     8 Ewok      21   
     9 Geonosian 17   
    10 Gungan    11.7 
    # ℹ 27 more rows

## Вывод

Научился пользоваться на практике функциями обработки данных пакета
dplyr
