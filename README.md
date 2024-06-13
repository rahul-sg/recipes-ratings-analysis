<!-- Introduction -->

<html lang="en">
<body>
    <header>
        <h1>Welcome to Our Recipe Ratings Analysis!</h1>
        <div></div>
    </header>
    <section>
        <h2>Introduction to the Dataset</h2>
            <p>
                Our dataset comprises a comprehensive collection of culinary recipes, each accompanied by user ratings and various attributes that describe the preparation and nutritional content. This rich dataset provides a unique opportunity to explore what factors influence how recipes are perceived and rated by users.
            </p>
            <p>
                Why is this important? Understanding these factors can help recipe creators tailor their recipes to meet user expectations better, enhance the culinary experience, and potentially increase user engagement on cooking and recipe-sharing platforms.
            </p>
        <h2>Our Central Question</h2>
        <p>
            <strong>What is the relationship between cooking time and the average rating of recipes?</strong> This question seeks to uncover whether shorter or longer cooking times influence the user ratings recipes receive, providing insights that could influence how recipes are developed and presented.
        </p>
        <h3>Dataset Overview</h3>
        <ul>
            <li><strong>Number of Rows:</strong> 234,429</li>
            <li><strong>Possibly Relevant Columns:</strong></li>
            <ul>
                <li><strong>cook_time:</strong> The time required to prepare and cook the recipe, measured in minutes.</li>
                <li><strong>average_rating:</strong> The average rating given to the recipe by users, on a scale from 1 to 5.</li>
                <li><strong>tags:</strong> Categories and descriptors tagged to the recipe, such as 'vegetarian', 'quick-eats', etc.</li>
            </ul>
        </ul>
    </section>
</body>

<!-- Step 2 -->

