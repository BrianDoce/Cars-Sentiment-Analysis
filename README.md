# Toyota and Honda Sentiment Analysis
This is a project I created using data I web scraped from Edmunds.com where I performed sentiment analysis on Toyota and Honda cars' reviews.

Author: Brian Docena

# Introduction
The website I received the data from was Edmunds.com, an online resource for automative information that provides enthusiasts with reviews, pricing, and comparison tools. In order to perform analysis on the data, I web scraped the website using Selenium and BeautifulSoup. The 
main goal for this project was to give me some insight on a hypothetical. If I were to buy
a car, what should it be? I chose to focus on Toyota and Honda cars because they are my 
favorite manufacturers as their cars makes me feel nostalgic.

df_toyota_details is a dataset about each model of Toyota cars, which 
contains 39 rows and the following columns:

| Column | Description |
| ----------- | ----------- |
| 'car_model' | The model of the car |
| 'price' | The cost of the car |
| 'average_rating' | The average rating of the model |

df_toyota_reviews has the information about each review for Toyota cars, which
contains 1110 rows and the following columns:

| Column | Description |
| ----------- | ----------- |
| 'car_model' | The model of the car |
| 'reviews' | User reviews |
| 'date' | The date the review was posted |
| 'user_rating' | The rating users gave on their review |
| 'helpful numerator' | How helpful the review was |
| 'helpful_denomindator' | Total amount interacted with review |

Similarly, df_honda_details is another subset of the data containing 20 rows and the following columns:

| Column | Description |
| ----------- | ----------- |
| 'car_model' | The model of the car |
| 'price' | The cost of the car |
| 'average_rating' | The average rating owners gave to the car |

df_honda_reviews has the information about each review for Honda cars containing 675 rows and
the following columns:

| Column | Description |
| ----------- | ----------- |
| 'car_model' | The model of the car |
| 'price' | The cost of the car |
| 'owner_rating' | The overall rating owners gave to the car |
| 'reviews' | User reviews |
| 'date' | The date the review was posted |
| 'user_rating' | The rating users gave on their review |
| 'helpful numerator' | How helpful the review was |
| 'helpful_denomindator' | Total amount interacted with review |

Given these datasets, I knew I wanted to merge them based on their corresponding car model, so
that I would eventually have two dataframes: one with Toyota cars and the other with Honda cars.
There was also some data cleaning to handle as some reviews were null and duplicated because 
if a car was the same model, but a different year, the reviews would be the same.

# Data Cleaning and Exploration
For data cleaning, I did the following steps:
1. I dropped the duplicated and null reviews from df_toyota_details and df_honda_details.
    - I wanted to perform sentiment analysis on the reviews, so having duplicated reviews
    or reviews that were null had no value for me. This led me to drop these rows.

2. I merged df_toyota_details and df_toyota_reviews on the car_model to create the df_toyota dataframe.

3. I merged df_honda_details and df_honda_reviews on the car_model to create the df_honda dataframe.

4. I concated the df_honda and df_toyota dataframe into one dataframe called df_cars to make 
it easier to clean the other columns.

5. I created a function to clean the price column from a string to a float.
    - Before the cleaning the data was in a format where the price included $ and ,. Having
    the data in this format is not useful because price represents a numeric value, not a string.

6.  I created a function to clean the average_rating column.
    - Similarly, the average_rating column was formatted as a string, so I thought it was best
    convert it into a numeric column.

7. I transformed the data column into DateTime, so that the column is more useful if I choose
to use it.

The final result is a dataframe with 1323 rows and 8 columns.
(Note: the following visualization is a portion of the columns)
![image of dataframe](image.png)

# Sentiment Analysis
For my project I used NLTK Vader to break down user reviews into positive, negative, and neutral values. Compound is a value on a scale from -1 (negative) to 1 (positive) that NLTK Vader assigns to a user's review. This value essentially determines whether a review is positive or negative. I also added a length of a review column as I thought it would be helpful to see the relationship between sentiment and review length or rating of a car model and the length of the review.

Here is a dataframe that demonstrates the statistics for each model within the dataset 
and their corresponding user's rating and their sentiment.

