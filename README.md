# Recipe-and-Average-Rating-Research-Project-2023

By Yulin Chen & Jiarui Zha  

Nov 2023

## Introduction of the Project

The project delves into the fascinating intersection of culinary art and data analysis. We aim to unearth patterns and insights that are not immediately apparent. Specifically, we focuses on understanding **how the number of ingredients in a recipe might influence its users' ratings**. 

Understanding the relationship between the number of ingredients in a recipe and its ratings is crucial for various reasons. It reveals consumer preferences, indicating whether simplicity or complexity is more valued in cooking. This insight is vital for chefs, recipe developers, and the food industry, as it guides recipe creation and menu planning, potentially influencing customer satisfaction and business success. Additionally, it offers home cooks guidance on popular recipe choices and can inform culinary education. For the health-conscious, it may also highlight trends in nutritional choices. Essentially, this analysis bridges culinary art with consumer behavior, enhancing our understanding of food preferences.

We collected our data from food.com, a renowned online platform that offers a vast collection of user-contributed recipes. This website has become a go-to resource for both amateur and professional cooks seeking culinary inspiration, recipe instructions, and nutritional information. The significance of sourcing data from food.com lies in its large user base and the diversity of recipes it hosts, which reflect a wide array of culinary tastes and preferences.

The data from food.com has divided into two seprated datasets: food_recipe and user_interactions. The food_recipe dataset contains 83782 rows,meaning we have 83782 unique recipes. Some relevant columns to our projects are *recipe name*, *recipe id*, *ingredients*, and *number of ingredients*. The user_interactions dataset contains 731927 rows,meaning we have 731927 reviews from the users. Some relevant columns to our projects are *recipe id* and *rating*. 

After collecting the data,we noticed that both dataset contains the recipe id. Before investigate our project,we choose to merge the food_recipe and the user_interactions dataset by *recipe id*. For futher research purpose, we have add column *average_rating* for each food recipe. In order to better correspond and find recipes, we use recipe id as the index.
The result dataframe is shown below(with only relevant columns display).

|     id | name                                 | ingredients                                                                                                                                                                                                                             |   n_ingredients |   average_rating |
|-------:|:-------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-----------------:|
| 333281 | 1 brownies in the world    best ever | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']                                                          |               9 |                4 |
| 453467 | 1 in canada chocolate chip cookies   | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                                                                             |              11 |                5 |
| 306168 | 412 broccoli casserole               | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']                                                                   |               9 |                5 |
| 286009 | millionaire pound cake               | ['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']                                                                                                                                |               7 |                5 |
| 475785 | 2000 meatloaf                        | ['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil'] |              13 |                5 |


## Cleaning and EDA (Exploratory Data Analysis)
