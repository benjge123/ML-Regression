# Machine learning on Taylor Swift songs
# Ben Ge
# benjaminge@arizona.edu
# 2024-11-05

library(randomForest)
library(dplyr)

# Read in data 
swift_data <- read.csv("data/swift-data.csv")
# Show first six rows
head(swift_data)

# Run a linear model with all predictors
#                     Y ~ X1 + X2 + X3. The "." allowed you to use the rest of data to predict Y
linear_model <- lm(peak_position ~ ., data = swift_data)
# Run a random forest model with all predictors
randomforest_model <- randomForest(peak_position ~., data = swift_data)

# Predict song's peak position based on linear model
linear_prediction <- predict(linear_model, newdata = swift_data)
# Predict song's peak position based on rand forest model
rf_prediction <- predict(randomforest_model, newdata = swift_data)

# Calculate squared errors for linear model
linear_sqerr <- (swift_data$peak_position - linear_prediction)^2
# Calculate Root Mean Square Error(rsme) for linear model
linear_rsme <- sqrt(mean(linear_sqerr))
# Calculate squared error for random forest model
rf_sqerr <- (swift_data$peak_position - rf_prediction)^2
#Calculate Root Mean Square Error(rsme) for random forest model
rf_rsme <- sqrt(mean(rf_sqerr))

# Prints variable values. RF has a lower rsme, making it a better model
linear_rsme
rf_rsme

# Create fold vector. Creates a set of numbers that lets us assign every row to a bucket
fold <- rep_len(x = 1:5, length.out = nrow(swift_data))

#this stuff isn't printing :(

linear_rsme <- numeric(5)
rf_rsme <- numeric(5)
# for loop that accomplishes the comments below
for (i in 1:5) {
  # Split data in training/testing
  training <- swift_data %>%
    filter(fold != i)
  testing <- swift_data %>%
    filter(fold == i)
  
  # Estimate model with training data
  linear_model <- lm(peak_position ~ ., data = training)
  randomforest_model <- randomForest(peak_position ~., data = training)
  
  # Make predictions on testing data
  linear_prediction <- predict(linear_model, newdata = testing)
  randomforest_prediction <- predict(randomforest_model, newdata = testing)
  
  # Calculate rmse values
  linear_sqerr <- (testing$peak_position - linear_prediction)^2
  linear_rsme[i] <- sqrt(mean(linear_sqerr))
  
  rf_sqerr <- (testing$peak_position - randomforest_prediction)^2
  rf_rsme[i] <- sqrt(mean(rf_sqerr))
}
# Boxplot comparing performance of linear model to random forest model
boxplot(x = linear_rsme, rf_rsme,
  names = c("Linear Model", "Random Forest"),
  ylab = "RMSE")

# Estimate random forest model again, this time using all data
full_model <- randomForest(peak_position ~ ., data = swift_data)

# Load song data for new album
new_album <- read.csv(file = "data/swift-new.csv")

# Predict chart position for each of the songs on the new album
new_predict <- predict(full_model, newdata = new_album)

# Data frame holding predictions and track name
song_predict <- data.frame(track_num = 1:12,
                           peak_position = new_predict,
                           track_name = new_album$track_names)

# Print predicted chart positions for new album
song_predict

