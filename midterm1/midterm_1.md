---
title: "Midterm 1"
author: "Arjun Basraon"
date: "2022-01-26"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your code should be organized, clean, and run free from errors. Remember, you must remove the `#` for any included code chunks to run. Be sure to add your name to the author header above. You may use any resources to answer these questions (including each other), but you may not post questions to Open Stacks or external help sites. There are 15 total questions, each is worth 2 points.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

This exam is due by 12:00p on Thursday, January 27.  

## Load the tidyverse
If you plan to use any other libraries to complete this assignment then you should load them here.

```r
library(tidyverse)
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --
```

```
## v ggplot2 3.3.5     v purrr   0.3.4
## v tibble  3.1.6     v dplyr   1.0.7
## v tidyr   1.1.4     v stringr 1.4.0
## v readr   2.1.1     v forcats 0.5.1
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```


```r
getwd()
```

```
## [1] "C:/Users/Magicfullrene laptop/Desktop/bis 15/BIS15W2022_Arjunbasraon/midterm1"
```

## Questions  
Wikipedia's definition of [data science](https://en.wikipedia.org/wiki/Data_science): "Data science is an interdisciplinary field that uses scientific methods, processes, algorithms and systems to extract knowledge and insights from noisy, structured and unstructured data, and apply knowledge and actionable insights from data across a broad range of application domains."  

1. (2 points) Consider the definition of data science above. Although we are only part-way through the quarter, what specific elements of data science do you feel we have practiced? Provide at least one specific example.


#answer1: we have learned to organize data from unstructured data like vectors to stacking and labeling them into data matrices and data frames, we also learned how to filter through large amounts of data in the form of data frames, how to filter the data we need with commands like "select" and "filter".  

2. (2 points) What is the most helpful or interesting thing you have learned so far in BIS 15L? What is something that you think needs more work or practice? 


#answer2: the most interesting was the pipe command and how we can use select and filter to basically browse large amounts of data reminiscent to data tables I browse on wikipedia or NCBI, which will be very usefull for my career ahead. 

