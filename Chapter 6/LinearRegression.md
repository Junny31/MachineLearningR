### Our goal is to predict the medical expenses of people enrolled in a medical insurance program in the USA
### Data is insurance.csv from the Packt Publishing group, also included in this chapter

### Get, explore and prepare data

insurance <- read.csv("insurance.csv", stringsAsFactors = TRUE)

head(table)

str(insurance)

summary(table)

### insurance.csv includes 1338 examples of beneficiary enrolled inthe insurance plan. 
### The features include "age" of the primary beneficialry, "sex" of the primary benficiary, "BMI" of primary beneficiary, number of children covered in the plan, smoker feature and geograp
### The dependent variable is "expenses"

hist(insurance$expenses)

### Look at the relationship (correlation) among the variables (including the dependent variable) in our dataset

cor(insurance[c("age", "bmi", "children", "expenses")])

### Create a scatterplot matrix to visulaize the relationship between variables

pairs(insurance[c("age", "bmi", "children", "expenses")])






