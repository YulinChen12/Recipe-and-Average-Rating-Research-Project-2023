# Recipe-and-Average-Rating-Research-Project-2023

By Yulin Chen & Jiarui Zha  

Nov 2023

## Introduction of the Project

The project delves into the fascinating intersection of culinary art and data analysis. We aim to unearth patterns and insights that are not immediately apparent. Specifically, we focuses on understanding **how the number of ingredients in a recipe might influence its users' ratings** and **We defined the recipe with number of ingredients greater than or equal to 15 as *Complex Recipe* and recipe with number of ingredients less than 15 ingredients as *Simple Recipe*.**

Understanding the relationship between the number of ingredients in a recipe and its ratings is crucial for various reasons. It reveals consumer preferences, indicating whether simplicity or complexity is more valued in cooking. This insight is vital for chefs, recipe developers, and the food industry, as it guides recipe creation and menu planning, potentially influencing customer satisfaction and business success. Additionally, it offers home cooks guidance on popular recipe choices and can inform culinary education. For the health-conscious, it may also highlight trends in nutritional choices. Essentially, this analysis bridges culinary art with consumer behavior, enhancing our understanding of food preferences.

We collected our data from food.com, a renowned online platform that offers a vast collection of user-contributed recipes. This website has become a go-to resource for both amateur and professional cooks seeking culinary inspiration, recipe instructions, and nutritional information. The significance of sourcing data from food.com lies in its large user base and the diversity of recipes it hosts, which reflect a wide array of culinary tastes and preferences.

The data from food.com has divided into two seprated datasets: food_recipe and user_interactions. The food_recipe dataset contains 83782 rows,meaning we have 83782 unique recipes. Some relevant columns to our projects are *recipe name*, *recipe id*, *ingredients*, and *number of ingredients*. The user_interactions dataset contains 731927 rows,meaning we have 731927 reviews from the users. Some relevant columns to our projects are *recipe id* and *rating*. 

After collecting the data,we noticed that both dataset contains the recipe id. Before investigate our project,we choose to merge the food_recipe and the user_interactions dataset by *recipe id*. In order to better correspond and find recipes, we use recipe id as the index.

The merged dataframe is shown below(with some relevant columns display).

|     id | name                                 | ingredients                                                                                                                                                                    |   n_ingredients |   rating |
|-------:|:-------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|---------:|
| 333281 | 1 brownies in the world    best ever | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] |               9 |        4 |
| 453467 | 1 in canada chocolate chip cookies   | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                    |              11 |        5 |
| 306168 | 412 broccoli casserole               | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |        5 |


## Cleaning and EDA

The first step in starting our project is to do some data cleaning to ensure that the data in each relevant column is reasonable and accurate.

> 0 Star Rating

We noticed that some of the recipes have 0 star rating. We believe that the reason for 0 star rating is not because the user gave this recipe 0 star rating, but because the user ignored the rating. A rating of 0 will lower the average rating of each recipe.

|     id | name                                       | ingredients                                                                                                                                                                                                                                                                                                                                                              |   n_ingredients |   rating |
|-------:|:-------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|---------:|
| 501028 | 50 chili   for the crockpot                | ['stewing beef', 'stewing pork', 'white onion', 'bell peppers', 'habanero pepper', 'garlic', 'beans', 'chunky salsa', 'tomato paste', 'beef broth', 'tortilla chips', 'chicken bouillon cube', 'beef bouillon cube', 'sazon goya', 'cinnamon', 'mexican chili powder', 'cumin', 'ground coriander', 'black pepper', 'salt', 'light brown sugar', 'dark chocolate chips'] |              22 |        0 |
| 455351 | lplermagronen                              | ['potato', 'penne pasta', 'onions', 'butter', 'cheese', 'milk', 'salt and pepper', 'applesauce']                                                                                                                                                                                                                                                                         |               8 |        0 |
| 523359 | der wiener schnitzel style chili dog sauce | ['ground beef', 'ground pork', 'water', 'cornstarch', 'wondra flour', 'tomato paste', 'chili powder', 'paprika', 'white vinegar', 'salt', 'dried onion flakes', 'granulated sugar', 'garlic powder', 'ground black pepper']                                                                                                                                              |              14 |        0 |
| 275675 | she crab  cream of crab soup               | ['cream of mushroom soup', 'cream of celery soup', 'half-and-half', 'milk', 'sherry wine', 'crabmeat', 'red pepper', 'salt', 'pepper', 'old bay seasoning']                                                                                                                                                                                                              |              10 |        0 |
| 275675 | she crab  cream of crab soup               | ['cream of mushroom soup', 'cream of celery soup', 'half-and-half', 'milk', 'sherry wine', 'crabmeat', 'red pepper', 'salt', 'pepper', 'old bay seasoning']                                                                                                                                                                                                              |              10 |        0 |

So the first step in our data clean is to replace the 0 star rating of each recipe with NaN, in order to calculate the correct average rating of each recipe. Then replace the NaN (0 Star Rating) with the average rating.

> Average Star Rating

After replace 0 with average star rating, we have add a new column of average_rating for each recipe for futher research purpose.

The Data Frame after our cleaning purpose is shown below(with only relevant columns display)

|     id | name                                 | ingredients                                                                                                                                                                    |   n_ingredients |   average_rating |
|-------:|:-------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-----------------:|
| 333281 | 1 brownies in the world    best ever | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour'] |               9 |                4 |
| 453467 | 1 in canada chocolate chip cookies   | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                    |              11 |                5 |
| 306168 | 412 broccoli casserole               | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']          |               9 |                5 |

## Exploratory Data Analysis
### Univariate Analysis

For the univariate analysis step, we analyze the distribution of number of ingredients and the distribution of number of average ratings.


<iframe src="assets/n_ingred.html" width=800 height=600 frameBorder=0></iframe>
Distribution Shape: The distribution of recipes across the number of ingredients appears to be unimodal, with a peak around the 7 to 10 ingredient range. This suggests that most recipes contain this number of ingredients.

Skewness: There is a right skew to the distribution, as the bars (bins) to the right of the peak (towards a higher number of ingredients) are smaller but extend further out, indicating that there are fewer recipes with a large number of ingredients.

Outliers: There are very few recipes with a very high number of ingredients (near 30 to 35), as indicated by the single bars at the far right of the histogram.

<iframe src="assets/average_rating.html" width=800 height=600 frameBorder=0></iframe>
The bottom of the box represents the first quartile (Q1), which is 4.5 in this case. This means that 25% of the ratings falls below this value.
The band inside the box is the median (the second quartile, Q2), which is 4.85. This is the midpoint of the all average rating.
The top of the box represents the third quartile (Q3), which is 5. Therefore, 75% of the rating is below this value, and 25% is above it.

Data Distribution: Given that Q3 is at the maximum of the rating scale (5), and the median is very close to the maximum (4.85), the data is left-skewed, indicating that most ratings are high, and very few are low (as also indicated by the outliers).

Overall Rating Quality: The concentration of the box at the high end of the rating scale implies that the average ratings are generally very good.

## Bivariate Analysis 
Then, we will perform bivariate analysis between the complex and simple recipes 