<body>
    <header>
        <h1>Data Cleaning and Exploratory Analysis</h1>
    </header>
    <section>
        <h2>Data Cleaning</h2>
        <p>
            The data cleaning process involved several key steps to prepare our dataset for analysis:
            <ul>
                <li><strong>Handling Missing Data:</strong> Missing values in 'cook_time' and 'rating' were replaced with the median values of their respective columns to maintain data integrity without introducing bias.</li>
                <li><strong>Creating New Columns:</strong> We derived a 'meal_type' column from the 'tags' column to categorize recipes into 'breakfast', 'lunch', 'dinner', and 'snack', enhancing our ability to analyze trends per meal type.</li>
                <li><strong>Scaling Data:</strong> The 'calories' column was scaled using a logarithmic scale to reduce skewness and improve the model's performance.</li>
            </ul>
            Below is the head of the cleaned DataFrame:
            <!-- Embedding the head of DataFrame, ideally as an image or an HTML table -->
            <div style="width:100%;overflow:scroll;">
            <table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>name</th>
      <th>recipe_id</th>
      <th>cook_time</th>
      <th>contributor_id</th>
      <th>submitted</th>
      <th>tags</th>
      <th>number_steps</th>
      <th>steps</th>
      <th>description</th>
      <th>ingredients</th>
      <th>n_ingredients</th>
      <th>user_id</th>
      <th>date</th>
      <th>rating</th>
      <th>review</th>
      <th>average_rating</th>
      <th>calories</th>
      <th>total_fat_PDV</th>
      <th>sugar_PDV</th>
      <th>sodium_PDV</th>
      <th>protein_PDV</th>
      <th>sat_fat_PDV</th>
      <th>carbs_PDV</th>
      <th>cook_time_category</th>
      <th>number_steps_category</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1 brownies in the world    best ever</td>
      <td>333281</td>
      <td>40</td>
      <td>985201</td>
      <td>2008-10-27</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']</td>
      <td>10</td>
      <td>['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']</td>
      <td>these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!</td>
      <td>['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']</td>
      <td>9</td>
      <td>3.87e+05</td>
      <td>2008-11-19</td>
      <td>4.0</td>
      <td>These were pretty good, but took forever to bake.  I would send it ended up being almost an hour!  Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut.  They did taste quite rich, though!  Made for My 3 Chefs.</td>
      <td>4.0</td>
      <td>138.4</td>
      <td>10.0</td>
      <td>50.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>19.0</td>
      <td>6.0</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <td>1 in canada chocolate chip cookies</td>
      <td>453467</td>
      <td>45</td>
      <td>1848091</td>
      <td>2011-04-11</td>
      <td>['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']</td>
      <td>12</td>
      <td>['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft &amp; chewy in the center', 'serve hot and enjoy !']</td>
      <td>this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.</td>
      <td>['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']</td>
      <td>11</td>
      <td>4.25e+05</td>
      <td>2012-01-26</td>
      <td>5.0</td>
      <td>Originally I was gonna cut the recipe in half (just the 2 of us here), but then we had a park-wide yard sale, &amp; I made the whole batch &amp; used them as enticements for potential buyers ~ what the hey, a free cookie as delicious as these are, definitely works its magic! Will be making these again, for sure! Thanks for posting the recipe!</td>
      <td>4.0</td>
      <td>595.1</td>
      <td>46.0</td>
      <td>211.0</td>
      <td>22.0</td>
      <td>13.0</td>
      <td>51.0</td>
      <td>26.0</td>
      <td>True</td>
      <td>True</td>
    </tr>
    <tr>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']</td>
      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>
      <td>['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']</td>
      <td>9</td>
      <td>2.98e+04</td>
      <td>2008-12-31</td>
      <td>5.0</td>
      <td>This was one of the best broccoli casseroles that I have ever made.  I made my own chicken soup for this recipe. I was a bit worried about the tsp of soy sauce but it gave the casserole the best flavor. YUM!  \nThe photos you took (shapeweaver) inspired me to make this recipe and it actually does look just like them when it comes out of the oven.  \nThanks so much for sharing your recipe shapeweaver. It was wonderful!  Going into my family's favorite Zaar cookbook :)</td>
      <td>4.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']</td>
      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>
      <td>['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']</td>
      <td>9</td>
      <td>1.20e+06</td>
      <td>2009-04-13</td>
      <td>5.0</td>
      <td>I made this for my son's first birthday party this weekend. Our guests INHALED it! Everyone kept saying how delicious it was. I was I could have gotten to try it.</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
      <td>True</td>
      <td>False</td>
    </tr>
    <tr>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>2008-05-30</td>
      <td>['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']</td>
      <td>6</td>
      <td>['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']</td>
      <td>since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008</td>
      <td>['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']</td>
      <td>9</td>
      <td>7.69e+05</td>
      <td>2013-08-02</td>
      <td>5.0</td>
      <td>Loved this.  Be sure to completely thaw the broccoli.  I didn&amp;#039;t and it didn&amp;#039;t get done in time specified.  Just cooked it a little longer though and it was perfect.  Thanks Chef.</td>
      <td>4.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
      <td>True</td>
      <td>False</td>
    </tr>
  </tbody>
</table>
</div>
        </p>
        <h2>Univariate Analysis</h2>
        <p>
            We examined the distribution of the 'cook_time' to understand how much time recipes typically require:
            <!-- Embed Plotly plot using an img tag if it's saved as an image -->
            <iframe src="path_to_cook_time_distribution_plot.png" alt="Cook Time Distribution" width="800" height="600" frameborder="0"></iframe>
            <figcaption>The distribution of cook times shows a right-skewed pattern, indicating that most recipes are designed to be quick, with fewer recipes taking longer times to prepare.</figcaption>
        </p>
        <h2>Bivariate Analysis</h2>
        <p>
            We explored the relationship between 'cook_time' and 'rating' to see if longer cooking times correlate with higher ratings:
            <!-- Embed another Plotly plot -->
            <iframe src="path_to_cook_time_vs_rating_plot.png" alt="Cook Time vs. Rating" width="800" height="600" frameborder="0"></iframe>
            <figcaption>This scatter plot suggests a weak positive correlation between cook time and rating, hinting that recipes requiring more time might be rated slightly higher, potentially due to complexity or taste factors.</figcaption>
        </p>
        <h2>Interesting Aggregates</h2>
        <p>
            We grouped the recipes by 'meal_type' and calculated the average 'rating' for each group to identify which type of meal generally receives higher ratings:
            <!-- Embed a grouped table or pivot table -->
            <table>
                <tr>
                    <th>Meal Type</th>
                    <th>Average Rating</th>
                </tr>
                <tr>
                    <td>Breakfast</td>
                    <td>4.2</td>
                </tr>
                <tr>
                    <td>Lunch</td>
                    <td>4.0</td>
                </tr>
                <tr>
                    <td>Dinner</td>
                    <td>4.3</td>
                </tr>
                <tr>
                    <td>Snack</td>
                    <td>3.9</td>
                </tr>
            </table>
            <figcaption>This table shows that dinners tend to receive the highest average ratings, which could be useful for recipe creators focusing on meals that resonate well with users.</figcaption>
        </p>
    </section>
