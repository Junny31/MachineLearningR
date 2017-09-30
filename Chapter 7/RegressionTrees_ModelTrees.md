### Task: Use regression trees and model trees to create a system capable of mimicking expact ratings of wine.
### We will identify key factors that contribute to better-rated wines.

### Data is whitewines.csv from http://archive.ics.uci.edu/ml. This data include examples of both red and white wines from Vinho Verde wines from Portugal

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
