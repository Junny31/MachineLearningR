# MachineLearningR %% This exercise is based on the book: Machine Learning with R second edition by BRETT LANTZ
### To examine bivariate relationship, usually scatter plot is the method of choice
### For the attached usedcars.csv data, here are the codes to explore the scatterplot relationship between mileage and price of cars in the dataset


plot(x = usedcars$mileage, y = usedcars$price,
 main = "Scatterplot of Price vs. Mileage",
 xlab = "Used Car Odometer (mi.)",
 ylab = "Used Car Price ($)")
 
 #### To examine the relationship between 2 norminal variables, a 2-way cross-tabulation (AKA crosstab or contigency table)
 
 ### To determine if there is a relationship between car model and color in the usedcars.csv data set, we can use the crosstab method.
 ### The Crosstab method is included in the gmodels package (by Gregory Warners)
 
 install.packages("gmodels")
 
 library(gmodels) ## load the "gmodels" package
 
 ### There are 9 different colors in the dataset. We are interested in weather or not the car color is conservative
 ### conservative colors (conColor): Black, Gray, Silver and White
 ### not conservative colors (notConColor): Blue, Gold, Green, Red, and Yellow
  
 usedcars$conColor <-  usedcars$color %in% c("Black", "Gray", "Silver", "White") 
 ### A true or false statement, weather or not used car color is in the set of Black, Gray, Silver, and White
 
 > table(usedcars$conColor)
 
 ### this is give us something like 
 ### FALSE (51) TRUE (99)
 
 
 ### Let's determine if the proportion of conservatively colored cars varies by the model using crosstab method
 
 CrossTable(x = usedcars$model, y = usedcars$conservative)
 

 
 
 
 
 

