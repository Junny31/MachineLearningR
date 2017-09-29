### Rules also uses the C5.0() function like decision tree in chapter 4, but we have to specify rules = TRUE
### Task: Identify rules for distinguihing poisonous mushrooms

### Data containing varieties of mushroom and their associated feature was obtained from  http://archive.ics.uci.edu/ml and included in this chpater mushroom.csv

### Get, explore and prepare data

mushrooms <- read.csv("mushrooms.csv", stringsAsFactors = TRUE)

head(mushrooms)

str(mushrooms) ### Note that veil_type only has has one level. It codes were probably entered incorrectly since the data code book mentions that there veil_type is either partial or universal. Since in our data set, the vel_type is the same in all examples, it doesnot provide any useful information

mushrooms$veil_type <- NULL ###We eliminate the veil_type feature from our data

table(mushroom$type) ### Get a sense of the proportion of poisonous mushroom in our dataset

### In this excericse, we are not trying to train our model to predict the poisoness of some unforeseen mushroom in the future. Our goal is to identify features that can distinguish poisonous mushrooms from their nonpoisonous counterpart. We will use all the muchroom examples to train our model

### Train our model on the data

###Let's use the 1R classifier to train our data: we are looking for a single predictive feature that can distinguish poisonous from non-poisonous mushroom. 1R classifier can be performed using the OneR() function in the RWeka package.

install.packages('RWeka') ### This package requires Java - make sure Java is install on your machine

library(RWeka)

mushroom_oneR <- OneR(type ~ ., data = mushrooms)

mushroom_oneR 

summary(mushroom_oneR)












