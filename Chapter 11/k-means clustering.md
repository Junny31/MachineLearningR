# Finding teen market segments

### The dataset represent a random sample of 30,000 US high school students who had profiles on a social networking site in 2006
### This data was collected by Brett Lantz from the Sociology department @ Notre Dame
### The data is included in this chapter

## Get, explore and prepare data

sns_teens <- read.csv("snsdata.csv")

head(sns_teens)

str(sns_teens)

summary(sns_teens)

### The features include contain 4 personal variables and 36 variables indiciting the interests of the 30,000 teenagers

### There are NAs in the gender and age categories

table(sns_teens$gender, useNA = "ifany")

summary(sns_teens$age)

summary(sns_teens$gender)

### There are 9% and 17% records missing the gender and ages data.
### Another issue with this dataset is that the minimum and maximum ages are 3 and 106. It is very unlikely that someone this young or that old is attending high school.

### To address the outlierish ages, I will treat the ages that are not betwen 13 and 20 as missing values

sns_teens$age <- ifelse(sns_teens$age >= 13 & sns_teens$age < 20,
sns_teens$age, NA)

summary(sns_teens$age) ### The age range now looks reasonable

## Dealing with missing values

### Treating teenages with unknown gender as its category will be a good way to handle such a data

sns_teens$female <- ifelse(sns_teens$gender == "F" &
!is.na(sns_teens$gender), 1, 0)

sns_teens$no_gender <- ifelse(is.na(sns_teens$gender), 1, 0)

> table(sns_teens$gender, useNA = "ifany")

> table(sns_teens$female, useNA = "ifany")

> table(sns_teens$no_gender, useNA = "ifany")

## Handling the missing age values by imputation (Guess the ages of teenages with missing values)

### A realiably approximation of the student  age can be obtain by making use of the graduation date of the teenager

ave_age <- ave(sns.teens$age, sns.teens$gradyear, FUN =
function(x) mean(x, na.rm = TRUE))

sns.teens$age <- ifelse(is.na(sns.teens$age), ave_age, sns.teens$age)

summary(sns.teens$age)

## Training the model using the stats package in the default R program

### I will use the 36 features that represent the interest of the students for the cluster analysis

interests <- sns.teens[5:40]

### z-score normalization of the features

interests_z <- as.data.frame(lapply(interests, scale))

...





















