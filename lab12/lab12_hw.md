---
title: "Lab 12 Homework"
author: "Please Add Your Name Here"
date: "2022-03-14"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above. For any included plots, make sure they are clearly labeled. You are free to use any plot type that you feel best communicates the results of your analysis.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(here)
library(ggmap)
```



## Load the Data
We will use two separate data sets for this homework.  

1. The first [data set](https://rcweb.dartmouth.edu/~f002d69/workshops/index_rspatial.html) represent sightings of grizzly bears (Ursos arctos) in Alaska. 


```r
grizzly <- read_csv(here("lab12", "data", "bear-sightings.csv"))
```

```
## Rows: 494 Columns: 3
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## dbl (3): bear.id, longitude, latitude
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
grizzly
```

```
## # A tibble: 494 x 3
##    bear.id longitude latitude
##      <dbl>     <dbl>    <dbl>
##  1       7     -149.     62.7
##  2      57     -153.     58.4
##  3      69     -145.     62.4
##  4      75     -153.     59.9
##  5     104     -143.     61.1
##  6     108     -150.     62.9
##  7     115     -152.     68.0
##  8     116     -147.     62.6
##  9     125     -157.     60.2
## 10     135     -156.     58.9
## # ... with 484 more rows
```

2. The second data set is from Brandell, Ellen E (2021), Serological dataset and R code for: Patterns and processes of pathogen exposure in gray wolves across North America, Dryad, [Dataset](https://doi.org/10.5061/dryad.5hqbzkh51).  


```r
wolf <- read_csv(here("lab12", "data", "wolves_data", "wolves_dataset.csv"))
```

```
## Rows: 1986 Columns: 23
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr  (4): pop, age.cat, sex, color
## dbl (19): year, lat, long, habitat, human, pop.density, pack.size, standard....
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
wolf
```

```
## # A tibble: 1,986 x 23
##    pop     year age.cat sex   color   lat  long habitat human pop.density
##    <chr>  <dbl> <chr>   <chr> <chr> <dbl> <dbl>   <dbl> <dbl>       <dbl>
##  1 AK.PEN  2006 S       F     G      57.0 -158.    254.  10.4           8
##  2 AK.PEN  2006 S       M     G      57.0 -158.    254.  10.4           8
##  3 AK.PEN  2006 A       F     G      57.0 -158.    254.  10.4           8
##  4 AK.PEN  2006 S       M     B      57.0 -158.    254.  10.4           8
##  5 AK.PEN  2006 A       M     B      57.0 -158.    254.  10.4           8
##  6 AK.PEN  2006 A       M     G      57.0 -158.    254.  10.4           8
##  7 AK.PEN  2006 A       F     G      57.0 -158.    254.  10.4           8
##  8 AK.PEN  2006 P       M     G      57.0 -158.    254.  10.4           8
##  9 AK.PEN  2006 S       F     G      57.0 -158.    254.  10.4           8
## 10 AK.PEN  2006 P       M     G      57.0 -158.    254.  10.4           8
## # ... with 1,976 more rows, and 13 more variables: pack.size <dbl>,
## #   standard.habitat <dbl>, standard.human <dbl>, standard.pop <dbl>,
## #   standard.packsize <dbl>, standard.latitude <dbl>, standard.longitude <dbl>,
## #   cav.binary <dbl>, cdv.binary <dbl>, cpv.binary <dbl>, chv.binary <dbl>,
## #   neo.binary <dbl>, toxo.binary <dbl>
```

1. Load the `grizzly` data and evaluate its structure. As part of this step, produce a summary that provides the range of latitude and longitude so you can build an appropriate bounding box.


```r
grizzly %>% 
  select(latitude, longitude) %>% 
  summary()
