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

### It is best remove numbers, punctuation and less informative words such and, but, and, or ...
### The tm package created by Ingo Feinerer can use for this purpose.

install.packages("tm")

library(tm)

###Create a corpus for SMS messages
### We use the VCorpus() function in the tm package.

sms_spam_corpus <- VCorpus(VectorSource(sms_spam$text))

print(sms_spam_corpus) ### You would see that sms_spam_corpus contain all the 5559 document

###To view sample messages

as.character(sms_spam_corpus[[1]]) 

lapply(sms_spam_corpus[1:2], as.character)

sms_spam_corpus_clean <- tm_map(sms_spma_corpus,
 content_transformer(tolower)) ### This standardize the messages to use only lowercases
 
 ###Confirmation that the previous line of code did its job
 
 as.character(sms_spam_corpus[[1]]) ### This should contain both upper and lowercases
 
 as.character(sms_spam_corpus_clean[[1]]) ### This should contain just lowercases
 
 ### Remove all the numbers from the messages
 
 sms_spam_corpus_clean <- tm_map(sms_spam_corpus_clean, removeNumbers)
 
 ### Remove less informative words such as the, to , but, and, or, is ... from the messages
 
 
 sms_spam_corpus_clean <- tm_map(sms_spam_corpus_clean,
 removeWords, stopwords())
 
 
 ###Remove punctuations
 
 sms_spam_corpus_clean <- tm_map(sms_spam_corpus_clean,
 removePunctuation)
 
 ###stemming: reduce words to their root form. Package is SnowballC
 
 install.packages("SnowballC")
  library(SnowballC)
  
  sms_spam_corpus_clean <- tm_map(sms_spam_corpus_clean, stemDocument)
  
  ###Remove additional whitespaces
  
  sms_spam_corpus_clean <- tm_map(sms_spam_corpus_clean, stripWhitespace)
  
  ### Check messages before and after cleaning
  
  as.character(sms_spam_corpus[1:3]) ### before cleaning
  
  as.character(sms_spam_corpus_clean[1:3]) ### After cleaning
  
  
  

  
  
  
  
  
  
  
 
 
 
 
 
 
 
 


 
 
 









print(sms_spam_corpus) ### We would see that 