| car_model                           |   ('user_rating', 'mean') |   ('user_rating', 'max') |   ('user_rating', 'min') |   ('user_rating', 'std') |   ('user_rating', 'count') |   ('compound', 'mean') |   ('compound', 'max') |   ('compound', 'min') |
|:------------------------------------|--------------------------:|-------------------------:|-------------------------:|-------------------------:|---------------------------:|-----------------------:|----------------------:|----------------------:|
| 2025 Toyota GR Corolla              |                   4.875   |                        5 |                        4 |                 0.353553 |                          8 |               0.718562 |                0.9967 |               -0.2068 |
| 2024 Toyota Prius Prime             |                   4.83333 |                        5 |                        4 |                 0.389249 |                         12 |               0.517767 |                0.9992 |               -0.225  |
| 2025 Toyota Land Cruiser            |                   4.78571 |                        5 |                        3 |                 0.578934 |                         14 |               0.755557 |                0.9969 |                0      |
| 2024 Toyota Grand Highlander Hybrid |                   4.76471 |                        5 |                        3 |                 0.562296 |                         17 |               0.785335 |                0.9987 |                0.1027 |
| 2024 Toyota 4Runner                 |                   4.73469 |                        5 |                        1 |                 0.784631 |                         49 |               0.612676 |                0.9927 |               -0.9839 |

# TF-IDF
To go further in depth I wanted to run TF-IDF on user reviews. TF-IDF or Text Frequency Inverse Document Frequency is used to identify the most important words in a document across documents. By implementing this method, I thought it would give more insight on car models and what words
from reviews would best represent the car model.

After performing TF-IDF, this is what the first few rows looks like:
| car_model                     | most_important_word   |
|:------------------------------|:----------------------|
| 2025 Toyota Highlander Hybrid | choose                |
| 2025 Toyota Highlander Hybrid | ok                    |
| 2025 Toyota Highlander Hybrid | map                   |
| 2025 Toyota Highlander Hybrid | sluggish              |
| 2025 Toyota Highlander Hybrid | mpgs                  |

It looks messy having multiple rows of repeated car model and having a single word that best represents each review, so I created a function to combine all the most important words into a single list for each model.

Here is a few of the rows of the resulting dataframe:
![dataframe of important words for each car model.](image-1.png)

# Interesting Aggregates
For my aggregates, I decided to group by rating and get the median, max, and standard deviation for calories.
This allows me to see what type of values of calories each rating consists of. I chose not to include mean because 
I noticed that the max calories of each rating would not make mean a good indicator of the central value.

|   ('rating', '') |   ('calories (#)', 'median') |   ('calories (#)', 'max') |   ('calories (#)', 'std') |
|-----------------:|-----------------------------:|--------------------------:|--------------------------:|
|                1 |                        316   |                   17551.6 |                   757.481 |
|                2 |                        326.3 |                    7585   |                   526.058 |
|                3 |                        309.6 |                   13101.5 |                   547.385 |
|                4 |                        302   |                   16894.9 |                   487.187 |
|                5 |                        298.2 |                   45609   |                   580.018 |

# Assessment of Missingness
## NMAR Analysis
In my dataframe, the three columns that have a significant amount of missing values are description, rating, and review. I believe that the missingness of review is NMAR because the probability of the data being missing is tied 
to the value itself as people who experience positive or negative feelings with the recipe are more likely to 
write a review.

## Missingness Dependency
I wanted to see if the missingness of ratings depended on calories 

Null Hypothesis: The missingness of rating does not depend on calories.

Alternate Hypothesis: The missingness of rating does depend on calories.

Test Statistic: Absolute difference of average calories

Level of Signficance: 0.05

I ran a permutation test by shuffling the calories 500 times and each time I collected the absolute difference in the average calories of the groups: missing ratings and not missing ratings.

<iframe
  src="assets/calories-missing.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

I calculated an observed statistic of 68.98 and a p-value of 0.0, which is less than the level of significance of 
0.05. This means that we reject the null hypothesis and it suggests that the missingness of rating does depend on calories.

# Hypothesis Testing
I conducted my hypothesis testing based on whether people rated low caloric recipes (recipes less than 500 calories) higher than high caloric recipes.

