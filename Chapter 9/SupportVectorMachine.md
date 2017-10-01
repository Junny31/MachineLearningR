# Use SVM to match hand written english letters to typed letters A to Z

## Get, explore and prepare data

### The data is the letterdata from http://archive.ics.uci.edu/ml 
### The dataset contains 20,000 examples of the 26 English alphabet capital letters that are printed using 20 different randomly reshaped and distorted black and white fonts

letters <- read.csv("letterdata.csv")

head(letters)

str(letters

summary(letters)

### For SVM learners, the features are suppose to be numeric and each feature is scaled to a fairly small interval

### from the summary output above, we can see that all the features are numeric, however, the ranges of the integer vairiable are fairly wide. Some R packages can automatically rescale the data.

### Split the data into the training and testing set

letters_train <- letters[1:17000, ]

letters_test <- letters[17001:20000, ]

## Training a model on the data, using the linear kernel function

### We will use the kernlab package

 install.packages("kernlab")
 
library(kernlab)

letter_classifier <- ksvm(letter ~ ., data = letters_train,
kernel = "vanilladot")


letter_classifier


## Evaluation of model performance

letter_predictions <- predict(letter_classifier, letters_test)

head(letter_predictions)

table(letter_predictions, letters_test$letter) ### This gives us an easy to understand matrix. That tells us the ratio of true yto false prediction for each letter. We can even simply this information with the following code

agreement <- letter_predictions == letters_test$letter

table(agreement)

## Improving the performance of our model

### We can improve the performance of our model by using a more kernel function to map the data into a higher dimensional space
### The popular convention is to begin with the Gaussian RBF kernel

letter_classifier_rbf <- ksvm(letter ~ ., data = letters_train,
kernel = "rbfdot")

### Prediction

letter_predictions_rbf <- predict(letter_classifier_rbf,
letters_test)

agreement_rbf <- letter_predictions_rbf == letters_test$letter
table(agreement_rbf)

prop.table(table(agreement_rbf))
















