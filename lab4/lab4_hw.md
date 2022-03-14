---
title: "Lab 4 Homework"
author: "Arjun Basraon"
date: "2022-03-14"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
library(dplyr)
```

## Data
For the homework, we will use data about vertebrate home range sizes. The data are in the class folder, but the reference is below.  

**Database of vertebrate home range sizes.**  
Reference: Tamburello N, Cote IM, Dulvy NK (2015) Energy and the scaling of animal space use. The American Naturalist 186(2):196-211. http://dx.doi.org/10.1086/682070.  
Data: http://datadryad.org/resource/doi:10.5061/dryad.q5j65/1  

**1. Load the data into a new object called `homerange`.**

**2. Explore the data. Show the dimensions, column names, classes for each variable, and a statistical summary. Keep these as separate code chunks.**  


```r
homerange <-  readr::read_csv("homerange") 
```

```
## Rows: 569 Columns: 24
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr (16): taxon, common.name, class, order, family, genus, species, primarym...
## dbl  (8): mean.mass.g, log10.mass, mean.hra.m2, log10.hra, dimension, preyma...
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
homerange
```

```
## # A tibble: 569 x 24
##    taxon  common.name   class   order   family genus species primarymethod N    
##    <chr>  <chr>         <chr>   <chr>   <chr>  <chr> <chr>   <chr>         <chr>
##  1 lake ~ american eel  actino~ anguil~ angui~ angu~ rostra~ telemetry     16   
##  2 river~ blacktail re~ actino~ cyprin~ catos~ moxo~ poecil~ mark-recaptu~ <NA> 
##  3 river~ central ston~ actino~ cyprin~ cypri~ camp~ anomal~ mark-recaptu~ 20   
##  4 river~ rosyside dace actino~ cyprin~ cypri~ clin~ fundul~ mark-recaptu~ 26   
##  5 river~ longnose dace actino~ cyprin~ cypri~ rhin~ catara~ mark-recaptu~ 17   
##  6 river~ muskellunge   actino~ esocif~ esoci~ esox  masqui~ telemetry     5    
##  7 marin~ pollack       actino~ gadifo~ gadid~ poll~ pollac~ telemetry     2    
##  8 marin~ saithe        actino~ gadifo~ gadid~ poll~ virens  telemetry     2    
##  9 marin~ lined surgeo~ actino~ percif~ acant~ acan~ lineat~ direct obser~ <NA> 
## 10 marin~ orangespine ~ actino~ percif~ acant~ naso  litura~ telemetry     8    
## # ... with 559 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <dbl>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```


```r
names(homerange)
```

```
##  [1] "taxon"                      "common.name"               
##  [3] "class"                      "order"                     
##  [5] "family"                     "genus"                     
##  [7] "species"                    "primarymethod"             
##  [9] "N"                          "mean.mass.g"               
## [11] "log10.mass"                 "alternative.mass.reference"
## [13] "mean.hra.m2"                "log10.hra"                 
## [15] "hra.reference"              "realm"                     
## [17] "thermoregulation"           "locomotion"                
## [19] "trophic.guild"              "dimension"                 
## [21] "preymass"                   "log10.preymass"            
## [23] "PPMR"                       "prey.size.reference"
```

```r
summary(homerange)
```

```
##     taxon           common.name           class              order          
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##     family             genus             species          primarymethod     
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##       N              mean.mass.g        log10.mass     
##  Length:569         Min.   :      0   Min.   :-0.6576  
##  Class :character   1st Qu.:     50   1st Qu.: 1.6990  
##  Mode  :character   Median :    330   Median : 2.5185  
##                     Mean   :  34602   Mean   : 2.5947  
##                     3rd Qu.:   2150   3rd Qu.: 3.3324  
##                     Max.   :4000000   Max.   : 6.6021  
##                                                        
##  alternative.mass.reference  mean.hra.m2          log10.hra     
##  Length:569                 Min.   :0.000e+00   Min.   :-1.523  
##  Class :character           1st Qu.:4.500e+03   1st Qu.: 3.653  
##  Mode  :character           Median :3.934e+04   Median : 4.595  
##                             Mean   :2.146e+07   Mean   : 4.709  
##                             3rd Qu.:1.038e+06   3rd Qu.: 6.016  
##                             Max.   :3.551e+09   Max.   : 9.550  
##                                                                 
##  hra.reference         realm           thermoregulation    locomotion       
##  Length:569         Length:569         Length:569         Length:569        
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  trophic.guild        dimension        preymass         log10.preymass   
##  Length:569         Min.   :2.000   Min.   :     0.67   Min.   :-0.1739  
##  Class :character   1st Qu.:2.000   1st Qu.:    20.02   1st Qu.: 1.3014  
##  Mode  :character   Median :2.000   Median :    53.75   Median : 1.7304  
##                     Mean   :2.218   Mean   :  3989.88   Mean   : 2.0188  
##                     3rd Qu.:2.000   3rd Qu.:   363.35   3rd Qu.: 2.5603  
##                     Max.   :3.000   Max.   :130233.20   Max.   : 5.1147  
##                                     NA's   :502         NA's   :502      
##       PPMR         prey.size.reference
##  Min.   :  0.380   Length:569         
##  1st Qu.:  3.315   Class :character   
##  Median :  7.190   Mode  :character   
##  Mean   : 31.752                      
##  3rd Qu.: 15.966                      
##  Max.   :530.000                      
##  NA's   :502
```