Null Hypothesis: The rating of high caloric recipes and low caloric recipes have the same distribution.

Alternate Hypothesis: The rating of low caloric recipes is greater than the rating of high caloric recipes.

Test Statistic: Difference in mean rating between low caloric and high caloric recipes

Level of Significance: 0.05

When conducting the hypothesis test, I used a permutation test because I wanted to see if the ratings of high caloric recipes and low caloric recipes were rated the same. I was curious on whether low caloric recipes would 
receive a higher average rating than high caloric recipes.

To perform my hypothesis test, I shuffled the rating 500 times and calculated the difference in the average rating 
of low caloric recipes and high caloric recipes each time. I then calculated the observed difference, which was 
0.017. This tells me that low caloric recipes in my sample were rated slightly higher than high caloric recipes. When I found the p_value, the value was 0.0. This causes us to reject the null hypothesis.

<iframe
  src="assets/highcalories-test.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


# Framing a Prediction Problem
For my prediction problem, I wanted to use regression to predict the amount of calories a recipe would have.
I chose to predict the amount of calories because calories are essential for people who have certain dietary needs 
or personal fitness goals they want to achieve.

Since I planned on using regression, I chose to use root mean squared error to evaluate my model because I thought 
it was more interpretable in the context of my problem as I can tell the average error my predicted calories was 
to the actual calories. My other option was using R^2^, but I felt like knowing the quality of my prediction line 
wasn't as meaningful.

At the time of the prediction, we wouldn't have access to the nutritional values. We would only have access to 
information about the recipe such as the number of steps, minutes take to prepare, etc.

# Baseline Model
For my baseline model, I used a linear regression model that uses three features: is_dessert (nominal), is_dietary (nominal), and minutes (quantitative). is_dessert and is_dietary are both nominal columns extracted from the tags column, which consists of 
True and False values. For my model I used one hot encoding for these columns and used the standardized version 
of minutes.

For testing of my model, I split my sample into training and testing sets. With this method, I calculated a 
root mean squared error of 586 for my training set and 568 for my testing set. I believe this model is terrible 
because for each recipe, its prediction is more than 500 calories away.

# Final Model
For my final model, I added several columns: average_rating, is_vegetarian, n_ingredients, and meal_time

## n_ingredients
I added n_ingredients because as I was doing bivariate analysis, I grouped n_ingredients and aggregated on calories and saw that at some point as the number of steps increased, the median calories was consistently high. I thought 
that this could be useful to predict calories.

## is_vegetarian
For this column I extracted if recipes had vegetarian within its tags. Recipes were given the values True or False, which I then one hot encoded. I believed that this feature would improve my model because recipes labeled with vegetarian should have lower calories compared to ones that aren't.

## meal_time
For this column I extracted if the tags had breakfast, dinner, etc. within it and made it into a column so I could
use one hot encoding within it. I believed this feature would improve 

The modeling algorithm I chose was Lasso with hyperparameters of alpha = 100 and fit_intercept = True as it performed slightly better on the testing set. To find the best hyperparameters, I used GridSearchCV with a 
5-fold cross-validation to find the best alpha and fit_intercept parameters.

## Results
My final model performed slightly better than my baseline model with my final model having a root mean squared error 
of 558.74 on the testing set compared to my baseline model's root mean squared error of 565.26. My final thoughts about my model was that it was extremely difficult trying to improve my linear regression model to predict 
calories. I believe that a linear regression model was too simple to predict calories, which led to high bias and 
high root mean squared error.

# Fairness Analysis
For my fairness analysis, I wanted to evaluate my model's root mean squared error parity. To do this, I wanted to 
see if it predicted both high caloric recipes and low caloric recipes the same. 

Null Hypothesis: The model is fair. Its RMSE for high caloric recipes and low caloric recipes are roughly the same.

Alternative Hypothesis: The model is unfair. Its RMSE for high caloric recipes is not the same for low caloric recipes.

Test Statistic: The absolute difference in Root mean Squared Error for the two groups

Significance Level: 0.05 

p-value: 0.00

Conclusion: For my fairness analysis, I observed a p value of 0.00, which causes me to reject the null hypothesis.

<iframe
  src="assets/fairness-dist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>











