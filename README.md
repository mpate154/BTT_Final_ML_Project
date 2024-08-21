# BTT_Final_ML_Project
**A Multiple Linear Regression Model using World Happiness Report Data Set to predict a feature called 'Freedom to make life choices'**

As a part of Cornell University's Break Thru Tech program, I explored an "The World Happiness record" dataset using libraries such as Sci-Kit learn, Numpy, Pandas, Keras, and TensorFlow on Jupyter notebook to train multiple supervised models that best fit to predict the feature "Freedom to make life choices". After testing different models, I ended up with a multiple linear regression model. 

**A detailed summary of my choices and explanations are included in the notebook, but I will explain below as well. I recommend reading these notes for a clearer understanding. Because I repeatedly changed my plan, the notes in the notebook are scattered and may not be relevant to the model I ended up choosing.** 

------
## Contents
- ### [Problem Statement/ Real World Application] (problem-statement/-real-world-application)
- ### [Data Cleaning Summary](data-cleaning-summary)
  - #### [Dealing with Missing Data](dealing-with-missing-data)
  - #### [Other Data Cleaning](other-data-cleaning)
- ### [Evaluation](evaluation)
- ### [Challenges, Insights Gained and Future Improvements](challenges,-insights-gained-and-future-improvements)
  - #### [Challenges](challenges)
  - #### [Insights Gained](insights-gained)
  - #### [Future Improvements](future-improvements)
-----
    

## Problem Statement/ Real World Application  
Looking into the amount of freedom there is in choices can give different companies perspectives on the market and lifestyle of a place. For example, a high amount of freedom can mean there are more opportunities for companies to compete for advertising and selling their products AKA an open market, as the people have more choice in deciding what they want to buy. They can use this as an optic to see if they'll have successful profits. This can be another option for a food product, different types of education (private, charter, catholic, vocational), etc. If a companies goal to offer more freedom in a way that's either literal (non-profit for a cause) or more abstract (create options in a market), they can use this label to see a current standing.

## Data Cleaning Summary
### Dealing with Missing Data 
I used three approaches when dealing with missing data in feature columns. If the feature column has less than 5% of the data missing, I used the mean per country for each specific column to fill in the missing values. This was done by country to reduce bias. If the feature had between 5-20% of it's data missing, I used a **KNN imputer** to fill in the missing data. For those with more than 20% data missing, I removed the column entirely.

- Columns to replace with mean by each country(<5% missing):
  - Log GDP, Social Support, Life Expectancy, Freedom to make choices, Generosity, Corruption, Positive, Negative

- KNN imputation (5-20% missing):
  - Confidence, Democratic qualily, Delivery quality, GINI index average 2000-15

- Remove column (>20% missing):
  - GINI index (World Bank Estimate)
  - gini of household income reported in Gallup, by wp5-year
 
### Other Data Cleaning
Remove column due to data type:
- country (object)

## Evaluation 
I used Root Mean Squared Error (RMSE) and R-squared (R^2 / coefficient of determination) to evaluate my model's results. 

## Challenges, Insights Gained and Future Improvements
### Challenges
- A big challenge I faced was picking the right model, though is it natural to test different models to see which works best for your situation. I initially tried a Feedforward Neural Network, though no matter how much regularization and drop layers I added, the model tended to overfit the data. A key indicator of this was that the training loss was consistently higher than the validation loss. I figured the dataset was too small for such a complex model and tried a simpler one: a decision tree. The training score for mean square was consistently 0, another sign of overfitting. Lastly, I decided to try a linear regression model using the column with the most correlation to the label. The results weren't too bad so I then went to a multiple linear regression model. *Code for attempts at these previous models is included at the end of the notebook.* 
  
### Insights Gained
- Because of the various types of modeling used, I have a better understanding of the structures, strengths, weaknesses, and complexities of the different machine learning models.
- You cannot use a neural network on small datasets because of massive overfitting that may not be fixable by regularization and dropping. Because of these prevention tactics, I actually ended up with validation losses less than my testing losses when trying to train a FNN with this small dataset. Even 'unindexing' the data by country didn't work.
- KNN's need to have cross validation to see if they are working properly.
There are different ways to handle missing data and it depends on how much is missing, where its missing (sometimes, in this cases whole countries with missing data made it hard to fill in), and how much that column correlates with the label. You can fill it with the means of that column or a subset of it, perform KNN imputation, or get rid a column entirely.
- What kind of model you choose may seem arbitrary at first and almost overwhelming because of the options of approaches you can take, but if you properly inspect your data, pick your label, and see what data can be used and the shape of it, it becomes more apparent which options are the best for your data.
- Some machine learning models require scaling such as FNN while decision trees do not.

### Future Improvements
- Use cross validation to improve my KNN imputer
- Train a more complex model using this data without overfitting and better predictive accuracy

