# Use of market basket analysis to identfy combinations of items that are often purchased together

## Get, explore and prepare data

### The dataset is the groceries dataset in the arules R package. This dataset is included in this chapter

### The groceries data contains 9,835 transactions and 169 groceries types

## A sparse matrix structure to handle this kind of data.The read.transaction() in in the arules package generates a matix suitable for transactional data
### Transaction data are best handled in a sparse matrix. The arules package can be used to create a sparse matrix for the groceries transaction data

install.packages("arules")

library(arules) 

groceries <- read.transactions("groceries.csv", sep = ",")

head(groceries)

summary(groceries)

### According the summary output, the columns density is 0.0261 (2.6%)
### 2.6% is the proportion of nonzero matrix cells. There are 1,662,115 (9,835*169) positions in the groceries matrix
### The total number of items purchase is 43,367 (1,662,115*0.0261) during the 30 days period when the data was collected

#### Examine the frequency of items in the groceries dataset

itemFrequency(groceries)

## Graphical presentation of items that appear at least 5% of the time in the dataset

itemFrequencyPlot(groceries, support = 0.05)

### Visual inspection of the entire sparse matrix

image(groceries) ### For very large datasets, we could look at just a sample of the data using (image(sample(groceries, 100))

### If the overall distribution of the dots in the figure looks fairly random, then it is a good indication to progress to the next step of training your model

### We will set our support threshold 0.006 (We want to include items that were purchased at least twice a day on average: i.e. 60 times in a month and 60/9835 = 0.006)
### Initially, we will set our confidence threshold to 0.25. This will eliminate a majority of the unreliable results while leaving room for optimzation 

groceryrules <- apriori(groceries, parameter = list(support =
0.006, confidence = 0.25, minlen = 2))

groceryrules ### This gives 463. 

## Evaluation of our model - how useful are the 463 rules obtained from this model?

summary(groceryrules) ### 150 rules have 2 items, 297 have  items 3, and 16 rules have 4 items

inspect(groceryrules[1:5])

## Improving the performance of the model

### Depdending on the objectives, the most interesting rules might be the ones with the highest support, confidence or lift

inspect(sort(groceryrules, by = "lift")[1:10]) ### To obtained the top 10 rules sorted by the lift statistic
























