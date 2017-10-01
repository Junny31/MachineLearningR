# Predicting the strength of concrete from a given listing of the composition of the input materials

## The data is the concrete.csv data from http://archive.ics.uci.edu/ml

### The concrete dataset contains 1030 examples of concretes with 8 features describing the components used in the mixture

## Get, explore and prepare data

concrete <- read.csv("concrete.csv")

head(concrete)

str(concrete)

summary(concrete)

## We see that there are 9 variables in the dataset - 8 corresponding to the 8 independent variable and the dependent viable is the strength

## The values of the features range from 0 to > 1000. Neural networks perform best with the input are scaled to a narrow range around zero

### Feature normalization

normalize <- function(x) {
return((x - min(x)) / (max(x) - min(x)))
}

concrete_norm <- as.data.frame(lapply(concrete, normalize))

### Check that the normalization was applied to all features

summary(concrete_norm$strength)

## Split our data into training and testing sets

concrete_train <- concrete_norm[1:750, ]

concrete_test <- concrete_norm[751:1030, ]

## Model training
### We will use a multilayer feedforward neural network in the neuralnet package

install.packages("neuralnet")

library(neuralnet)

concrete_model <- neuralnet(strength ~ cement + slag
+ ash + water + superplastic + coarseagg + fineagg + age,
data = concrete_train)

## To visualize the network topology, we can use the plot() function

plot(concrete_model)

### We will see from the result that this is a simple model with one input node for each of the 8 features. All the 8 nodes fit into a single hidden node that predicts the concrerete strength

### Evaluation of model performance. We use the compute() to make predictions on the testing dataset

model_results <- compute(concrete_model, concrete_test[1:8])

model_results  

## The model_results has 2 components (1) $neurons - which stores the neurons for each layer in the network, and $net.result, which sores the predicted values.
### So to get strength prediction we use

predicted_strength <- model_results$net.result

### To determine the model accuracy, we measure the correlation between our predcited concrete strength and the true value

cor(predicted_strength, concrete_test$strength)

### Correlations close to 1 are indicative of strong linear relationships. Which will imply that our model is doing pretty well

## Improving the performance of our model

### Networks with more complex topologies are capable of learning more difficult concepts. Lets increase our number of hidden nodes from 1 to 5 (5 fold increase)


concrete_model2 <- neuralnet(strength ~ cement + slag +
ash + water + superplastic +
coarseagg + fineagg + age,
data = concrete_train, hidden = 5)

plot(concrete_model2)

model_results2 <- compute(concrete_model2, concrete_test[1:8])

predicted_strength2 <- model_results2$net.result

cor(predicted_strength2, concrete_test$strength)

### Compare the correlation value to what we had earlier














