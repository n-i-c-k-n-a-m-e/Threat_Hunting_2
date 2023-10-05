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
a<-filter(starwars, name != 'NA', height != 'NA', mass != 'NA')
b <- data.frame (a$name,a$mass*(a$height^2))
b
```

                      a.name a.mass....a.height.2.
    1         Luke Skywalker               2277968
    2                  C-3PO               2091675
    3                  R2-D2                294912
    4            Darth Vader               5549344
    5            Leia Organa               1102500
    6              Owen Lars               3802080
    7     Beru Whitesun lars               2041875
    8                  R5-D4                301088
    9      Biggs Darklighter               2813076
    10        Obi-Wan Kenobi               2550548
    11      Anakin Skywalker               2968896
    12             Chewbacca               5822208
    13              Han Solo               2592000
    14                Greedo               2214746
    15 Jabba Desilijic Tiure              41588750
    16        Wedge Antilles               2225300
    17      Jek Tono Porkins               3564000
    18                  Yoda                 74052
    19             Palpatine               2167500
    20             Boba Fett               2618840
    21                 IG-88               5600000
    22                 Bossk               4079300
    23      Lando Calrissian               2474991
    24                 Lobot               2419375
    25                Ackbar               2689200
    26 Wicket Systri Warrick                154880
    27             Nien Nunb               1740800
    28          Qui-Gon Jinn               3315161
    29           Nute Gunray               3283290
    30         Jar Jar Binks               2535456
    31          Roos Tarpals               4114432
    32               Sebulba                501760
    33            Darth Maul               2450000
    34           Ayla Secura               1742620
    35              Dud Bolt                397620
    36        Ben Quadinaros               1726985
    37            Mace Windu               2968896
    38          Ki-Adi-Mundi               3214728
    39             Kit Fisto               3342192
    40            Adi Gallia               1692800
    41              Plo Koon               2827520
    42          Gregar Typho               2909125
    43     Poggle the Lesser               2679120
    44       Luminara Unduli               1624180
    45         Barriss Offee               1377800
    46                 Dooku               2979920
    47            Jango Fett               2645631
    48            Zam Wesell               1552320
    49       Dexter Jettster               3998808
    50               Lama Su               4614808
    51         Ratts Tyerell                 93615
    52            Wat Tambor               1787952
    53              Shaak Ti               1805988
    54              Grievous               7418304
    55               Tarfful               7446816
    56       Raymus Antilles               2792176
    57             Sly Moore               1520832
    58            Tion Medon               3394880
    59         Padmé Amidala               1225125

## Задание 8

### Найти 10 самых “вытянутых” персонажей. “Вытянутость” оценить по отношению массы (mass) к росту (height) персонажей

``` r
a<-filter(starwars, name != 'NA', height != 'NA', mass != 'NA')
b <- data.frame(a$name, a$mass/a$height)
c <- arrange(b, desc(a$mass/a$height))
##c <- sort(b, decreasing = TRUE)
top_n(c,10)
```

    Selecting by a.mass.a.height

                      a.name a.mass.a.height
    1  Jabba Desilijic Tiure       7.7600000
    2               Grievous       0.7361111
    3                  IG-88       0.7000000
    4              Owen Lars       0.6741573
    5            Darth Vader       0.6732673
    6       Jek Tono Porkins       0.6111111
    7                  Bossk       0.5947368
    8                Tarfful       0.5811966
    9        Dexter Jettster       0.5151515
    10             Chewbacca       0.4912281

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
d
```

    # A tibble: 15 × 2
    # Groups:   eye_color [15]
       eye_color         n
       <chr>         <int>
     1 brown            21
     2 blue             19
     3 yellow           11
     4 black            10
     5 orange            8
     6 red               5
     7 hazel             3
     8 unknown           3
     9 blue-gray         1
    10 dark              1
    11 gold              1
    12 green, yellow     1
    13 pink              1
    14 red, blue         1
    15 white             1

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
