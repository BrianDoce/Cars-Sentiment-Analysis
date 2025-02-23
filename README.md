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

The final result is a dataframe with 234428 rows and 25 columns.
(Note: the following visualization is a portion of the columns)

| car_model                     |   price |   average_rating | reviews                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | date                |   user_rating |   helpful_numerator |   helpful_denominator |
|:------------------------------|--------:|-----------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------|--------------:|--------------------:|----------------------:|
| 2025 Toyota Highlander Hybrid |   48086 |              4.3 | The Honda Odyssey with 200,000 miles in 9 years was a really good car. When the time came, I had to choose a new car, and I decided to buy a hybrid car. The reason for this is that the fuel efficiency is good, the engine operates only when necessary, so there is little noise, and as a result, the life of various parts is long, and I liked the fact that the brakes last a long time through regenerative braking. However, Honda didn't have much choice of hybrid vehicles, so I chose Toyota's vehicle, which is the strongest in hybrid technology. | 2023-04-05 00:00:00 |             5 |                  14 |                    15 |
|                               |         |                  | I chose the Highlander as it is a vehicle that I often drive for work, is good for riding with my family, can carry a lot of luggage, and does not have any problems on snowy roads and mountain roads in winter.                                                                                                                                                                                                                                                                                                                                                 |                     |               |                     |                       |
|                               |         |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                     |               |                     |                       |
|                               |         |                  | The results were beyond expectations.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |                     |               |                     |                       |
|                               |         |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                     |               |                     |                       |
|                               |         |                  | I'm amazed that a vehicle this large can get 40 mpg when driven on fuel economy. And the interior design, functions such as wireless Android Auto, spacious interior space, and quiet driving really give me new pleasure every day.                                                                                                                                                                                                                                                                                                                              |                     |               |                     |                       |
|                               |         |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                     |               |                     |                       |
|                               |         |                  | I don't have much interest in cars and I don't enjoy driving much, so even if I buy a new car, I feel good for a while at first because it's a new car, but I think it's the first time I've ever enjoyed driving like this.                                                                                                                                                                                                                                                                                                                                      |                     |               |                     |                       |
|                               |         |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                     |               |                     |                       |
|                               |         |                  | I don't change cars often. So, through a lot of research, I choose a car that I can ride without problems for a long time, and I am sure that the Toyota Highlander is exactly what I wanted.                                                                                                                                                                                                                                                                                                                                                                     |                     |               |                     |                       |
|                               |         |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                     |               |                     |                       |
|                               |         |                  | Thank you Toyota                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |                     |               |                     |                       |
| 2025 Toyota Highlander Hybrid |   48086 |              4.3 | We purchased the 2023 Highlander Platinum AWD Hybrid.  The gas mileage started at 28MPG.  This is a far cry from EPA ratings but understand there are variables that come into play.  That being said, I am now up to 32.6 so it is improving but question if it will ever get better since I have been stuck on this mileage for a while now.                                                                                                                                                                                                                    | 2023-07-10 00:00:00 |             2 |                  26 |                    31 |
|                               |         |                  | The heated seats are weak at best in the winter as are the fan cooled seats in the summer.  Very disappointing.                                                                                                                                                                                                                                                                                                                                                                                                                                                   |                     |               |                     |                       |
|                               |         |                  | The premium sound system is also a disappointment.  Just not the dynamic system I expected for Highlander.                                                                                                                                                                                                                                                                                                                                                                                                                                                        |                     |               |                     |                       |
|                               |         |                  | The seating is OK but for the money we paid, I should have waited for the new Lexus.  A much better value, much more comfortable and a much better vehicle in general.                                                                                                                                                                                                                                                                                                                                                                                            |                     |               |                     |                       |
|                               |         |                  | I do not recommend this vehicle as a value.  We were just too quick to purchase and recommend others to shop around a bit as this is a very crowded category of vehicle.                                                                                                                                                                                                                                                                                                                                                                                          |                     |               |                     |                       |
|                               |         |                  | By the way, did I mention I am still waiting for my second ignition key 8 months after I purchased the car.  Chip shortage was the excuse.  OK, I can be patient but 8 months?  That is ridiculous.                                                                                                                                                                                                                                                                                                                                                               |                     |               |                     |                       |
|                               |         |                  | Keep looking including the Lexus Hybrid which is priced around the same.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |                     |               |                     |                       |
| 2025 Toyota Highlander Hybrid |   48086 |              4.3 | First Toyota.  It is noisy (wind and road noise), tinny and...Unless you subscribe (after one year) to their connected service...every time you get in the car..a MARKETING Screen pops up and says Experience Drive Connect.  You CANNOT (I confirmed with Toyota Customer Service) get to the Toyota map (gee...I paid for that nav system and that large screen).  You have to use Apple Car Play.  I’d just like to see the map...I don’t need live traffic...Complete rip off...and I am shocked Toyota does this. Mine is a Limited Hybrid                  | 2024-05-07 00:00:00 |             3 |                   8 |                     9 |
| 2025 Toyota Highlander Hybrid |   48086 |              4.3 | Great vehicle in every way but engine being sluggish.  The partnership with BMW on interior seats and finish is comfortable and luxurioius.  The underperformance of acceleration with the 4 cyliner non turbo just isn't enough power.  The 6 cylinder was better.                                                                                                                                                                                                                                                                                               | 2023-11-06 00:00:00 |             3 |                  16 |                    20 |
| 2025 Toyota Highlander Hybrid |   48086 |              4.3 | Love everything about this vehicle.  Purchased it in December 2023.  Beautiful blizzard pearl paint with special black wheels and trim accents.  Acceleration and MPGs are both great.  I get 36-40 MPGs depending on the driving conditions.  Very quiet inside and the engine is also really quiet even when accelerating.  It also has a really tight turning radius for such a large vehicle.  We have no kids living with us, so the 3-row is not a factor.                                                                                                  | 2024-03-01 00:00:00 |             5 |                   4 |                     4 |
# Univariate Analysis
For my univariate analysis, I wanted to see the distribution of calories to get a better understanding
of the values within the column. From the visualization, we can see that the distribution is skewed right 
and that most of the calories fall within the 250 - 750 range.

<iframe
  src="assets/dist-calories.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

# Bivariate Analysis
For my bivariate analysis, I wanted to see what proportion of high caloric recipes and low caloric recipes were
in each rating. From the visualization, we can see that the proportion of high caloric recipes in the 1 - 3 rating 
range are slightly greater than low caloric recipes.

<iframe
  src="assets/calories-rating.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

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