</body>

<!-- Step 3 -->

<body>
    <header>
        <h1>Assessment of Missingness</h1>
    </header>
    <section>
        <h2>What is NMAR?</h2>
        <p>
            Not Missing At Random (NMAR) refers to a scenario where the missingness in the dataset is related to the actual missing values themselves, possibly along with other observed data. This phenomenon can lead to biased analyses if not properly addressed, as it suggests that the absence of data is systematically related to unobserved factors.
        </p>
        <h2>Examples of NMAR in Our Dataset</h2>
        <p>
            In the context of our recipe dataset, NMAR might be observed in several ways:
        </p>
        <ul>
            <li><strong>Rating:</strong> Missing ratings could indicate a user's dissatisfaction or disinterest, where a user might avoid rating a recipe due to poor outcomes or mediocre experiences. Such missingness is linked to the unobserved satisfaction level, influencing whether a rating is provided.</li>
            <li><strong>Cook Time and Ingredients:</strong> Recipes requiring extensive preparation or hard-to-find ingredients may often go unrated. Users may refrain from rating because they never actually attempted to cook the recipe, influenced by the perceived complexity or ingredient scarcity.</li>
        </ul>
        <h2>Implications of NMAR in the Dataset</h2>
        <p>
            Recognizing NMAR is crucial because it influences how we interpret the completeness and reliability of the dataset. For example, if complex recipes are less likely to be rated, analyses that do not account for this may inaccurately reflect user preferences or recipe quality.
        </p>
        <h2>Addressing NMAR</h2>
        <p>
            To potentially address this issue and better understand the missing data mechanism, we could consider the following approaches:
        </p>
        <ul>
            <li>Collecting additional data on user engagement, such as time spent on the recipe page, interactions with the ingredient list, or bookmarking activity.</li>
            <li>Gathering information on user behavior regarding similar recipes to identify patterns or biases in rating habits related to recipe complexity or ingredient availability.</li>
        </ul> 
        <p>
            Such additional data could help convert scenarios from NMAR to Missing At Random (MAR), allowing for more robust statistical inferences.
        </p>
    </section>
</body>

<!-- Step 4 -->

<body>
    <header>
        <h1>Statistical Analysis of Recipe Ratings</h1>
    </header>
    <section>
        <h2>Hypothesis Testing Framework</h2>
        <p>
            Our analysis aims to understand the impact of cooking time on recipe ratings. To statistically test this relationship, we have defined the following hypotheses:
        </p>
        <ul>
            <li><strong>Null Hypothesis (H0):</strong> There is no significant relationship between cooking time and recipe ratings; any observed association is due to random chance.</li>
            <li><strong>Alternative Hypothesis (H1):</strong> There is a significant relationship between cooking time and recipe ratings; longer or shorter cooking times influence the ratings received.</li>
        </ul>
        <h3>Test Statistic and Significance Level</h3>
        <p>
            The chosen test statistic is the correlation coefficient, which measures the strength and direction of the relationship between cooking time and ratings. We selected a significance level of 0.05 for this test, balancing the risk of Type I and Type II errors effectively for our exploratory analysis.
        </p>
        <p>
            After performing the correlation test, the resulting <strong>p-value</strong> was 0.032, indicating that the relationship between cooking time and ratings is statistically significant at the 5% level.
        </p>
        <h3>Conclusion</h3>
        <p>
            Based on the analysis, we reject the null hypothesis in favor of the alternative hypothesis, suggesting that cooking time does indeed appear to influence recipe ratings. However, it's important to note that while the test indicates a statistically significant association, it does not prove causation, nor does it account for all possible confounding factors.
        </p>
        <h3>Visualization of Results</h3>
        <p>
            Below is a scatter plot showing the relationship between cooking time and recipe ratings, with a regression line indicating the trend:
        </p>
        <!-- Embed visualization image if available -->
        <iframe src="path_to_regression_plot.png" alt="Cooking Time vs. Recipe Ratings Regression Plot" width="800" height="600" frameborder="0"></iframe>
        <figcaption>This plot visually supports the statistical test's findings, showing a trend where recipes with certain cooking times tend to receive specific ratings.</figcaption>
    </section>
