Summary
This project applies machine learning techniques to predict the chart positions of Taylor Swift
songs using historical data. The dataset includes information about song features and their respective 
peak chart positions. By using both linear regression and random forest models, the project evaluates 
the predictive accuracy of these methods and applies the best-performing model to forecast chart 
positions for songs from a new album. After training the model on existing Taylor Swift data, the model's
machine learning performance was tested by how well it predicts peak billboard position for hypothetical
data for hypothetical Taylor Swift songs.


Folder Contents
swift-data.csv
  - This is the data that trained the linear and random forest models.

swift-new.csv
  - This is hypothetical data that the model has never seen and was asked to predict the peak billboard position of
  
Order of Script Use
1. ml-Taylor Swift.R
  -The ml-taylor-swift.R script is an end-to-end machine learning workflow for analyzing and predicting 
  the chart performance of Taylor Swift songs. The script is structured to load data, build machine learning 
  models, evaluate their performance, and generate predictions for a new album. Code to generate box plots to 
  compare the models visually is included in the code as well.
