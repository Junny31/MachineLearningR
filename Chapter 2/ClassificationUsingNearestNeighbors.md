### Classification using the nearest neighbor classifiers algorithm (a widely used classifier is k-NN -  k-nearest neighbors algorithm) makes use of the fact that things that are alike usually have similar properties.
### "If a concept is difficult to define, but you know it when you see it, then k-NN might be the best choice"
### In k-NN, the algorithm uses information about an example's k-nearest neighbors to classify unlabled examples. k can be ny number. The algorithm requires training dataset with examples that have been classified into several categories with nominal labels.
### For each unlabled record in the test dataset, k-NN identified k records in the training data that are the nearest in similarity. The unlabled test instances is assigned the class of the majority of the k nearest neighbors

### Exercise: Use k-NN algorithm to diagnose breast cancer
### Data: Wisconsin Breast Cancer Diagnostic data set (http://archive.ics.uci.edu/ml). Data is included in this chapter
### The data include 569 cancer biopsies - each with 32 features: Including patient identification, type of cancer diagnosis (benign or metastatic) and 30 numeric measurements for each biopsy.

breastCancer<-read.csv("wisc_bc_data.csv", stringsAsFactors = FALSE)

head(breastCancer) ### Get a sense of the different viables in the data set

str(breastCancer) ### Understand the structure of the data and types of viables in each feature

### the first variable is just patient identification number which does not provide any information for our porpuse. Let's exclude this column

breastCancer<-breastCancer[-1]

head(breastCancer) ### check to make sure that the column has been excluded

table(breastCancer$diagnosis) ### Determine how many biopsies are benign and how many are malignant
 
### Many machine learning classifiers R packages require that the target feature is coded as a factor. 

breastCancer$diagnosis<- factor(breastCancer$diagnosis, levels = c("B", "M"),
labels = c("Benign", "Malignant"))

###Normalization of the numeric data
### There are two commonly used: min-max normalization and z-score standardization; here, we will use the min-max normalization proceduce

normalize <- function(x) {
 return ((x - min(x)) / (max(x) - min(x))) ### normalization function
 }
 ### Test the normalization function on a vector y
 y1<-1:10
 z1<-c(2,10,300,9000,2000)
 normalize(y1) 
 normalize(z1) ### observe that all the normalized values fall betwen 0 and 1 irrespective of the original data. 
 
 ###We can now use the normalize() function on the numeric data to cancer data set
 
breastCancer_norm <- as.data.frame(lapply(breastCancer[2:31], normalize))

#### To confirm that the normalization was correcly carried out

summary(breastCancer_norm) ###All values (min and max values for each feature should be 0 and 1 respectively)


### Data preparation: training and test data set
### Split breastCancer_norm into training and testing datasets

### Out of the 569 cases, we will use 450 for the training dataset and the remaining 119 to test our "model"


BreastCancer_train <-BreastCancer_norm[1:450, ]

BreastCancer_test <-BreastCancer_norm[451:569, ]

BreastCancer_train_labels <- BreastCancer[1:450, 1]
 
BreastCancer_test_labels <- BreastCancer[451:569, 1]

###training on the data

install.packages("class")

library(class)

BreastCancer_test_pred <- knn(train = BreastCancer_train, test = BreastCancer_test,
 cl = BreastCancer_train_labels, k = 21) ### We use k =21, which is ~ the sqrt(450)
 
 
 ### Evaluation of our "model" performance
 
 ## We use the CrossTable() function which is part of the gmodels package. We already loaded this package in chapter 1
 
 CrossTable(x = BreastCancer_test_labels, y = BreastCancer_test_pred,
 prop.chisq=FALSE) ### Specifying chisq=FASLSE, since chi-square values from the output are not informative for our porpuse.
 
 ####Visit my blog ... for data intepretation
 
 
 ###There are a few ways to improve the k-nn model performance. (1) Use a different scaling method e.g. Z-scores standardization or (2) try several values for k
 
 ### R has a built function - scale() - which can be use to standardize a vector
 
 BreastCancer_Zscore<- as.data.frame(scale(BreastCancer[-1])) ### Rescale all the numeric features and store the data frame as BreastCancer_Zscore
 
summary(BreastCancer_Zscore) ### To confirm the transformation
 
 
 #### The mean is always zero and the range is fairly compact. Values that >3 or <-3 are indicative of extreme values
 
 
 ###Just like above, we seperate the data into testing and training datasets
 

BreastCancer_train <-BreastCancer_Zscore[1:450, ]

BreastCancer_test <-BreastCancer_Zscore[451:569, ]

BreastCancer_train_labels <- BreastCancer[1:450, 1]
 
BreastCancer_test_labels <- BreastCancer[451:569, 1]

 
 
 BreastCancer_test_pred <- knn(train = BreastCancer_train, test = BreastCancer_test,
 cl = BreastCancer_train_labels, k = 21)
 
 CrossTable(x = BreastCancer_test_labels, y = BreastCancer_test_pred,
 prop.chisq=FALSE) 
 
 
 
 
 
 


 










 
 
 
 
 
 
 
 