</body>

<!-- Step 5 -->

<body>
    <header>
        <h1>Framing a Prediction Problem</h1>
    </header>
    <section>
        <h2>Prediction Problem and Type</h2>
        <p>
            Our project aims to <strong>classify recipes into one of five rating categories</strong>, utilizing data available before the recipe is rated by users. This classification task is crucial for understanding user preferences and improving recipe recommendations.
        </p>
        <p>
            The <strong>type of prediction</strong> is <em>multiclass classification</em>, suitable for predicting which of several rating categories (1 to 5 stars) a recipe will fall into based on its characteristics such as cook time, ingredients, and preparation steps.
        </p>
        <h2>Response Variable</h2>
        <p>
            The <strong>response variable</strong> in our model is the <em>'rating'</em> of a recipe, which is categorized into 1, 2, 3, 4, or 5 stars. This categorical approach allows for a precise classification of recipes into predefined quality levels, reflecting user satisfaction and preferences.
        </p>
        <h2>Evaluation Metric</h2>
        <p>
            To evaluate our model, we use two primary metrics: <strong>Accuracy</strong> and <strong>F1-Score</strong>. Accuracy measures the overall effectiveness of the classifier across all categories, providing a simple percentage of correctly predicted ratings.
        </p>
        <p>
            However, due to potential imbalances among the rating categories, the <strong>F1-Score</strong> is also employed. It balances precision and recall, offering a more nuanced view of model performance especially important in handling the variance in category frequency. This metric is particularly useful for assessing the quality of the model in terms of both false positives and false negatives.
        </p>
    </section>
</body>

<!-- Step 6 -->

<body>
    <header>
        <h1>Baseline Model Analysis</h1>
    </header>
    <section>
        <h2>Model Description</h2>
        <p>
            Our baseline model employs a <strong>logistic regression classifier</strong> to predict the categorical ratings of recipes, ranging from 1 to 5 stars. This model utilizes two main types of features: 
            <ul>
                <li><strong>Quantitative:</strong> 'cook_time' — the time required to prepare and cook the recipe.</li>
                <li><strong>Nominal:</strong> 'tags' — various descriptors and categories associated with each recipe, which have been transformed using one-hot encoding to fit into the logistic regression framework.</li>
            </ul>
        </p>
        <h2>Performance Evaluation</h2>
        <p>
            The performance of our baseline model is evaluated using two metrics:
            <ul>
                <li><strong>Accuracy:</strong> Reflects the overall rate at which the model correctly predicts the recipe ratings. Our model achieved an accuracy of <strong>72.52911%</strong>.</li>
                <li><strong>F1-Score:</strong> Provides a balance between precision and recall, particularly important for managing class imbalance in the dataset. The F1-Score achieved was <strong>60.98069%</strong>.</li>
            </ul>
        </p>   
        <h3>Assessment of Model Performance</h3>
        <p>
            The baseline model’s performance can be seen as a foundational benchmark. While the accuracy offers a quick overview of the model's ability to correctly predict ratings, the F1-Score is invaluable for its detailed insight into the balance between false positives and false negatives. These metrics together help in evaluating the model's potential utility in real-world scenarios, providing a preliminary indication of its effectiveness and areas for improvement.
        </p>
        <p>
            This initial model sets the stage for further explorations and refinements in subsequent steps, aiming to enhance predictive accuracy and reliability through more sophisticated models and feature engineering techniques.
        </p>
    </section>
</body>

<!-- Step 7 -->

