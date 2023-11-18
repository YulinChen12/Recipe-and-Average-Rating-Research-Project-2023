# Recipe-and-Average-Rating-Research-Project-2023

By Yulin Chen & Jiarui Zha  

Nov 2023

## Introduction of the Project

The project delves into the fascinating intersection of culinary art and data analysis. We aim to unearth patterns and insights that are not immediately apparent. Specifically, we focuses on understanding **how the number of ingredients in a recipe might influence its users' ratings** 

More specifically **Do people tend to give more star rating for the complex recipe than the simple recipe?**

We defined the recipe with number of ingredients greater than 15 as **Complex Recipe** and recipe with number of ingredients less than or equal to 15 as **Simple Recipe**.

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

> Category 

We also add a new column of classify each recipe into simple or complex based on their number of ingredients, to further analyze our problem.


The Data Frame after our cleaning purpose is shown below(with only relevant columns display)

|     id | name                                         | ingredients                                                                                                                                                                                                                                                                                                                                               |   n_ingredients |   average_rating | Category   |
|-------:|:---------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-----------------:|:-----------|
| 486161 | zydeco soup                                  | ['celery', 'onion', 'green sweet pepper', 'garlic cloves', 'olive oil', 'cooked ham', 'paprika', 'sugar', 'dry mustard', 'ground cumin', 'dried basil', 'dried oregano', 'dried thyme', 'ground cloves', 'black pepper', 'cayenne pepper', 'black-eyed peas', 'yellow hominy', 'diced tomatoes', 'low sodium chicken broth', 'fresh parsley', 'molasses'] |              22 |                5 | Complex    |
| 493372 | zydeco spice mix                             | ['paprika', 'salt', 'garlic powder', 'onion powder', 'dried basil', 'dried oregano', 'dried tarragon', 'dried thyme', 'powdered sugar', 'black pepper', 'cayenne pepper', 'red pepper flakes', 'celery seed']                                                                                                                                             |              13 |                5 | Simple     |
| 308080 | zydeco ya ya deviled eggs                    | ['hard-cooked eggs', 'mayonnaise', 'dijon mustard', 'salt-free cajun seasoning', 'tabasco sauce', 'salt', 'black pepper', 'fresh italian parsley']                                                                                                                                                                                                        |               8 |                5 | Simple     |
| 298512 | cookies by design   cookies on a stick       | ['butter', 'eagle brand condensed milk', 'light brown sugar', 'sour cream', 'egg', 'extract', 'nutmeg', 'self-rising flour', 'bisquick', 'wooden popsicle sticks']                                                                                                                                                                                        |              10 |                1 | Simple     |
| 298509 | cookies by design   sugar shortbread cookies | ['granulated sugar', 'shortening', 'eggs', 'flour', 'cream of tartar', 'baking soda', 'vanilla extract']                                                                                                                                                                                                                                                  |               7 |                3 | Simple     |

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

<iframe src="assets/compare.html" width=800 height=600 frameBorder=0></iframe>

While the median ratings for simple and complex recipes are identical, the distribution of the ratings is not the same. Complex recipes show greater variability in ratings with more lower outliers, whereas simple recipes show a tighter clustering of ratings around the median with fewer outliers. This could suggest that while both types of recipes can achieve a median level of satisfaction, simple recipes tend to do so more consistently, whereas complex recipes have a greater risk of receiving lower ratings.




## Interesting Aggregates

| Category   |   minutes |   n_steps |   average_rating |
|:-----------|----------:|----------:|-----------------:|
| Complex    |   147.846 |  16.6411  |          4.6436  |
| Simple     |   112.866 |   9.67429 |          4.62417 |

The table quantifies the complexity of recipes in terms of time and effort (number of steps). This suggests that complex recipes take more time and more steps to complete than simple recipes.

 One interesting connection we have found is that users might rate recipes not just on the outcome but also based on their experience of cooking the meal. A complex recipe, as indicated by more minutes and steps, might be rated higher if the users enjoy the challenge or the result, or it might be rated lower if they find it too cumbersome.

 In relation to our hypothesis about the number of ingredients affecting ratings, this table suggests there are additional layers of complexity beyond just the number of ingredients. This makes us understand more about the relationship between recipe complexity (as measured by time, steps, and ingredient count) and user ratings by multiple predictors of ratings.

 ## Assessment of Missingness

 After the data cleaning and analysis step, we will conduct the assessment of missingness in this part.

 ### NMAR Analysis

 The column average_rating appears to be Not Missing At Random (NMAR), suggesting that the absence of data within this column may not be coincidental or uniformly distributed, but rather could be indicative of a pattern pertaining to the response variable itself. It is plausible to hypothesize that a lack of ratings could correlate with a negative reception of the recipe. That is, if consumers are dissatisfied or indifferent towards a recipe, they may be less inclined to leave a rating, thereby leading to missing values in the average_rating column.

### Missingness Dependency Analysis
Furthermore, the columns name, description, and average_rating are identified as having missing entries. This observation warrants a more nuanced approach to data analysis, as the missingness in average_rating is potentially informative and could be a factor of underlying attitudes or preferences which influence the decision to not provide a rating.

> Number of Ingredients and Descriptions

In our investigation into the relationship between the completeness of recipe descriptions and the number of ingredients, we employed permutation testing to determine the statistical significance of our observations.

