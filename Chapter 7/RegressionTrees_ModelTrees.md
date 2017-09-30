### Task: Use regression trees and model trees to create a system capable of mimicking expact ratings of wine.
### We will identify key factors that contribute to better-rated wines.

### Data is whitewines.csv from http://archive.ics.uci.edu/ml. This data include examples of both white wines from Vinho Verde wines from Portugal

### Get, explore and prepare data

wines <- read.csv("whitewines.csv")

head(wines)

str(wines)

### This data includes features on 11 chemical properties of 4,898 wine samples. 
### The samples were rated by blind tasting panelist on a qualitative scale from 0 (very bad) to 10 (Excellent)

hist(wines$quality)

### Model training

## Split data into training and testing data

wines_train <- wines[1:3500, ]
wines_test <- wines[3501:4898, ]

# REGRESSION TREE MODEL
## We will use the rpart package

install.packages("rpart")

library(rpart)

wines.rpart <- rpart(quality ~ ., data = wine_train)

wines.rpart

summary(wines.rpart)


## Decision tree visualization using the rpart.plot package

install.packages("rpart.plot")

library(rpart.plot)

rpart.plot(wines.rpart, digits = 3)

### Evaluation of model performance

pred_wines.rpart <- predict(wines.rpart, wines_test)

summary(pred_wines.rpart)














