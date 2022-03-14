---
title: "Lab 2 Homework"
author: "Please Add Your Name Here"
date: "2022-03-14"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

1. What is a vector in R?  
the data set

2. What is a data matrix in R?  
vectors stacked onto each other

3. Below are data collected by three scientists (Jill, Steve, Susan in order) measuring temperatures of eight hot springs. Run this code chunk to create the vectors.  

```r
spring_1 <- c(36.25, 35.40, 35.30)
spring_2 <- c(35.15, 35.35, 33.35)
spring_3 <- c(30.70, 29.65, 29.20)
spring_4 <- c(39.70, 40.05, 38.65)
spring_5 <- c(31.85, 31.40, 29.30)
spring_6 <- c(30.20, 30.65, 29.75)
spring_7 <- c(32.90, 32.50, 32.80)
spring_8 <- c(36.80, 36.45, 33.15)
```

4. Build a data matrix that has the springs as rows and the columns as scientists.  


```r
temp1 <- c(spring_1, spring_2, spring_3, spring_4, spring_5, spring_6, spring_7, spring_8)
temp1
```

```
##  [1] 36.25 35.40 35.30 35.15 35.35 33.35 30.70 29.65 29.20 39.70 40.05 38.65
## [13] 31.85 31.40 29.30 30.20 30.65 29.75 32.90 32.50 32.80 36.80 36.45 33.15
```

```r
temperature <- matrix(temp1, nrow=8, byrow=T)
temperature
```

```
##       [,1]  [,2]  [,3]
## [1,] 36.25 35.40 35.30
## [2,] 35.15 35.35 33.35
## [3,] 30.70 29.65 29.20
## [4,] 39.70 40.05 38.65
## [5,] 31.85 31.40 29.30
## [6,] 30.20 30.65 29.75
## [7,] 32.90 32.50 32.80
## [8,] 36.80 36.45 33.15
```


```r
titles <- c("jill", "steve", "susan")
titles
```

```
## [1] "jill"  "steve" "susan"
```

```r
regions <- c("spring_1", "spring_2", "spring_3", "spring_4", "spring_5", "spring_6", "spring_7", "spring_8")
regions
```

```
## [1] "spring_1" "spring_2" "spring_3" "spring_4" "spring_5" "spring_6" "spring_7"
## [8] "spring_8"
```

```r
colnames(temperature) <- titles
rownames(temperature) <- regions
temperature
```

```
##           jill steve susan
## spring_1 36.25 35.40 35.30
## spring_2 35.15 35.35 33.35
## spring_3 30.70 29.65 29.20
## spring_4 39.70 40.05 38.65
## spring_5 31.85 31.40 29.30
## spring_6 30.20 30.65 29.75
## spring_7 32.90 32.50 32.80
## spring_8 36.80 36.45 33.15
```

5. The names of the springs are 1.Bluebell Spring, 2.Opal Spring, 3.Riverside Spring, 4.Too Hot Spring, 5.Mystery Spring, 6.Emerald Spring, 7.Black Spring, 8.Pearl Spring. Name the rows and columns in the data matrix. Start by making two new vectors with the names, then use `colnames()` and `rownames()` to name the columns and rows.


```r
spring_names <- c("Bluebell Spring", "Opal Spring", "Riverside Spring", "Too Hot Spring", "Mystery Spring", "Emerald Spring", "Black Spring", "Pearl Spring")
spring_names 
```

```
## [1] "Bluebell Spring"  "Opal Spring"      "Riverside Spring" "Too Hot Spring"  
## [5] "Mystery Spring"   "Emerald Spring"   "Black Spring"     "Pearl Spring"
```

```r
Spring_day <- cbind (spring_names, temperature) 
Spring_day
```

```
##          spring_names       jill    steve   susan  
## spring_1 "Bluebell Spring"  "36.25" "35.4"  "35.3" 
## spring_2 "Opal Spring"      "35.15" "35.35" "33.35"
## spring_3 "Riverside Spring" "30.7"  "29.65" "29.2" 
## spring_4 "Too Hot Spring"   "39.7"  "40.05" "38.65"
## spring_5 "Mystery Spring"   "31.85" "31.4"  "29.3" 
## spring_6 "Emerald Spring"   "30.2"  "30.65" "29.75"
## spring_7 "Black Spring"     "32.9"  "32.5"  "32.8" 
## spring_8 "Pearl Spring"     "36.8"  "36.45" "33.15"
```

6. Calculate the mean temperature of all eight springs.

```r
average_of_spring <- c("average", mean(spring_1), mean(spring_2), mean(spring_3), mean(spring_4), mean(spring_5), mean(spring_6), mean(spring_7), mean(spring_8))
average_of_spring
```

```
## [1] "average"          "35.65"            "34.6166666666667" "29.85"           
## [5] "39.4666666666667" "30.85"            "30.2"             "32.7333333333333"
## [9] "35.4666666666667"
```

```r
average_of_spring_n <- c(mean(spring_1), mean(spring_2), mean(spring_3), mean(spring_4), mean(spring_5), mean(spring_6), mean(spring_7), mean(spring_8))
average_of_spring_n                        
```

```
## [1] 35.65000 34.61667 29.85000 39.46667 30.85000 30.20000 32.73333 35.46667
```
7. Add this as a new column in the data matrix.  


```r
Spring_data <- cbind(Spring_day , average_of_spring)
```

```
## Warning in cbind(Spring_day, average_of_spring): number of rows of result is not
## a multiple of vector length (arg 2)
```

```r
Spring_data
```

```
##          spring_names       jill    steve   susan   average_of_spring 
## spring_1 "Bluebell Spring"  "36.25" "35.4"  "35.3"  "average"         
## spring_2 "Opal Spring"      "35.15" "35.35" "33.35" "35.65"           
## spring_3 "Riverside Spring" "30.7"  "29.65" "29.2"  "34.6166666666667"
## spring_4 "Too Hot Spring"   "39.7"  "40.05" "38.65" "29.85"           
## spring_5 "Mystery Spring"   "31.85" "31.4"  "29.3"  "39.4666666666667"
## spring_6 "Emerald Spring"   "30.2"  "30.65" "29.75" "30.85"           
## spring_7 "Black Spring"     "32.9"  "32.5"  "32.8"  "30.2"            
## spring_8 "Pearl Spring"     "36.8"  "36.45" "33.15" "32.7333333333333"
```

8. Show Susan's value for Opal Spring only.


```r
Spring_data[2,4]
```

```
## [1] "33.35"
```

9. Calculate the mean for Jill's column only.  


```r
mean(temperature[ ,1])
```

```
## [1] 34.19375
```

10. Use the data matrix to perform one calculation or operation of your interest.


```r
mean(average_of_spring_n)
```

```
## [1] 33.60417
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.  