```r
glimpse(homerange)
```

```
## Rows: 569
## Columns: 24
## $ taxon                      <chr> "lake fishes", "river fishes", "river fishe~
## $ common.name                <chr> "american eel", "blacktail redhorse", "cent~
## $ class                      <chr> "actinopterygii", "actinopterygii", "actino~
## $ order                      <chr> "anguilliformes", "cypriniformes", "cyprini~
## $ family                     <chr> "anguillidae", "catostomidae", "cyprinidae"~
## $ genus                      <chr> "anguilla", "moxostoma", "campostoma", "cli~
## $ species                    <chr> "rostrata", "poecilura", "anomalum", "fundu~
## $ primarymethod              <chr> "telemetry", "mark-recapture", "mark-recapt~
## $ N                          <chr> "16", NA, "20", "26", "17", "5", "2", "2", ~
## $ mean.mass.g                <dbl> 887.00, 562.00, 34.00, 4.00, 4.00, 3525.00,~
## $ log10.mass                 <dbl> 2.9479236, 2.7497363, 1.5314789, 0.6020600,~
## $ alternative.mass.reference <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,~
## $ mean.hra.m2                <dbl> 282750.00, 282.10, 116.11, 125.50, 87.10, 3~
## $ log10.hra                  <dbl> 5.4514026, 2.4504031, 2.0648696, 2.0986437,~
## $ hra.reference              <chr> "Minns, C. K. 1995. Allometry of home range~
## $ realm                      <chr> "aquatic", "aquatic", "aquatic", "aquatic",~
## $ thermoregulation           <chr> "ectotherm", "ectotherm", "ectotherm", "ect~
## $ locomotion                 <chr> "swimming", "swimming", "swimming", "swimmi~
## $ trophic.guild              <chr> "carnivore", "carnivore", "carnivore", "car~
## $ dimension                  <dbl> 3, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 3, 3~
## $ preymass                   <dbl> NA, NA, NA, NA, NA, NA, 1.39, NA, NA, NA, N~
## $ log10.preymass             <dbl> NA, NA, NA, NA, NA, NA, 0.1430148, NA, NA, ~
## $ PPMR                       <dbl> NA, NA, NA, NA, NA, NA, 530, NA, NA, NA, NA~
## $ prey.size.reference        <chr> NA, NA, NA, NA, NA, NA, "Brose U, et al. 20~
```


**3. Change the class of the variables `taxon` and `order` to factors and display their levels.**  


```r
homerange$taxon <- as.factor(homerange$taxon)
class(homerange$taxon)
```

```
## [1] "factor"
```


```r
homerange$order <- as.factor(homerange$order)
class(homerange$order)
```

```
## [1] "factor"
```

**4. What taxa are represented in the `homerange` data frame? Make a new data frame `taxa` that is restricted to taxon, common name, class, order, family, genus, species.**  


```r
unique(homerange$taxon)
```

```
## [1] lake fishes   river fishes  marine fishes birds         mammals      
## [6] lizards       snakes        turtles       tortoises    
## 9 Levels: birds lake fishes lizards mammals marine fishes ... turtles
```


```r
taxa <- homerange %>%
  select(taxon, common.name, class, order, family, genus, species) 
taxa
```

