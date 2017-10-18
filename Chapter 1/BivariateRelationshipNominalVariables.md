# Determine the relationship between 2 Nominal variables

## Get Data

setwd("C:/Users/Owner/Desktop/MachineLearningR_sampleData")
used_cars <- read.csv("usedcars.csv", stringsAsFactors = TRUE)
head(used_cars)
summary(used_cars)


### There are 9 different colors in the dataset. We are interested in weather or not the car color is conservative
### conservative colors (conColor): Black, Gray, Silver and White
### not conservative colors (notConColor): Blue, Gold, Green, Red, and Yellow


used_cars$conColor <-  used_cars$color %in% c("Black", "Gray", "Silver", "White")

table(used_cars$conColor)

## Determine whether or not used car color is in the set of Black, Gray, Silver, and White

 
### this is give us

### FALSE (51) TRUE (99)
 
 
## Proportion of conservatively colored cars varies by the model using crosstab method
 
library(gmodels)
CrossTable(x = used_cars$model, y = used_cars$conColor)


### - 65% of the SE cars are coloerd conservatively
### - 70% of the SEL cars are colored conservatively
### - 65% of the SES cars are colored conservatively

### There is no difference in the types of colors chosen by the model of the car. 
  