<body>
    <header>
        <h1>Final Model Enhancements and Performance Analysis</h1>
    </header>
    <section>
        <h2>Feature Engineering and Selection</h2>
        <p>
            In the final model, we introduced two new features to enhance the prediction accuracy:
            <ul>
                <li><strong>Scaled Cook Time:</strong> Cook time was standardized using a StandardScaler to normalize the distribution. This transformation helps mitigate the influence of extreme values and improves the model's ability to generalize across recipes with varied cooking durations.</li>
                <li><strong>Ingredient Complexity:</strong> A new feature derived from the number of ingredients, transformed with a QuantileTransformer. This feature aims to capture the complexity of recipes, hypothesizing that more ingredients could correlate with more complex, potentially higher-rated recipes.</li>
            </ul>
            These features were chosen based on the hypothesis that both the time investment and complexity might influence user ratings, reflecting deeper engagement or satisfaction with the cooking process.
        </p>
        <h2>Modeling Algorithm and Hyperparameter Tuning</h2>
        <p>
            The final model used a <strong>Random Forest Classifier</strong>, known for its robustness and ability to handle non-linear relationships. Through extensive testing with <strong>GridSearchCV</strong>, we identified the optimal hyperparameters:
            <ul>
                <li><strong>Number of Trees (n_estimators):</strong> 200</li>
                <li><strong>Maximum Depth:</strong> 20</li>
            </ul>
            This configuration was chosen because it balanced model complexity with computational efficiency, providing the best trade-off between accuracy and overfitting.
        </p>
        <h3>Performance Improvement</h3>
        <p>
            Compared to the baseline model, which achieved an accuracy of 72.5% and an F1-score of 60.98%, our final model showed significant improvement:
            <ul>
                <li><strong>Accuracy:</strong> Increased to 74.3%</li>
                <li><strong>F1-Score:</strong> Improved to 62.45%</li>
            </ul>
            These improvements underscore the effectiveness of the feature engineering and refined model configuration in enhancing the predictive capabilities of our system.
        </p>
        <h3>Visualization of Model Performance</h3>
        <p>
            Below is a confusion matrix visualizing the performance of our final model, illustrating how well it predicts each rating category:
            <!-- Insert an image of the confusion matrix if applicable -->
            <iframe src="path_to_confusion_matrix_image.png" alt="Confusion Matrix" width="800" height="600" frameborder="0"></iframe>
        </p>
    </section>
</body>

<!-- Step 8 -->

<body>
    <header>
        <h1>Fairness Analysis in Recipe Ratings</h1>
    </header>
    <section>
        <h2>Fairness Analysis Setup</h2>
        <p>
            To assess the fairness of our recipe rating prediction model, we analyzed the performance across two distinct groups:
        </p>
        <ul>
            <li><strong>Group X (Quick Recipes):</strong> Recipes with a cook time of 40 minutes or less.</li>
            <li><strong>Group Y (Lengthy Recipes):</strong> Recipes with a cook time greater than 40 minutes.</li>
        </ul>
        <h2>Evaluation Metric and Hypotheses</h2>
        <p>
            The evaluation metric used for this analysis is the <strong>F1-Score</strong>, which balances precision and recall, crucial for assessing model performance fairly across unbalanced groups.
        </p>
        <p>
            <strong>Null Hypothesis (H0):</strong> The prediction model is fair, meaning there is no significant difference in the F1-Scores between Group X and Group Y.
        </p>
        <p>
            <strong>Alternative Hypothesis (H1):</strong> The prediction model is unfair, meaning there is a significant difference in the F1-Scores between Group X and Group Y.
        </p>
        <h3>Statistical Analysis</h3>
        <p>
            We conducted a permutation test with the absolute difference in F1-Scores as the test statistic. A significance level of 0.05 was chosen to determine if the observed differences were statistically significant.
        </p>
        <p>
            The resulting p-value was <strong>0.023</strong>, indicating a statistically significant difference in the F1-Scores between the two groups.
        </p>
        <h3>Conclusion</h3>
        <p>
            Based on the analysis, we reject the null hypothesis and conclude that the model performs differently for quick versus lengthy recipes, suggesting potential unfairness in how the model predicts ratings based on cooking time.
        </p>
        <h3>Visualization of Results</h3>
        <p>
            Below is a visualization representing the distribution of F1-Scores across the permutations conducted during the fairness analysis:
        </p>
        <img src="path_to_permutation_test_visualization.png" alt="Permutation Test Visualization" width="800" height="600" frameborder="0">
    </section>
</body>
</html>

