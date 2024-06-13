<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Recipe Ratings Analysis</title>
</head>
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
            <li><strong>Relevant Columns:</strong></li>
            <ul>
                <li><strong>cook_time:</strong> The time required to prepare and cook the recipe, measured in minutes.</li>
                <li><strong>average_rating:</strong> The average rating given to the recipe by users, on a scale from 1 to 5.</li>
                <li><strong>tags:</strong> Categories and descriptors tagged to the recipe, such as 'vegetarian', 'quick-eats', etc.</li>
            </ul>
        </ul>
    </section>
</body>


<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Data Cleaning and Exploratory Data Analysis</title>
</head>
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
            <img src="path_to_dataframe_head.png" alt="Head of Cleaned DataFrame">
        </p>
        <h2>Univariate Analysis</h2>
        <p>
            We examined the distribution of the 'cook_time' to understand how much time recipes typically require:
            <!-- Embed Plotly plot using an img tag if it's saved as an image -->
            <img src="path_to_cook_time_distribution_plot.png" alt="Cook Time Distribution">
            <figcaption>The distribution of cook times shows a right-skewed pattern, indicating that most recipes are designed to be quick, with fewer recipes taking longer times to prepare.</figcaption>
        </p>
        <h2>Bivariate Analysis</h2>
        <p>
            We explored the relationship between 'cook_time' and 'rating' to see if longer cooking times correlate with higher ratings:
            <!-- Embed another Plotly plot -->
            <img src="path_to_cook_time_vs_rating_plot.png" alt="Cook Time vs. Rating">
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


<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NMAR Analysis in Recipe Ratings</title>
</head>
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


<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prediction Model for Recipe Ratings</title>
</head>
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


<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Baseline Model for Recipe Ratings</title>
</head>
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


<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Final Model Enhancements and Performance</title>
</head>
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
            <img src="path_to_confusion_matrix_image.png" alt="Confusion Matrix" style="width:100%;max-width:600px;">
        </p>
    </section>
</body>


<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fairness Analysis of Recipe Ratings</title>
</head>
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
        <img src="path_to_permutation_test_visualization.png" alt="Permutation Test Visualization" style="width:100%;max-width:600px;">
    </section>
</body>
</html>