```

```
##     latitude       longitude     
##  Min.   :55.02   Min.   :-166.2  
##  1st Qu.:58.13   1st Qu.:-154.2  
##  Median :60.97   Median :-151.0  
##  Mean   :61.41   Mean   :-149.1  
##  3rd Qu.:64.13   3rd Qu.:-145.6  
##  Max.   :70.37   Max.   :-131.3
```


```r
lat <- c(55.02, 70.37)
long <- c(-166.2, -131.3)
bbox <- make_bbox(long, lat, f = 0.05)
```

2. Use the range of the latitude and longitude to build an appropriate bounding box for your map.
3. Load a map from `stamen` in a terrain style projection and display the map.

```r
grizzlymap <- get_map(bbox, maptype = "terrain", source = "stamen")
```

```
## Source : http://tile.stamen.com/terrain/5/1/6.png
```

```
## Source : http://tile.stamen.com/terrain/5/2/6.png
```

```
## Source : http://tile.stamen.com/terrain/5/3/6.png
```

```
## Source : http://tile.stamen.com/terrain/5/4/6.png
```

```
## Source : http://tile.stamen.com/terrain/5/1/7.png
```

```
## Source : http://tile.stamen.com/terrain/5/2/7.png
```

```
## Source : http://tile.stamen.com/terrain/5/3/7.png
```

```
## Source : http://tile.stamen.com/terrain/5/4/7.png
```

```
## Source : http://tile.stamen.com/terrain/5/1/8.png
```

```
## Source : http://tile.stamen.com/terrain/5/2/8.png
```

```
## Source : http://tile.stamen.com/terrain/5/3/8.png
```

```
## Source : http://tile.stamen.com/terrain/5/4/8.png
```

```
## Source : http://tile.stamen.com/terrain/5/1/9.png
```

```
## Source : http://tile.stamen.com/terrain/5/2/9.png
```

```
## Source : http://tile.stamen.com/terrain/5/3/9.png
```

```
## Source : http://tile.stamen.com/terrain/5/4/9.png
```

```
## Source : http://tile.stamen.com/terrain/5/1/10.png
```

```
## Source : http://tile.stamen.com/terrain/5/2/10.png
```

```
## Source : http://tile.stamen.com/terrain/5/3/10.png
```

```
## Source : http://tile.stamen.com/terrain/5/4/10.png
```

```r
ggmap(grizzlymap)
```

![](lab12_hw_files/figure-html/unnamed-chunk-6-1.png)<!-- -->



4. Build a final map that overlays the recorded observations of grizzly bears in Alaska.


```r
ggmap(grizzlymap) + 
  geom_point(data = grizzly, aes(longitude, latitude)) +
  labs(x= "Longitude", y= "Latitude", title="Bear sightings")
```

![](lab12_hw_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

Let's switch to the wolves data. Brandell, Ellen E (2021), Serological dataset and R code for: Patterns and processes of pathogen exposure in gray wolves across North America, Dryad, [Dataset](https://doi.org/10.5061/dryad.5hqbzkh51).  

5. Load the data and evaluate its structure.  


```r
wolf %>% 
  select(lat, long) %>% 
  summary()
