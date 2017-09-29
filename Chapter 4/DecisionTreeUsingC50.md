###Decision trees are widely use in the banking industry to predict risky loans

### In this example we will predict loans that have a higher risk of default using information on loans obtain a German credit agency  (http://archive.ics.uci.edu/ml). This data is included in this chapter credit.csv

#### Get data

loans <- read.csv("credit.csv")

###Explore data

head(loans)

str(loans)

#### Lets explore some of the features that might be important predictors of loan default status

table(loans$checking_balance)

table(loans$savings_balance)

###Note that the customers checking and saving account balance are categorical variables


summary(loans$months_loan_duration)

summary(loans$amount)

###The loan duration and amount of loan requested are numeric variables

summary(loans$default)

###A total of 30% of the loan went into default

###Data Preparation

### Creating training and test datasets (85% of the data for training and 15 for the testing dataset)

set.seed(1)

train_sample <- sample(1000, 850)


loans_train <- loans[train_sample, ]
loans_test <- credit[-train_sample, ]

### If our randomization was good we should have 30% of default loans in both the training and testing datasets

prop.table(table(loans_train$default))

prop.table(table(loans_test$default))

### We will use the C5.0 algorithm to train our model

install.packages("C50")

library(C50)

?C5.0

loansDefault_model <- C5.0(loans_train[-17], loans_train$default) ## The 17th column is the default class variable

###Examine the desicion tree stored in loansDefault_model

loansDefault_model

summary(loansDefault_model)

### Evaluating model performance: Apply the model to our test dataset

loan_pred <- predict(loansDefault_model, credit_test)

### The preceding code generates a vector of predicted values which we can compare to the actual values using the CrossTable() function which we install as part of the gmodels package in chaper 2.

CrossTable(loans_test$default, credit_pred,
prop.chisq = FALSE, prop.c = FALSE, prop.r = FALSE,
dnn = c('actual default', 'predicted default'))

####Improving C5.0 performance: (1) Boosting - using the trial parameter in C5.0(), we will try the widely used 10 trials


loans_boost10 <- C5.0(loans_train[-17], loans_train$default,
trials = 10)


loans_boost10

summary(loans_boost10)









