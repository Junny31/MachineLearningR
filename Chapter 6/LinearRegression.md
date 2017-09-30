### Our goal is to predict the medical expenses of people enrolled in a medical insurance program in the USA
### Data is insurance.csv from the Packt Publishing group, also included in this chapter

### Get, explore and prepare data

insurance <- read.csv("insurance.csv", stringsAsFactors = TRUE)

head(insurance)

str(insurance)

summary(insurance)

### insurance.csv includes 1338 examples of beneficiary enrolled inthe insurance plan. 
### The features include "age" of the primary beneficialry, "sex" of the primary benficiary, "BMI" of primary beneficiary, number of children covered in the plan, smoker feature and geograp
### The dependent variable is "expenses"

hist(insurance$expenses)

### Look at the relationship (correlation) among the variables (including the dependent variable) in our dataset

cor(insurance[c("age", "bmi", "children", "expenses")])

### Create a scatterplot matrix to visulaize the relationship between variables

pairs(insurance[c("age", "bmi", "children", "expenses")])


### The pairs.panel() from the psych package produces a more informative plot

install.packages("psych")

library(psych)

insurance_model <- lm(expenses ~ age + children + bmi + sex +
smoker + region, data = insurance)

summary(insurance_model)

### Improving the performance of our model
### Its is important to have some basic understanding on how certain independent features in your dataset can affect the dependent variable. For example, it is possible that the relationship between age and expenses might not be a linear function. Medical expenses may become disproportionaly more expensive for oldest population. To increase the effect of age on our model, we might square the age variable.

insurance$age2 <- insurance$age^2 ### We create a new variable "age2" with values that are two fold the age values

### Also, some variable might need to get to a certain threshold for them to have an effect on the dependent variable. BMI for example: BMI =< 30 are considered healthy while BMI > 30 might have an effect on medical expenses

insurance$bmi30 <- ifelse(insurance$bmi >= 30, 1, 0)

### Some features might also have a combine impact on the dependent variable. It is possible that BMI and smoking can in combination have an effect on medical expenses. We can use bmi30*smoker to instruct R to model any adding interaction between bmi and smoking status on medical expenses

insurance_model2 <- lm(expenses ~ age + age2 + children + bmi + sex +
bmi30*smoker + region, data = insurance)

summary(insurance_model2)