Null hypothesis: **The number of ingredients is NOT dependent on the presence of recipe descriptions**

Alternative Hypothesis: **The number of ingredients IS dependent on the presence of recipe descriptions**

<iframe src="assets/average_des.html" width=800 height=600 frameBorder=0></iframe>

The analysis involved creating two visual histograms: the first for recipes lacking descriptions, which showed a roughly uniform distribution across the number of ingredients, and the second for recipes with descriptions, which exhibited a right-skewed distribution, where a majority of recipes had fewer ingredients.

To test our hypothesis rigorously, we conducted a permutation test with 100 iterations. This non-parametric test allowed us to assess the null hypothesis of independence between the two variables without making assumptions about the distribution of our data.

The permutation test yielded a **p-value of 0.002**. This result is well below the standard alpha threshold of 0.05, leading us to reject the null hypothesis and accept the alternative hypothesis. 

In conclusion, our permutation-based analysis provides robust evidence that the likelihood of a recipe description being omitted is not a matter of chance but indicates there is a statistical association between them, however, it does not imply causation between these two variables.

> Minutes of the Recipe and Descriptions

In our analysis focusing on the relationship between the duration of recipe preparation (denoted in minutes) and the presence of recipe descriptions, we utilized permutation testing to ascertain the statistical significance of our findings.

Null hypothesis: **The preparation time (minutes) is NOT dependent on the presence of recipe descriptions**.

Alternative Hypothesis: **The preparation time (minutes) IS dependent on the presence of recipe descriptions**.

<iframe src="assets/mins_des.html" width=800 height=600 frameBorder=0></iframe>

The investigation featured the creation of two histograms for visual data representation. The first histogram depicted the distribution of preparation times for recipes without descriptions, which did not display any particular pattern and appeared relatively flat. Conversely, the second histogram for recipes with descriptions also did not suggest a distinctive distribution, and also appeared relatively flat

We applied a permutation test with 100 permutations to rigorously evaluate the null hypothesis of no dependency between preparation time and the presence of a description.

The outcome of the permutation test was a **p-value of 0.596**. Given that this value exceeds the conventional alpha level of 0.05, we do not reject the null hypothesis. This leads us to conclude that, based on our sample data, there is no statistically significant evidence to suggest a dependency between the preparation time of a recipe and the existence of a recipe description.

## Hypothesis Testing

Finally,we go back to our rearch question: **Do people tend to give more star rating for the complex recipe than the simple recipe?**

In order to answer that, we will conduct a permutation test.

### Setting Up
Null Hypothesis: People are rating the complex ingredients recipe and simple ingreditents recipe in the same scale. Any observed association in the sample data is due to random chance.

Alternative Hypothesis: People are giving complex ingredients recipe a higher rating. The observed association is not due to random chance.

For The only relevant columns are average_rating,n_ingredients and Category:

|     id |   average_rating |   n_ingredients | Category   |
|-------:|-----------------:|----------------:|:-----------|
| 333281 |                4 |               9 | Simple     |
| 453467 |                5 |              11 | Simple     |
| 306168 |                5 |               9 | Simple     |
| 286009 |                5 |               7 | Simple     |
| 475785 |                5 |              13 | Simple     |

Since the average_rating is numerical,we calculated the observed statistic, which is the difference in average ratings between complex and simple recipes in the data

| Category   |   average_rating |   n_ingredients |
|:-----------|-----------------:|----------------:|
| Complex    |          4.643604  |        18.0498  |
| Simple     |          4.624172|         8.63113 |

Our observed statistic is (4.64 - 4.62417) = **0.01943221486512492**

### Permutation Test 

The permutation test involved 1000 iterations, shuffling the label of the Catrgory and calculating the difference in average ratings between the newly designated 'complex' and 'simple' groups for each iteration.

<iframe src="assets/permutation.html" width=800 height=600 frameBorder=0></iframe>

The histogram shows the distribution of the difference in mean ratings obtained from 1000 permutation iterations. These permutations simulate the distribution of differences we might expect to see by chance when there is no actual effect.

The position of the observed statistic, marked by the red line, indicates that the observed difference in mean ratings is greater than most of the differences obtained by chance through permutation. This suggests that the observed effect is not common in the null distribution.

### Test Result and Conclusion

We obtained a **p-value of 0.011**. Given that this p-value is below the conventional significance threshold of 0.05, we reject the null hypothesis. This suggests that the higher ratings associated with complex recipes in our sample data are unlikely to be due to random chance.

The result could be reasonable by several reasons:

Consumer Preferences: The study suggests that users may have a preference for recipes that are deemed more complex. This could indicate a desire for more sophisticated or varied cuisine, which users may perceive as higher quality or more exciting culinary experiences, and thus rate them more favorably.

Perceived Value: Complex recipes often involve a variety of ingredients which can create a perception of greater value, both in terms of flavor and nutritional benefits. Users may reward this perceived value with higher ratings.

Skill Demonstration: Home cooks and culinary enthusiasts may derive satisfaction from successfully completing more challenging recipes. Thus, the complexity of the recipe could be linked to the satisfaction of the user, leading to higher ratings.

Engagement: Complex recipes may lead to higher engagement, as users who invest more time and effort may be more inclined to provide feedback in the form of ratings.