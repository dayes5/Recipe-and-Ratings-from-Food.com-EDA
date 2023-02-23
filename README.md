# Recipe-and-Ratings-from-Food.com-EDA

## Introduction



Our merged dataset contains these relevant columns: 

| Column Name | Description |
| ----------- | ----------- |
| `name` | Name of the recipe |
| `id` | A unique identifier for each recipe |
| `tags` | A list of different tags that apply to this recipe |
| `nutrition`| Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]. PDV stands for “percentage of daily value” |
| `n_steps` | The number of steps for this recipe |
| `description` | The user-provided description |
| `rating` | The rating given, out of a total of 5 |
| `review` | The text of the given review |
| `avg_rate` | The average rating for this recipe |

Note: In our data cleaning process, our `nutrition` column was later split into different columns such as `protein` (PDV) and `carbohydrates` (PDV). One such relevant column is `calories`:

| `calories` | The number of calories for this recipe |

## Cleaning and EDA

 
**Data Cleaning**

Our first step was to merge the recipes DataFrame, which contains information about things like a recipe’s ingredients and tags, with the interactions DataFrame, which contains information about things like reviews and ratings from different users.

We then decided to find the average rating of each recipe, and added the information in a new column: `avg_rate`. We also changed the `submitted` and `date` columns from strings to datetime objects.

Next, we decided to separate the elements inside of the nutrition and tags for better readability and analysis potential. 

We used string methods to convert the data inside of the `nutrition`, `tags`, `steps`, and `ingredients` columns from a string of a list to an actual list.

In our merged dataframe, we exchanged the nutrition columns for columns such as `calories`, `total_fat`, etc., which correspond with the original values and units in the old nutrition lists. 

We decided to use one-hot encoding to flatten our tags data, as shown below:



**Univariate Graph EDA**
<iframe src="assets/protien_univariate2.html" width=800 height=600 frameBorder=0></iframe>
Description and Trends: This is a graph that shows the recipes and their protein count. From the graph, we can quickly see that many recipes (about 43,000) have a protein amount between 0 to 4 PDV(Percent Daily Value) ; the distribution is right-skewed and we see a large decrease in the number of recipes following the initial peak. 

**Bivariate Graph EDA**

<iframe src="assets/box_biivariate.html" width=800 height=600 frameBorder=0></iframe>
Description and Trends: This graph gives us a box plot, or a five summary set, for calories per rating. It tells us the minimum, 1st quartile, median, 3rd quartile, and maximum for calories within each ranking. Based on this graph, we can see that the 1st quartile, or where the first 25% of the calorie values would lie, remains fairly consistent throughout each ranking. We can also see that the median for calories, per each rating, are about the same. As the rating decreases, the 3rd quartile, or the value where 75% and less of the data lies, appears to increase in number of calories. The max calorie count is very variable throughout the rankings. 






## Assessment of Missingness

**NMAR ANALYSIS:***
What is NMAR? → add this?

We believe that the `description` column of our dataset is Not Missing At Random (NMAR). We believe this because the description of a recipe does not really have any correlation to the other columns like `recipe_id`, `recipe_name`, or `n_steps`. In addition, the description may be missing depending on the actual description itself. For example, if the description would have been extremely short, since the recipe is self-explanatory or very widely known, users may have decided to exclude the description. If the user was lazy, and wanted to only write the bare minimum, they may have also decided to exclude a description. Because of the `description` column’s (logical) independence from the other columns in our DataFrame, and how the values of description itself may influence the missingness of the `description` column, we decided to categorize the `description` column as NMAR.


## Hypothesis Testing