In the midterm 1 folder there is a second folder called `data`. Inside the `data` folder, there is a .csv file called `ElephantsMF`. These data are from Phyllis Lee, Stirling University, and are related to Lee, P., et al. (2013), "Enduring consequences of early experiences: 40-year effects on survival and success among African elephants (Loxodonta africana)," Biology Letters, 9: 20130011. [kaggle](https://www.kaggle.com/mostafaelseidy/elephantsmf).  

3. (2 points) Please load these data as a new object called `elephants`. Use the function(s) of your choice to get an idea of the structure of the data. Be sure to show the class of each variable.


```r
getwd()
```

```
## [1] "C:/Users/Magicfullrene laptop/Desktop/bis 15/BIS15W2022_Arjunbasraon/midterm1"
```


```r
elephants <- readr::read_csv("data/ElephantsMF.csv")
```

```
## Rows: 288 Columns: 3
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr (1): Sex
## dbl (2): Age, Height
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
elephants
```

```
## # A tibble: 288 x 3
##      Age Height Sex  
##    <dbl>  <dbl> <chr>
##  1   1.4   120  M    
##  2  17.5   227  M    
##  3  12.8   235  M    
##  4  11.2   210  M    
##  5  12.7   220  M    
##  6  12.7   189  M    
##  7  12.2   225  M    
##  8  12.2   204  M    
##  9  28.2   266. M    
## 10  11.7   233  M    
## # ... with 278 more rows
```

4. (2 points) Change the names of the variables to lower case and change the class of the variable `sex` to a factor.



```r
elephants <- rename(elephants, age = "Age", height="Height", sex="Sex")
```

```r
elephants
```

```
## # A tibble: 288 x 3
##      age height sex  
##    <dbl>  <dbl> <chr>
##  1   1.4   120  M    
##  2  17.5   227  M    
##  3  12.8   235  M    
##  4  11.2   210  M    
##  5  12.7   220  M    
##  6  12.7   189  M    
##  7  12.2   225  M    
##  8  12.2   204  M    
##  9  28.2   266. M    
## 10  11.7   233  M    
## # ... with 278 more rows
```


```r
class(elephants$sex)
```

```
## [1] "character"
```

```r
elephants$sex <- as.factor(elephants$sex)
class(elephants$sex)
```

```
## [1] "factor"
```

```r
elephants
```

```
## # A tibble: 288 x 3
##      age height sex  
##    <dbl>  <dbl> <fct>
##  1   1.4   120  M    
##  2  17.5   227  M    
##  3  12.8   235  M    
##  4  11.2   210  M    
##  5  12.7   220  M    
##  6  12.7   189  M    
##  7  12.2   225  M    
##  8  12.2   204  M    
##  9  28.2   266. M    
## 10  11.7   233  M    
## # ... with 278 more rows
```

5. (2 points) How many male and female elephants are represented in the data?


```r
table(elephants[ ,3])
```

```
## 
##   F   M 
## 150 138
```
150 females, 138 males

6. (2 points) What is the average age all elephants in the data?


```r
mean(elephants$age)
```

```
## [1] 10.97132
```
10.97132 =mean

7. (2 points) How does the average age and height of elephants compare by sex?


```r
  male_elephants <- filter(elephants, sex == "M")
male_elephants
```

```
## # A tibble: 138 x 3
##      age height sex  
##    <dbl>  <dbl> <fct>
##  1   1.4   120  M    
##  2  17.5   227  M    
##  3  12.8   235  M    
##  4  11.2   210  M    
##  5  12.7   220  M    
##  6  12.7   189  M    
##  7  12.2   225  M    
##  8  12.2   204  M    
##  9  28.2   266. M    
## 10  11.7   233  M    
## # ... with 128 more rows
```

```r
mean(male_elephants$age)
```

```
## [1] 8.945145
```

```r
mean(male_elephants$height)
```

```
## [1] 185.1312
```


```r
female_elephants <- filter(elephants, sex == "F")
female_elephants
```

```
## # A tibble: 150 x 3
##      age height sex  
##    <dbl>  <dbl> <fct>
##  1 11.1   218.  F    
##  2  2.33  133.  F    
##  3  2.42  145.  F    
##  4 26.5   206.  F    
##  5 11.8   207   F    
##  6  0.33   85.6 F    
##  7 26.8   227.  F    
##  8 13.4   203   F    
##  9 28.4   228.  F    
## 10  2.08  131.  F    
## # ... with 140 more rows
```

```r
mean(female_elephants$age)
```

```
## [1] 12.8354
```


```r
mean(female_elephants$height)
```

```
## [1] 190.0307
```
since 185.1312<190.0307 and 8.945145<12.8354 female elephants given in the data are older and taller on average

8. (2 points) How does the average height of elephants compare by sex for individuals over 20 years old. Include the min and max height as well as the number of individuals in the sample as part of your analysis.  


```r
males <- elephants%>%
  filter(sex == "M")%>%
  filter(age>20)
males
```

```
## # A tibble: 13 x 3
##      age height sex  
##    <dbl>  <dbl> <fct>
##  1  28.2   266. M    
##  2  25.4   252. M    
##  3  26.5   258. M    
##  4  26.7   269. M    
##  5  25.7   237. M    
##  6  28.8   302. M    
##  7  24.2   253. M    
##  8  23.9   282. M    
##  9  26.1   304. M    
## 10  25.4   294. M    
## 11  24.2   287. M    
## 12  21.2   273. M    
## 13  21.3   229. M
```

```r
dim(males)
```

```
## [1] 13  3
```
there are 13 male elephants over the age of 20

```r
mean(males$height)
```

```
## [1] 269.5931
```
the mean height of male elephants over the age of 20 is 269.5931

```r
summary(males)
```

```
##       age            height      sex   
##  Min.   :21.25   Min.   :228.7   F: 0  
##  1st Qu.:24.17   1st Qu.:253.1   M:13  
##  Median :25.42   Median :268.6         
##  Mean   :25.19   Mean   :269.6         
##  3rd Qu.:26.50   3rd Qu.:287.1         
##  Max.   :28.75   Max.   :304.1
```
the minimum height of the elephant here is 228.7, while the largest male is 304.1


```r
females <- elephants%>%
  filter(sex == "F")%>%
  filter(age>20)
females
```

```
## # A tibble: 37 x 3
##      age height sex  
##    <dbl>  <dbl> <fct>
##  1  26.5   206. F    
##  2  26.8   227. F    
##  3  28.4   228. F    
##  4  27.2   226. F    
##  5  25.4   240. F    
##  6  23.3   238. F    
##  7  26.8   235. F    
##  8  27.8   265  F    
##  9  28.2   216. F    
## 10  26.1   216. F    
## # ... with 27 more rows
```

```r
dim(females)
```

```
## [1] 37  3
```
there are 37 female elephants in the data

```r
mean(females$height)
```

```
## [1] 232.2014
```
mean height of females over the age of 20 is 232.2014, this is smaller than the mean height of male elephants over the age of 20 is 269.5931, with a difference of 37.3917 

```r
summary(females)
```

```
##       age            height      sex   
##  Min.   :20.17   Min.   :192.5   F:37  
##  1st Qu.:23.33   1st Qu.:221.6   M: 0  
##  Median :26.08   Median :227.3         
##  Mean   :25.63   Mean   :232.2         
##  3rd Qu.:27.42   3rd Qu.:241.9         
##  Max.   :32.17   Max.   :277.8
```
the max height of a female over 20 is 277.8 and the minimum is 192.5

For the next series of questions, we will use data from a study on vertebrate community composition and impacts from defaunation in [Gabon, Africa](https://en.wikipedia.org/wiki/Gabon). One thing to notice is that the data include 24 separate transects. Each transect represents a path through different forest management areas.  

Reference: Koerner SE, Poulsen JR, Blanchard EJ, Okouyi J, Clark CJ. Vertebrate community composition and diversity declines along a defaunation gradient radiating from rural villages in Gabon. _Journal of Applied Ecology_. 2016. This paper, along with a description of the variables is included inside the midterm 1 folder.  

9. (2 points) Load `IvindoData_DryadVersion.csv` and use the function(s) of your choice to get an idea of the overall structure. Change the variables `HuntCat` and `LandUse` to factors.


```r
gabon <- readr::read_csv("data/IvindoData_DryadVersion.csv")
```

```
## Rows: 24 Columns: 26
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr  (2): HuntCat, LandUse
## dbl (24): TransectID, Distance, NumHouseholds, Veg_Rich, Veg_Stems, Veg_lian...
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
gabon
```

```
## # A tibble: 24 x 26
##    TransectID Distance HuntCat  NumHouseholds LandUse Veg_Rich Veg_Stems
##         <dbl>    <dbl> <chr>            <dbl> <chr>      <dbl>     <dbl>
##  1          1     7.14 Moderate            54 Park        16.7      31.2
##  2          2    17.3  None                54 Park        15.8      37.4
##  3          2    18.3  None                29 Park        16.9      32.3
##  4          3    20.8  None                29 Logging     12.4      29.4
##  5          4    16.0  None                29 Park        17.1      36  
##  6          5    17.5  None                29 Park        16.5      29.2
##  7          6    24.1  None                29 Park        14.8      31.2
##  8          7    19.8  None                54 Logging     13.2      32.6
##  9          8     5.78 High                25 Neither     12.6      23.7
## 10          9     5.13 High                73 Logging     16        27.1
## # ... with 14 more rows, and 19 more variables: Veg_liana <dbl>, Veg_DBH <dbl>,
## #   Veg_Canopy <dbl>, Veg_Understory <dbl>, RA_Apes <dbl>, RA_Birds <dbl>,
## #   RA_Elephant <dbl>, RA_Monkeys <dbl>, RA_Rodent <dbl>, RA_Ungulate <dbl>,
## #   Rich_AllSpecies <dbl>, Evenness_AllSpecies <dbl>,
## #   Diversity_AllSpecies <dbl>, Rich_BirdSpecies <dbl>,
## #   Evenness_BirdSpecies <dbl>, Diversity_BirdSpecies <dbl>,
## #   Rich_MammalSpecies <dbl>, Evenness_MammalSpecies <dbl>, ...
```

```r
str(gabon)
```

```
## spec_tbl_df [24 x 26] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ TransectID             : num [1:24] 1 2 2 3 4 5 6 7 8 9 ...
##  $ Distance               : num [1:24] 7.14 17.31 18.32 20.85 15.95 ...
##  $ HuntCat                : chr [1:24] "Moderate" "None" "None" "None" ...
##  $ NumHouseholds          : num [1:24] 54 54 29 29 29 29 29 54 25 73 ...
##  $ LandUse                : chr [1:24] "Park" "Park" "Park" "Logging" ...
##  $ Veg_Rich               : num [1:24] 16.7 15.8 16.9 12.4 17.1 ...
##  $ Veg_Stems              : num [1:24] 31.2 37.4 32.3 29.4 36 ...
##  $ Veg_liana              : num [1:24] 5.78 13.25 4.75 9.78 13.25 ...
##  $ Veg_DBH                : num [1:24] 49.6 34.6 42.8 36.6 41.5 ...
##  $ Veg_Canopy             : num [1:24] 3.78 3.75 3.43 3.75 3.88 2.5 4 4 3 3.25 ...
##  $ Veg_Understory         : num [1:24] 2.89 3.88 3 2.75 3.25 3 2.38 2.71 3.25 3.13 ...
##  $ RA_Apes                : num [1:24] 1.87 0 4.49 12.93 0 ...
##  $ RA_Birds               : num [1:24] 52.7 52.2 37.4 59.3 52.6 ...
##  $ RA_Elephant            : num [1:24] 0 0.86 1.33 0.56 1 0 1.11 0.43 2.2 0 ...
##  $ RA_Monkeys             : num [1:24] 38.6 28.5 41.8 19.9 41.3 ...
##  $ RA_Rodent              : num [1:24] 4.22 6.04 1.06 3.66 2.52 1.83 3.1 1.26 4.37 6.31 ...
##  $ RA_Ungulate            : num [1:24] 2.66 12.41 13.86 3.71 2.53 ...
##  $ Rich_AllSpecies        : num [1:24] 22 20 22 19 20 22 23 19 19 19 ...
##  $ Evenness_AllSpecies    : num [1:24] 0.793 0.773 0.74 0.681 0.811 0.786 0.818 0.757 0.773 0.668 ...
##  $ Diversity_AllSpecies   : num [1:24] 2.45 2.31 2.29 2.01 2.43 ...
##  $ Rich_BirdSpecies       : num [1:24] 11 10 11 8 8 10 11 11 11 9 ...
##  $ Evenness_BirdSpecies   : num [1:24] 0.732 0.704 0.688 0.559 0.799 0.771 0.801 0.687 0.784 0.573 ...
##  $ Diversity_BirdSpecies  : num [1:24] 1.76 1.62 1.65 1.16 1.66 ...
##  $ Rich_MammalSpecies     : num [1:24] 11 10 11 11 12 12 12 8 8 10 ...
##  $ Evenness_MammalSpecies : num [1:24] 0.736 0.705 0.65 0.619 0.736 0.694 0.776 0.79 0.821 0.783 ...
##  $ Diversity_MammalSpecies: num [1:24] 1.76 1.62 1.56 1.48 1.83 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   TransectID = col_double(),
##   ..   Distance = col_double(),
##   ..   HuntCat = col_character(),
##   ..   NumHouseholds = col_double(),
##   ..   LandUse = col_character(),
##   ..   Veg_Rich = col_double(),
##   ..   Veg_Stems = col_double(),
##   ..   Veg_liana = col_double(),
##   ..   Veg_DBH = col_double(),
##   ..   Veg_Canopy = col_double(),
##   ..   Veg_Understory = col_double(),
##   ..   RA_Apes = col_double(),
##   ..   RA_Birds = col_double(),
##   ..   RA_Elephant = col_double(),
##   ..   RA_Monkeys = col_double(),
##   ..   RA_Rodent = col_double(),
##   ..   RA_Ungulate = col_double(),
##   ..   Rich_AllSpecies = col_double(),
##   ..   Evenness_AllSpecies = col_double(),
##   ..   Diversity_AllSpecies = col_double(),
##   ..   Rich_BirdSpecies = col_double(),
##   ..   Evenness_BirdSpecies = col_double(),
##   ..   Diversity_BirdSpecies = col_double(),
##   ..   Rich_MammalSpecies = col_double(),
##   ..   Evenness_MammalSpecies = col_double(),
##   ..   Diversity_MammalSpecies = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```


```r
summary(gabon)
```

```
##    TransectID       Distance        HuntCat          NumHouseholds  
##  Min.   : 1.00   Min.   : 2.700   Length:24          Min.   :13.00  
##  1st Qu.: 5.75   1st Qu.: 5.668   Class :character   1st Qu.:24.75  
##  Median :14.50   Median : 9.720   Mode  :character   Median :29.00  
##  Mean   :13.50   Mean   :11.879                      Mean   :37.88  
##  3rd Qu.:20.25   3rd Qu.:17.683                      3rd Qu.:54.00  
##  Max.   :27.00   Max.   :26.760                      Max.   :73.00  
##    LandUse             Veg_Rich       Veg_Stems       Veg_liana     
##  Length:24          Min.   :10.88   Min.   :23.44   Min.   : 4.750  
##  Class :character   1st Qu.:13.10   1st Qu.:28.69   1st Qu.: 9.033  
##  Mode  :character   Median :14.94   Median :32.45   Median :11.940  
##                     Mean   :14.83   Mean   :32.80   Mean   :11.040  
##                     3rd Qu.:16.54   3rd Qu.:37.08   3rd Qu.:13.250  
##                     Max.   :18.75   Max.   :47.56   Max.   :16.380  
##     Veg_DBH        Veg_Canopy    Veg_Understory     RA_Apes      
##  Min.   :28.45   Min.   :2.500   Min.   :2.380   Min.   : 0.000  
##  1st Qu.:40.65   1st Qu.:3.250   1st Qu.:2.875   1st Qu.: 0.000  
##  Median :43.90   Median :3.430   Median :3.000   Median : 0.485  
##  Mean   :46.09   Mean   :3.469   Mean   :3.020   Mean   : 2.045  
##  3rd Qu.:50.58   3rd Qu.:3.750   3rd Qu.:3.167   3rd Qu.: 3.815  
##  Max.   :76.48   Max.   :4.000   Max.   :3.880   Max.   :12.930  
##     RA_Birds      RA_Elephant       RA_Monkeys      RA_Rodent    
##  Min.   :31.56   Min.   :0.0000   Min.   : 5.84   Min.   :1.060  
##  1st Qu.:52.51   1st Qu.:0.0000   1st Qu.:22.70   1st Qu.:2.047  
##  Median :57.90   Median :0.3600   Median :31.74   Median :3.230  
##  Mean   :58.64   Mean   :0.5450   Mean   :31.30   Mean   :3.278  
##  3rd Qu.:68.17   3rd Qu.:0.8925   3rd Qu.:39.88   3rd Qu.:4.093  
##  Max.   :85.03   Max.   :2.3000   Max.   :54.12   Max.   :6.310  
##   RA_Ungulate     Rich_AllSpecies Evenness_AllSpecies Diversity_AllSpecies
##  Min.   : 0.000   Min.   :15.00   Min.   :0.6680      Min.   :1.966       
##  1st Qu.: 1.232   1st Qu.:19.00   1st Qu.:0.7542      1st Qu.:2.248       
##  Median : 2.545   Median :20.00   Median :0.7760      Median :2.316       
##  Mean   : 4.166   Mean   :20.21   Mean   :0.7699      Mean   :2.310       
##  3rd Qu.: 5.157   3rd Qu.:22.00   3rd Qu.:0.8083      3rd Qu.:2.429       
##  Max.   :13.860   Max.   :24.00   Max.   :0.8330      Max.   :2.566       
##  Rich_BirdSpecies Evenness_BirdSpecies Diversity_BirdSpecies Rich_MammalSpecies
##  Min.   : 8.00    Min.   :0.5590       Min.   :1.162         Min.   : 6.000    
##  1st Qu.:10.00    1st Qu.:0.6825       1st Qu.:1.603         1st Qu.: 9.000    
##  Median :11.00    Median :0.7220       Median :1.680         Median :10.000    
##  Mean   :10.33    Mean   :0.7137       Mean   :1.661         Mean   : 9.875    
##  3rd Qu.:11.00    3rd Qu.:0.7722       3rd Qu.:1.784         3rd Qu.:11.000    
##  Max.   :13.00    Max.   :0.8240       Max.   :2.008         Max.   :12.000    
##  Evenness_MammalSpecies Diversity_MammalSpecies
##  Min.   :0.6190         Min.   :1.378          
##  1st Qu.:0.7073         1st Qu.:1.567          
##  Median :0.7390         Median :1.699          
##  Mean   :0.7477         Mean   :1.698          
##  3rd Qu.:0.7847         3rd Qu.:1.815          
##  Max.   :0.8610         Max.   :2.065
```


```r
names(gabon)
```

```
##  [1] "TransectID"              "Distance"               
##  [3] "HuntCat"                 "NumHouseholds"          
##  [5] "LandUse"                 "Veg_Rich"               
##  [7] "Veg_Stems"               "Veg_liana"              
##  [9] "Veg_DBH"                 "Veg_Canopy"             
## [11] "Veg_Understory"          "RA_Apes"                
## [13] "RA_Birds"                "RA_Elephant"            
## [15] "RA_Monkeys"              "RA_Rodent"              
## [17] "RA_Ungulate"             "Rich_AllSpecies"        
## [19] "Evenness_AllSpecies"     "Diversity_AllSpecies"   
## [21] "Rich_BirdSpecies"        "Evenness_BirdSpecies"   
## [23] "Diversity_BirdSpecies"   "Rich_MammalSpecies"     
## [25] "Evenness_MammalSpecies"  "Diversity_MammalSpecies"
```

```r
class(gabon$HuntCat)
```

```
## [1] "character"
```

```r
class(gabon$LandUse)
```

```
## [1] "character"
```

```r
gabon$HuntCat <- as.factor(gabon$HuntCat)
gabon$LandUse <- as.factor(gabon$LandUse)
class(gabon$HuntCat)
```

```
## [1] "factor"
```

```r
class(gabon$LandUse)
```

```
## [1] "factor"
```

10. (4 points) For the transects with high and moderate hunting intensity, how does the average diversity of birds and mammals compare?


```r
high <- gabon%>%
  filter(HuntCat == "High")
high
```

```
## # A tibble: 7 x 26
##   TransectID Distance HuntCat NumHouseholds LandUse Veg_Rich Veg_Stems Veg_liana
##        <dbl>    <dbl> <fct>           <dbl> <fct>      <dbl>     <dbl>     <dbl>
## 1          8     5.78 High               25 Neither     12.6      23.7      5.13
## 2          9     5.13 High               73 Logging     16        27.1      9.75
## 3         15     2.7  High               46 Neither     10.9      25.4      9.25
## 4         17     3.83 High               19 Neither     14.2      32.6     16.4 
## 5         21     5.14 High               24 Neither     16.2      34.9     15.4 
## 6         22     5.33 High               13 Logging     17.1      41.6     13.4 
## 7         27     2.92 High               13 Logging     12.4      47.6     12.9 
## # ... with 18 more variables: Veg_DBH <dbl>, Veg_Canopy <dbl>,
## #   Veg_Understory <dbl>, RA_Apes <dbl>, RA_Birds <dbl>, RA_Elephant <dbl>,
## #   RA_Monkeys <dbl>, RA_Rodent <dbl>, RA_Ungulate <dbl>,
## #   Rich_AllSpecies <dbl>, Evenness_AllSpecies <dbl>,
## #   Diversity_AllSpecies <dbl>, Rich_BirdSpecies <dbl>,
## #   Evenness_BirdSpecies <dbl>, Diversity_BirdSpecies <dbl>,
## #   Rich_MammalSpecies <dbl>, Evenness_MammalSpecies <dbl>, ...
```

```r
moderate <- gabon%>%
  filter(HuntCat == "Moderate")
moderate
```

```
## # A tibble: 8 x 26
##   TransectID Distance HuntCat NumHouseholds LandUse Veg_Rich Veg_Stems Veg_liana
##        <dbl>    <dbl> <fct>           <dbl> <fct>      <dbl>     <dbl>     <dbl>
## 1          1     7.14 Modera~            54 Park        16.7      31.2      5.78
## 2         13     6.61 Modera~            46 Logging     12.4      23.4      7   
## 3         14     8.23 Modera~            56 Logging     15.8      30.2     14.1 
## 4         16     6.1  Modera~            36 Logging     14.6      39.1     11.9 
## 5         19    14.0  Modera~            54 Logging     14.9      35       12   
## 6         20     6.61 Modera~            24 Logging     13.2      26.9     10.5 
## 7         25    15.0  Modera~            54 Logging     15        26.8     12.6 
## 8         26    11.2  Modera~            73 Logging     18.8      39.1     16   
## # ... with 18 more variables: Veg_DBH <dbl>, Veg_Canopy <dbl>,
## #   Veg_Understory <dbl>, RA_Apes <dbl>, RA_Birds <dbl>, RA_Elephant <dbl>,
## #   RA_Monkeys <dbl>, RA_Rodent <dbl>, RA_Ungulate <dbl>,
## #   Rich_AllSpecies <dbl>, Evenness_AllSpecies <dbl>,
## #   Diversity_AllSpecies <dbl>, Rich_BirdSpecies <dbl>,
## #   Evenness_BirdSpecies <dbl>, Diversity_BirdSpecies <dbl>,
## #   Rich_MammalSpecies <dbl>, Evenness_MammalSpecies <dbl>, ...
```

```r
high %>%
  select(Diversity_BirdSpecies, Diversity_MammalSpecies)
```

```
## # A tibble: 7 x 2
##   Diversity_BirdSpecies Diversity_MammalSpecies
##                   <dbl>                   <dbl>
## 1                  1.88                    1.71
## 2                  1.26                    1.80
## 3                  1.71                    1.57
## 4                  1.86                    1.64
## 5                  1.81                    1.71
## 6                  1.39                    1.90
## 7                  1.72                    1.83
```

```r
mean(high$Diversity_BirdSpecies)
```

```
## [1] 1.660857
```


```r
mean(high$Diversity_MammalSpecies)
```

```
## [1] 1.737
```


```r
moderate %>%
  select(Diversity_BirdSpecies, Diversity_MammalSpecies)
```

```
## # A tibble: 8 x 2
##   Diversity_BirdSpecies Diversity_MammalSpecies
##                   <dbl>                   <dbl>
## 1                  1.76                    1.76
## 2                  1.60                    1.69
## 3                  1.68                    2.06
## 4                  1.46                    1.44
## 5                  1.60                    1.38
## 6                  1.71                    1.51
## 7                  1.48                    1.94
## 8                  1.68                    1.68
```

```r
mean(moderate$Diversity_BirdSpecies)
```

```
## [1] 1.62125
```


```r
mean(moderate$Diversity_MammalSpecies)
```

```
## [1] 1.68375
```
in high hunting intensity, the average bird species diversity is larger than moderate hunting intensity (1.660857>1.62125)
in high hunting intensity, the average mammal species diversity is larger than moderate hunting intensity (1.737>1.68375)

11. (4 points) One of the conclusions in the study is that the relative abundance of animals drops off the closer you get to a village. Let's try to reconstruct this (without the statistics). How does the relative abundance (RA) of apes, birds, elephants, monkeys, rodents, and ungulates compare between sites that are less than 3km from a village to sites that are greater than 25km from a village? The variable `Distance` measures the distance of the transect from the nearest village. Hint: try using the `across` operator.  


```r
near <- gabon%>%
  filter(Distance < 3)%>%
  select (Distance, RA_Apes, RA_Birds, RA_Elephant, RA_Monkeys, RA_Rodent, RA_Ungulate) %>%
  summarize(across(contains("RA_"), mean))
near
```

```
## # A tibble: 1 x 6
##   RA_Apes RA_Birds RA_Elephant RA_Monkeys RA_Rodent RA_Ungulate
##     <dbl>    <dbl>       <dbl>      <dbl>     <dbl>       <dbl>
## 1    0.12     76.6       0.145       17.3      3.90        1.87
```


```r
far <- gabon%>%
  filter(Distance > 25)%>%
  select (Distance, RA_Apes, RA_Birds, RA_Elephant, RA_Monkeys, RA_Rodent, RA_Ungulate) %>%
  summarize(across(contains("RA_"), mean))
far
```

```
## # A tibble: 1 x 6
##   RA_Apes RA_Birds RA_Elephant RA_Monkeys RA_Rodent RA_Ungulate
##     <dbl>    <dbl>       <dbl>      <dbl>     <dbl>       <dbl>
## 1    4.91     31.6           0       54.1      1.29        8.12
```

There is more abundance of birds, elephants and rodents at distances less than 3 while there is more abundance of apes, monkeys, and ungulates at distances more than 25.

12. (4 points) Based on your interest, do one exploratory analysis on the `gabon` data of your choice. This analysis needs to include a minimum of two functions in `dplyr.`

I will be seeing if there is a correlation between land use and all species diversity.


```r
logging_land <- gabon %>%
  filter(LandUse == "Logging") %>%
  arrange(Diversity_AllSpecies) %>%
  select(LandUse, Diversity_AllSpecies)
logging_land
```

```
## # A tibble: 13 x 2
##    LandUse Diversity_AllSpecies
##    <fct>                  <dbl>
##  1 Logging                 1.97
##  2 Logging                 2.01
##  3 Logging                 2.13
##  4 Logging                 2.16
##  5 Logging                 2.19
##  6 Logging                 2.23
##  7 Logging                 2.27
##  8 Logging                 2.27
##  9 Logging                 2.32
## 10 Logging                 2.36
## 11 Logging                 2.37
## 12 Logging                 2.37
## 13 Logging                 2.38
```

```r
mean(logging_land$Diversity_AllSpecies)
```

```
## [1] 2.232538
```

```r
park_land <- gabon %>%
  filter(LandUse == "Park") %>%
  arrange(Diversity_AllSpecies) %>%
  select(LandUse, Diversity_AllSpecies)
park_land
```

```
## # A tibble: 7 x 2
##   LandUse Diversity_AllSpecies
##   <fct>                  <dbl>
## 1 Park                    2.29
## 2 Park                    2.31
## 3 Park                    2.43
## 4 Park                    2.43
## 5 Park                    2.45
## 6 Park                    2.50
## 7 Park                    2.57
```

```r
mean(park_land$Diversity_AllSpecies)
```

```
## [1] 2.425143
```


```r
neither_land <- gabon %>%
  filter(LandUse == "Neither") %>%
  arrange(Diversity_AllSpecies) %>%
  select(LandUse, Diversity_AllSpecies)
neither_land
```

```
## # A tibble: 4 x 2
##   LandUse Diversity_AllSpecies
##   <fct>                  <dbl>
## 1 Neither                 2.25
## 2 Neither                 2.28
## 3 Neither                 2.45
## 4 Neither                 2.45
```

```r
mean(neither_land$Diversity_AllSpecies)
```

```
## [1] 2.3575
```
2.425143>2.3575>2.232538 hence parks have the highest amount of diversity of all species, then comes neither and then logging
