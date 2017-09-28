### Bayesian classification is best for problems in which the we need the information from numerous features to estimate the overall probability of an outcome.

###Strength: Many ML algprithms ignore features that have weak effects, Naives Bayes uses all available evidence. Many features with minor contribution can combine to have a larger effects.

### Data is SMS Spam from  http://www.dt.fee.unicamp.br/~tiago/smsspamcollection/. Also attached to this chapter

### Get, explore and prepare the data

sms_spam <- read.csv("sms_spam.csv", stringsAsFactors = FALSE)

head(sms_spam)

str(sms_spam)

###From the out of str(sms_spam) you will see that the "type" element is a character vector. We convert it to a factor

sms_spam$type <- factor(sms_spam$type)

###confirmation of the conversion

str(sms_spam$type)

table(sms_raw$type)


#### Cleaning and standardizing text data