```
## # A tibble: 569 x 7
##    taxon         common.name             class   order   family   genus  species
##    <fct>         <chr>                   <chr>   <fct>   <chr>    <chr>  <chr>  
##  1 lake fishes   american eel            actino~ anguil~ anguill~ angui~ rostra~
##  2 river fishes  blacktail redhorse      actino~ cyprin~ catosto~ moxos~ poecil~
##  3 river fishes  central stoneroller     actino~ cyprin~ cyprini~ campo~ anomal~
##  4 river fishes  rosyside dace           actino~ cyprin~ cyprini~ clino~ fundul~
##  5 river fishes  longnose dace           actino~ cyprin~ cyprini~ rhini~ catara~
##  6 river fishes  muskellunge             actino~ esocif~ esocidae esox   masqui~
##  7 marine fishes pollack                 actino~ gadifo~ gadidae  polla~ pollac~
##  8 marine fishes saithe                  actino~ gadifo~ gadidae  polla~ virens 
##  9 marine fishes lined surgeonfish       actino~ percif~ acanthu~ acant~ lineat~
## 10 marine fishes orangespine unicornfish actino~ percif~ acanthu~ naso   litura~
## # ... with 559 more rows
```

**5. The variable `taxon` identifies the large, common name groups of the species represented in `homerange`. Make a table the shows the counts for each of these `taxon`.**  


```r
table(homerange$taxon)
```

```
## 
##         birds   lake fishes       lizards       mammals marine fishes 
##           140             9            11           238            90 
##  river fishes        snakes     tortoises       turtles 
##            14            41            12            14
```

**6. The species in `homerange` are also classified into trophic guilds. How many species are represented in each trophic guild.**  


```r
homerange %>% count(trophic.guild)
```

```
## # A tibble: 2 x 2
##   trophic.guild     n
##   <chr>         <int>
## 1 carnivore       342
## 2 herbivore       227
```


```r
homerange %>%
  select(trophic.guild, species) %>%
  filter(trophic.guild == "herbivore") %>%
  count(species)
```

```
## # A tibble: 212 x 2
##    species              n
##    <chr>            <int>
##  1 aberti               2
##  2 aegyptius            1
##  3 aethiopicus          1
##  4 africaeaustralis     1
##  5 africana             1
##  6 africanus            1
##  7 agassizii            1
##  8 agrestis             1
##  9 alces                1
## 10 americana            2
## # ... with 202 more rows
```


```r
homerange %>%
  select(trophic.guild, species) %>%
  filter(trophic.guild == "carnivore") %>%
  count(species)
```

```
## # A tibble: 322 x 2
##    species        n
##    <chr>      <int>
##  1 adspersus      1
##  2 aedon          1
##  3 alba           2
##  4 albicauda      1
##  5 aluco          1
##  6 americana      2
##  7 americanus     1
##  8 analis         1
##  9 annularis      1
## 10 anomalum       1
## # ... with 312 more rows
```

**7. Make two new data frames, one which is restricted to carnivores and another that is restricted to herbivores.**  


```r
herbivore <- homerange %>%
  filter(trophic.guild == "herbivore")
herbivore
```

```
## # A tibble: 227 x 24
##    taxon  common.name   class   order  family  genus species primarymethod N    
##    <fct>  <chr>         <chr>   <fct>  <chr>   <chr> <chr>   <chr>         <chr>
##  1 marin~ lined surgeo~ actino~ perci~ acanth~ acan~ lineat~ direct obser~ <NA> 
##  2 marin~ orangespine ~ actino~ perci~ acanth~ naso  litura~ telemetry     8    
##  3 marin~ bluespine un~ actino~ perci~ acanth~ naso  unicor~ telemetry     7    
##  4 marin~ redlip blenny actino~ perci~ blenni~ ophi~ atlant~ direct obser~ 20   
##  5 marin~ bermuda chub  actino~ perci~ kyphos~ kyph~ sectat~ telemetry     11   
##  6 marin~ cherubfish    actino~ perci~ pomaca~ cent~ argi    direct obser~ <NA> 
##  7 marin~ damselfish    actino~ perci~ pomace~ chro~ chromis direct obser~ <NA> 
##  8 marin~ twinspot dam~ actino~ perci~ pomace~ chry~ biocel~ direct obser~ 18   
##  9 marin~ wards damsel  actino~ perci~ pomace~ poma~ wardi   direct obser~ <NA> 
## 10 marin~ australian g~ actino~ perci~ pomace~ steg~ apical~ direct obser~ <NA> 
## # ... with 217 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <dbl>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```

**8. Do herbivores or carnivores have, on average, a larger `mean.hra.m2`? Remove any NAs from the data.**  