```

```
##       lat             long        
##  Min.   :33.89   Min.   :-157.84  
##  1st Qu.:44.60   1st Qu.:-123.73  
##  Median :46.83   Median :-110.99  
##  Mean   :50.43   Mean   :-116.86  
##  3rd Qu.:57.89   3rd Qu.:-110.55  
##  Max.   :80.50   Max.   : -82.42
```

6. How many distinct wolf populations are included in this study? Mae a new object that restricts the data to the wolf populations in the lower 48 US states.


```r
wolf2 <- filter(wolf, pop != "AK.PEN")
wolf2
```

```
## # A tibble: 1,886 x 23
##    pop      year age.cat sex   color   lat  long habitat human pop.density
##    <chr>   <dbl> <chr>   <chr> <chr> <dbl> <dbl>   <dbl> <dbl>       <dbl>
##  1 BAN.JAS  2001 A       F     B      52.2 -117.  18553. 1145.        8.85
##  2 BAN.JAS  2003 A       F     B      52.2 -117.  18553. 1145.        8.85
##  3 BAN.JAS  2001 A       F     B      52.2 -117.  18553. 1145.        8.85
##  4 BAN.JAS  2003 A       F     B      52.2 -117.  18553. 1145.        8.85
##  5 BAN.JAS  2005 S       M     B      52.2 -117.  18553. 1145.        8.85
##  6 BAN.JAS  2001 A       F     G      52.2 -117.  18553. 1145.        8.85
##  7 BAN.JAS  2001 S       F     G      52.2 -117.  18553. 1145.        8.85
##  8 BAN.JAS  2006 A       F     <NA>   52.2 -117.  18553. 1145.        8.85
##  9 BAN.JAS  2001 A       M     G      52.2 -117.  18553. 1145.        8.85
## 10 BAN.JAS  2003 A       M     G      52.2 -117.  18553. 1145.        8.85
## # ... with 1,876 more rows, and 13 more variables: pack.size <dbl>,
## #   standard.habitat <dbl>, standard.human <dbl>, standard.pop <dbl>,
## #   standard.packsize <dbl>, standard.latitude <dbl>, standard.longitude <dbl>,
## #   cav.binary <dbl>, cdv.binary <dbl>, cpv.binary <dbl>, chv.binary <dbl>,
## #   neo.binary <dbl>, toxo.binary <dbl>
```

7. Use the range of the latitude and longitude to build an appropriate bounding box for your map.


```r
lat <- c(33.89, 80.50)
long <- c(-157.84, -82.42)
wbox <- make_bbox(long, lat, f = 0.05)
```

8.  Load a map from `stamen` in a `terrain-lines` projection and display the map.


```r
wolfmap <- get_map(wbox, maptype = "terrain-lines", source = "stamen")
```

```
## Source : http://tile.stamen.com/terrain/4/0/0.png
```

```
## Source : http://tile.stamen.com/terrain/4/1/0.png
```

```
## Source : http://tile.stamen.com/terrain/4/2/0.png
```

```
## Source : http://tile.stamen.com/terrain/4/3/0.png
```

```
## Source : http://tile.stamen.com/terrain/4/4/0.png
```

```
## Source : http://tile.stamen.com/terrain/4/0/1.png
```

```
## Source : http://tile.stamen.com/terrain/4/1/1.png
```

```
## Source : http://tile.stamen.com/terrain/4/2/1.png
```

```
## Source : http://tile.stamen.com/terrain/4/3/1.png
```

```
## Source : http://tile.stamen.com/terrain/4/4/1.png
```

```
## Source : http://tile.stamen.com/terrain/4/0/2.png
```

```
## Source : http://tile.stamen.com/terrain/4/1/2.png
```

```
## Source : http://tile.stamen.com/terrain/4/2/2.png
```

```
## Source : http://tile.stamen.com/terrain/4/3/2.png
```

```
## Source : http://tile.stamen.com/terrain/4/4/2.png
```

```
## Source : http://tile.stamen.com/terrain/4/0/3.png
```

```
## Source : http://tile.stamen.com/terrain/4/1/3.png
```

```
## Source : http://tile.stamen.com/terrain/4/2/3.png
```

```
## Source : http://tile.stamen.com/terrain/4/3/3.png
```

```
## Source : http://tile.stamen.com/terrain/4/4/3.png
```

```
## Source : http://tile.stamen.com/terrain/4/0/4.png
```

```
## Source : http://tile.stamen.com/terrain/4/1/4.png
```

```
## Source : http://tile.stamen.com/terrain/4/2/4.png
```

```
## Source : http://tile.stamen.com/terrain/4/3/4.png
```

```
## Source : http://tile.stamen.com/terrain/4/4/4.png
```

```
## Source : http://tile.stamen.com/terrain/4/0/5.png
```

```
## Source : http://tile.stamen.com/terrain/4/1/5.png
```

```
## Source : http://tile.stamen.com/terrain/4/2/5.png
```

```
## Source : http://tile.stamen.com/terrain/4/3/5.png
```

```
## Source : http://tile.stamen.com/terrain/4/4/5.png
```

```
## Source : http://tile.stamen.com/terrain/4/0/6.png
```

```
## Source : http://tile.stamen.com/terrain/4/1/6.png
```

```
## Source : http://tile.stamen.com/terrain/4/2/6.png
```

```
## Source : http://tile.stamen.com/terrain/4/3/6.png
```

```
## Source : http://tile.stamen.com/terrain/4/4/6.png
```

```r
ggmap(wolfmap)
```

![](lab12_hw_files/figure-html/unnamed-chunk-11-1.png)<!-- -->

9. Build a final map that overlays the recorded observations of wolves in the lower 48 states.


```r
wolf2 %>% 
  select(lat, long) %>% 
  summary()
```

```
##       lat             long        
##  Min.   :33.89   Min.   :-151.06  
##  1st Qu.:44.60   1st Qu.:-117.05  
##  Median :46.83   Median :-110.99  
##  Mean   :50.08   Mean   :-114.69  
##  3rd Qu.:57.89   3rd Qu.:-110.55  
##  Max.   :80.50   Max.   : -82.42
```


```r
lat <- c(33.89, 80.50)
long <- c(-151.06, -82.42)
cbox <- make_bbox(long, lat, f = 0.05)
```


```r
wolf2map <- get_map(cbox, maptype = "terrain-lines", source = "stamen")
ggmap(wolf2map)
```

![](lab12_hw_files/figure-html/unnamed-chunk-14-1.png)<!-- -->


```r
ggmap(wolf2map) + 
  geom_point(data = wolf2, aes(long, lat, size=pop)) +
  labs(x= "Longitude", y= "Latitude", title="wolf population")
```

```
## Warning: Using size for a discrete variable is not advised.
```

![](lab12_hw_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

10. Use the map from #9 above, but add some aesthetics. Try to `fill` and `color` by population.


```r
ggmap(wolf2map) + 
  geom_point(data = wolf2, aes(long, lat, size=pop.density)) +
  labs(x= "Longitude", y= "Latitude", title="wolf population")
```

![](lab12_hw_files/figure-html/unnamed-chunk-16-1.png)<!-- -->


```r
ggmap(wolf2map) + 
  geom_point(data = wolf2, aes(long, lat, fill=pop.density)) +
  labs(x= "Longitude", y= "Latitude", title="wolf population")
```

![](lab12_hw_files/figure-html/unnamed-chunk-17-1.png)<!-- -->

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 

