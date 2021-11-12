# Python-and-R-Workrgroup---Task-2.2

# Objective:
Our purpose was to import a dataframe and through various techniques of manipulation and visualization, create graphs in order to simplify the visualization of the data in R. R is a free software environment for statistical computing and graphics.

#Info about the dataframe:
Magic: The Gathering, also Magic or MTG, is a strategy card game created by Richard Garfield in 1993, and published by Wizards of the Coast. Magic holds the title of "Most Played Trading Card Game".
To access the dataframe we used the following link: https://raw.githubusercontent.com/simonelugithub/API-project-/7eb17de80689dcbc6251c354d87aad6bb51ec6b0/MGT.csv
The dataframe we need to work on is a JSON file. The jsonlite package is a JSON parser/generator optimized for the web. Its main strength is that it implements a bidirectional mapping between JSON data and the most important R data types. Thereby we can convert between R objects and JSON without loss of type or information, and without the need for any manual data munging.

## Code explanation
Library is a statement to load a packages. We  load all the packages that we need with the command library() 

```r
library(tidyverse)
...
library(ggpubr)
```
We import the CSV dataframe from a GIT repository thanks to the function fromJSON used to convert JSON data in R objects.
```R
cards <- fromJSON("https://raw.githubusercontent.com/simonelugithub/API-project-/7eb17de80689dcbc6251c354d87aad6bb51ec6b0/MGT.csv")
```
For brevity sake we assign the name "df" to our dataframe and select the columns that interest us.
```
df <- as.data.frame(cards)
df <- df[c(1,3,4,7,8,9,11,13,15,16,29)]
```
we decide to create two new columns of variables. The new two columns contain: the average of each card representing the sum of power and toughness, and the ratio that is calculated as the relation between the ratio and the mana cost of evocation of each card.
```
df$cards.average <- as.numeric(df$cards.power)   +  as.numeric(df$cards.toughness)
df$cards.ratio <-  as.numeric(df$cards.average) / df$cards.cmc
```
We note that some columns contain null values named by the initials NA or special characters. We decide to omit those lines from our dataframe as they would complicate the graphic transposition.
```
filter(df, !(cards.power== c("NA","*","*")))
```
We create a new dataframe by selecting only the columns that contain the quantitative variables. Thanks to the use of the pipe operator the code is better readable. 
```
df_clean <- df %>% 
  select(cards.name,cards.cmc,cards.rarity,      cards.power:cards.ratio)%>%
  arrange(desc(cards.ratio))
```  
 Out of curiosity we want to see how many legendary cards are present in this dataframe
``` 
 Legendary.cards= filter(df, cards.supertypes == "Legendary")
```

# Code Explanation
The complete explanation of the code is available here: [Documentation]()