```r
carnivore <- homerange %>%
  filter(trophic.guild == "carnivore")
carnivore
```

```
## # A tibble: 342 x 24
##    taxon   common.name   class   order  family genus species primarymethod N    
##    <fct>   <chr>         <chr>   <fct>  <chr>  <chr> <chr>   <chr>         <chr>
##  1 lake f~ american eel  actino~ angui~ angui~ angu~ rostra~ telemetry     16   
##  2 river ~ blacktail re~ actino~ cypri~ catos~ moxo~ poecil~ mark-recaptu~ <NA> 
##  3 river ~ central ston~ actino~ cypri~ cypri~ camp~ anomal~ mark-recaptu~ 20   
##  4 river ~ rosyside dace actino~ cypri~ cypri~ clin~ fundul~ mark-recaptu~ 26   
##  5 river ~ longnose dace actino~ cypri~ cypri~ rhin~ catara~ mark-recaptu~ 17   
##  6 river ~ muskellunge   actino~ esoci~ esoci~ esox  masqui~ telemetry     5    
##  7 marine~ pollack       actino~ gadif~ gadid~ poll~ pollac~ telemetry     2    
##  8 marine~ saithe        actino~ gadif~ gadid~ poll~ virens  telemetry     2    
##  9 marine~ giant treval~ actino~ perci~ caran~ cara~ ignobi~ telemetry     4    
## 10 lake f~ rock bass     actino~ perci~ centr~ ambl~ rupest~ mark-recaptu~ 16   
## # ... with 332 more rows, and 15 more variables: mean.mass.g <dbl>,
## #   log10.mass <dbl>, alternative.mass.reference <chr>, mean.hra.m2 <dbl>,
## #   log10.hra <dbl>, hra.reference <chr>, realm <chr>, thermoregulation <chr>,
## #   locomotion <chr>, trophic.guild <chr>, dimension <dbl>, preymass <dbl>,
## #   log10.preymass <dbl>, PPMR <dbl>, prey.size.reference <chr>
```

**9. Make a new dataframe `deer` that is limited to the mean mass, log10 mass, family, genus, and species of deer in the database. The family for deer is cervidae. Arrange the data in descending order by log10 mass. Which is the largest deer? What is its common name?** 


```r
deer <- homerange %>%
  select(mean.mass.g, log10.mass, family, genus, species) %>%
  filter(family == "cervidae")
deer
```

```
## # A tibble: 12 x 5
##    mean.mass.g log10.mass family   genus      species    
##          <dbl>      <dbl> <chr>    <chr>      <chr>      
##  1     307227.       5.49 cervidae alces      alces      
##  2      62823.       4.80 cervidae axis       axis       
##  3      24050.       4.38 cervidae capreolus  capreolus  
##  4     234758.       5.37 cervidae cervus     elaphus    
##  5      29450.       4.47 cervidae cervus     nippon     
##  6      71450.       4.85 cervidae dama       dama       
##  7      13500.       4.13 cervidae muntiacus  reevesi    
##  8      53864.       4.73 cervidae odocoileus hemionus   
##  9      87884.       4.94 cervidae odocoileus virginianus
## 10      35000.       4.54 cervidae ozotoceros bezoarticus
## 11       7500.       3.88 cervidae pudu       puda       
## 12     102059.       5.01 cervidae rangifer   tarandus
```

**10. As measured by the data, which snake species has the smallest homerange? Show all of your work, please. Look this species up online and tell me about it!** **Snake is found in taxon column**    


```r
homerange %>% 
  filter (taxon == "snakes") %>%
  select(taxon, family, genus, species, mean.mass.g) %>%
  arrange(mean.mass.g) 
```

```
## # A tibble: 41 x 5
##    taxon  family     genus         species      mean.mass.g
##    <fct>  <chr>      <chr>         <chr>              <dbl>
##  1 snakes colubridae carphopis     vermis              3.46
##  2 snakes colubridae carphopis     viridis             3.65
##  3 snakes colubridae diadophis     punctatus           9   
##  4 snakes viperidae  bitis         schneideri         17.0 
##  5 snakes colubridae thamnophis    butleri            21.5 
##  6 snakes elapidae   hoplocephalus bungaroides        48.8 
##  7 snakes colubridae oocatochus    rufodorsatus       62.5 
##  8 snakes viperidae  crotalus      pricei             67.2 
##  9 snakes colubridae natrix        natrix             78.5 
## 10 snakes viperidae  vipera        latastei           97.4 
## # ... with 31 more rows
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
