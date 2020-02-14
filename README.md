# boston_dataset

GA is a public company traded in Stock exchange. The CEO of GA wants to invest in the real estate properties in the Boston area. He gave me a dataset containing housing values in the suburbs of Boston in the file Boston.csv.

__Boston.csv file__
![Boston Dataset](https://i.imgur.com/kNX5S5v.png)

__I am asked to perform the following tasks by writing a script in R.__

1. Read the dataset in Boston.csv. Preview the document into R. Call the loaded data Boston. Make sure that you have the directory set to the correct location for the data.
  ```{r}
Boston <- read.csv("Boston.csv")
```
2. How many rows are in the data frame? How many columns? What do the rows and columns represent?
```{r}
head(Boston)
```
3. Select the 1st, 100th, and 500th rows with columns tax and medv.
```{r}
Boston[c(1, 100, 500),c("tax", "medv")]
```
4. Look at the data using cor function. Are any of the predictors associated with per capita crime rate? If so, explain the relationship based on correlation coefficents.
```{r}
cor(Boston)
```
5. Make some pairwise scatterplots of the predictors, crim, rad, tax, indus, and lstat in this data set. Describe your findings.
```{r}
pairs(Boston[,c("crim", "rad", "tax", "indus", "lstat")])
```
![Pairwise Scatterplots](https://i.imgur.com/sQ6l5Qn.png)
6. Do any of the suburbs of Boston appear to have particularly high crime rates by looking at the histogram of crim? What is the range of crim by using range() function in R?
```{r}
hist(Boston[,c("crim")],
     main="Crime Rates",
     xlab="Crime rates in different suburbs",
     col="red"
     )
```
![Crime Rates](https://i.imgur.com/bjV5I9B.png)

#6.1 Range of crim
```{r}
range(Boston[,c("crim")])
```
7. How many of the suburbs in this dataset bound the Charles River?
```{r}
library(dplyr) #Addint dplyr library for filtering data.

Boston %>%
  select(chas) %>%
  filter(chas == 1) %>% # (1 if tract bounds river; 0 otherwise)
  count(chas) #35 Suburbs are bound to the Charles River
```
8. What is the median pupil-teach ratio among the towns in this dataset? What’s the mean?
```{r}
median(Boston$ptratio) #The median is 19.05 among the towns
```
9. In this dataset, how many of the suburbs average more than seven rooms per dwelling? More than eight rooms per dwelling? Comment on the suburbs that average more than eight rooms per dwelling.
```{r}
Boston %>%
  select(rm) %>%
  filter(rm > 7) %>% 
  count(rm) #62 suburbs has more than seven rooms per dwelling.
```

#9.1.More than eight rooms per dwelling?
```{r}
Boston %>%
  select(rm) %>%
  filter(rm > 8) %>% 
  count(rm) #13 suburbs has more than seven rooms per dwelling.
```
10. Convert chas to a factor. Boxplot the medv against chas. Are houses around the Charles River more expensive?
```
boxplot(Boston$medv~y, data=ToothGrowth, notch=FALSE,
  main="Price for Houses around the Charles River", xlab="0 - Not Charles River | 1 - Charles River", ylab="Median value of owner-occupied homes in $1000's")
```
![Boxplot](https://i.imgur.com/5QDAjKb.png)
