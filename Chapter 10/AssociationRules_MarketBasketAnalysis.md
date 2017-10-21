## Get, explore and prepare data


library(arules) 
setwd("C:/Users/Owner/Desktop/MachineLearningR_sampleData")
groceries <- read.transactions("groceries.csv", sep = ",")
head(groceries)
summary(groceries)

### The dataset is the Groceries dataset in the arules R package. 
### The groceries data contains 9,835 transactions and 169 groceries types. Transaction data are best handled in a sparse matrix. The read.transaction() function in the arules package can be used to create a sparse matrix for the groceries dataset

### The columns density is 0.0261 (2.6%). That is 2.6% is the proportion of nonzero matrix cells.By multiplying 9,835 & 169 we get 1,662,115  positions in the groceries matrix

### 2.6% of 1,662,115 is 43,367 (the total number of items purchase during the 30 days period when the data was collected)


## Examine the frequency of items in the groceries dataset

a<-sort(itemFrequency(groceries), decreasing = FALSE)
head(a)


## Graphical presentation of items that appear at least 5% of the time in the dataset

itemFrequencyPlot(groceries, support = 0.05)


## Visual inspection of the entire sparse matrix

(image(sample(groceries, 100)))

### The overall distribution of the sparse matrix looks fairly random. This is a good indication to progress to the next step (model training)


## Support and confidence threshols setting

### I will set our support threshold 0.006 (We want to include items that were purchased at least twice a day on average: i.e. 60 times in a month and 60/9835 = 0.006)

### I will start with a confidence threshold to 0.25 and optimize as needed 


groceryrules <- apriori(groceries, parameter = list(support =
0.006, confidence = 0.25, minlen = 2))


### This gives 463 rules 


## Model evaluation (how useful are the 463 rules?)

summary(groceryrules) 


### 150 rules have 2 items, 297 have  items 3, and 16 rules have 4 items


inspect(groceryrules[1:5])


### Depdending on the objectives, the most interesting rules might be the ones with the highest support, confidence or lift


inspect(sort(groceryrules, by = "lift")[1:10]) # To obtained the top 10 rules sorted by the lift statistic


## Interpretation of first and second rules:

### Compared to the typical customer, people that bought herbs or berries were ~4 times more likely to buy root veggies or whipped cream respectively.
