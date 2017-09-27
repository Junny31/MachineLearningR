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


