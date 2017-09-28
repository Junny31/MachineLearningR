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
  
  ### Data preparation: splitting text documents into words (AKA tokenization)
  
  ### DocumentTermMatrix() function will take a corpus and create a Docmunet Term Matrix where the rows represent SMS messages and the columns are the words in the SMS: This function is present in the tm package that we installed earlier
  
  
  sms_spam_dtm <- DocumentTermMatrix(sms_spam_corpus_clean)
  
  
  ### All the data cleaning and preparation steps can be performed with a single chunck of code
  
  
  
 sms_spam_dtm2 <- DocumentTermMatrix(sms_corpus, control = list(
   tolower = TRUE,
   removeNumbers = TRUE,
   stopwords = TRUE,
   removePunctuation = TRUE,
   stemming = TRUE
   )
 )
 
 ### Creating training and test datasets
 
  sms_spam_dtm_train <- sms_spam_dtm[1:4500, ]
  
  sms_spam_dtm_test <- sms_spam_dtm[4500:5559, ]
  
 ### Labels for the rows in the training and testing datasets.  Labels are not stored in the DTM data frame, so we get them from the original sms.spam data frame
 
 sms_spam_train_labels <- sms_spam[1:4500, ]$type
 sms_spam_test_labels <- sms_spam[4500:5559, ]$type
  
  ###Visualizing text data using word clouds. This can be done using the wordcloud package
  
  install.packages("wordcloud")
  
  library(wordcloud)
  
   wordcloud(sms_spam_corpus_clean, min.freq = 50, random.order = FALSE)
   
    spam <- subset(sms_spam, type == "spam")
    ham <- subset(sms_raw, type == "ham")
    
    wordcloud(spam$text, max.words = 40, random.order = FALSE)
    
    wordcloud(ham$text, max.words = 40, random.order = FALSE)
    
###The last step in the data prep is to transform sparse matrix into a data structure that we can use to train a Naive Bayes classifier
    
###Let's eliminate any word that occurs in less than 5 (0.1%) SMS messages. We use the FinFreqTerms() function in the tm package

sms_spam_freq_words <- findFreqTerms(sms_spam_dtm_train, 5) ###The function returns a character vector containing words that appear at least 5 times

sms_spam_req_train <- sms_spam_dtm_train[ , sms_spam_freq_words]

sms_spam_req_test <- sms_spam_dtm_test[ , sms_spam_freq_words]
 


    
    
    
  
  
  
  
  
  
 
 
   
  
  

  
  
  
  
  
  
  
 
 
 
 
 
 
 
 


 
 
 









print(sms_spam_corpus) ### We would see that 






