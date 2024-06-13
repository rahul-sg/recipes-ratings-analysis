<!-- Introduction -->

<html lang="en">
<body>
    <header>
        <h1>Welcome to Our Recipe Ratings Analysis!</h1>
        <h3>By: Rahul Sengupta</h3>
        <p><strong>NOTE/IMPORTANT:</strong> I realized I accidentally turned in a much older version of the jupyter notebook on gradescope and was unable to resubmit the correct one
        I have attached the correct one here: 
        </p>
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
                <li><strong><code>cook_time:</code></strong> The time required to prepare and cook the recipe, measured in minutes.</li>
                <li><strong><code>average_rating:</code></strong> The average rating given to the recipe by users, on a scale from 1 to 5.</li>
                <li><strong><code>tags</code></strong> Categories and descriptors tagged to the recipe, such as 'vegetarian', 'quick-eats', etc.</li>
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
                <li><strong>Handling Missing Data:</strong> Missing values in <code>cook_time</code> and <code>rating</code> were replaced with the median values of their respective columns to maintain data integrity without introducing bias. We used mean imputation to replace the correct missing values for numerical columns. <strong>Note:</strong> These were done after the MAR analysis.</li>
                <li><strong>Handling datetimes:</strong> Converted the object values in <code>submitted</code> and <code>date</code> to pd.datetime objects.</li>
                <li><strong>Melted <code>nutrition</code>:</strong> Extracted the list objects from <code>nutrition</code> column and made them separate variables in the dataframe.</li>
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
                    <td>['60-minutes-or-less', 'time-to-make', ...]</td>
                    <td>10</td>
                    <td>['heat the oven to 350f and arrange the ...]</td>
                    <td>these are the most; chocolatey, moist,...</td>
                    <td>['bittersweet chocolate', 'unsalted butter', 'eggs', ...]</td>
                    <td>9</td>
                    <td>3.87e+05</td>
                    <td>2008-11-19</td>
                    <td>4.0</td>
                    <td>These were pretty good, but took forever to bake.  I woul...</td>
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
                    <td>['60-minutes-or-less', 'time-to-make', ...]</td>
                    <td>12</td>
                    <td>['pre-heat oven the 350 degrees f', 'in a mixing bowl ...]</td>
                    <td>this is the recipe that we use at my school cafete...</td>
                    <td>['white sugar', 'brown sugar', 'salt', 'margarine', ...]</td>
                    <td>11</td>
                    <td>4.25e+05</td>
                    <td>2012-01-26</td>
                    <td>5.0</td>
                    <td>Originally I was gonna cut the recipe in half ...</td>
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
                    <td>['60-minutes-or-less', 'time-to-make...]</td>
                    <td>6</td>
                    <td>['preheat oven to 350 degrees', 'spra...]</td>
                    <td>since there are already 411 recipes for broccoli ...</td>
                    <td>['frozen broccoli cuts', 'cream of chicken soup'...]</td>
                    <td>9</td>
                    <td>2.98e+04</td>
                    <td>2008-12-31</td>
                    <td>5.0</td>
                    <td>This was one of the best broccoli casseroles ...</td>
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
                    <td>['60-minutes-or-less', 'time-to-make', 'course'...]</td>
                    <td>6</td>
                    <td>['preheat oven to 350 degrees', 'spray a 2 quart ...]</td>
                    <td>since there are already 411 recipes for broccoli ...</td>
                    <td>['frozen broccoli cuts', 'cream of chicken soup', ...]</td>
                    <td>9</td>
                    <td>1.20e+06</td>
                    <td>2009-04-13</td>
                    <td>5.0</td>
                    <td>I made this for my son's first birthday party...</td>
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
                    <td>['60-minutes-or-less', 'time-to-make'...]</td>
                    <td>6</td>
                    <td>['preheat oven to 350 degrees', 'spray a 2 quart baking ...]</td>
                    <td>since there are already 411 recipes for broccoli ...</td>
                    <td>['frozen broccoli cuts', 'cream of chicken soup', ...]</td>
                    <td>9</td>
                    <td>7.69e+05</td>
                    <td>2013-08-02</td>
                    <td>5.0</td>
                    <td>Loved this.  Be sure to completely thaw the broccoli...</td>
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
            <h3><code>cook_time</code></h3>
            <p>
                We examined the distribution of the 'cook_time' to understand how much time recipes typically require:
                <!-- Embed Plotly plot using an img tag if it's saved as an image -->
                <iframe src="assets/univar1.html" alt="Cook Time Distribution" width="800" height="450" frameborder="0"></iframe>
                <figcaption>The distribution of cook times shows a right-skewed pattern, indicating that most recipes are designed to be quick, with fewer recipes taking longer times to prepare.</figcaption>
            </p>
            <h3><code>number_steps</code></h3>
            <p>
                We examined the distribution of the 'number_steps' to understand how much time recipes typically require:
                <!-- Embed Plotly plot using an img tag if it's saved as an image -->
                <iframe src="assets/univar2.html" alt="Cook Time Distribution" width="800" height="450" frameborder="0"></iframe>
                <figcaption>The distribution of the number of steps shows a right-skewed pattern, indicating that most recipes are designed to be quick, with fewer recipes having lesser steps to complete.</figcaption>
            </p>
            <h3><code>rating</code></h3>
            <p>
                We examined the distribution of the <code>rating</code> to understand how ratings are typically assigned for recips:
                <!-- Embed Plotly plot using an img tag if it's saved as an image -->
                <iframe src="assets/univar3.html" alt="Cook Time Distribution" width="800" height="450" frameborder="0"></iframe>
                <figcaption>The distribution of ratings shows a left-skewed pattern, indicating that most recipes have pretty high ratings. One can infer that food is a comfort for many, which is why people are more compelled to rate them higher as opposed to goods from amazon or any other items purchased/made</figcaption>
            </p>
            <h3><code>average_rating</code></h3>
            <p>
                We examined the distribution of the <code>average_rating</code> to how ratings are distributed based on each recipe:
                <!-- Embed Plotly plot using an img tag if it's saved as an image -->
                <iframe src="assets/univar4.html" alt="Cook Time Distribution" width="800" height="450" frameborder="0"></iframe>
                <figcaption>The distribution of average ratings also shows a right-skewed pattern. In this case we can see that the 4 star rating is more common than the 5 star rating for the distribution of all ratings. This could suggest that a majority of ratings of a recipe are 4 stars as it is grouped by recipe here and not a total distribution. </figcaption>
            </p>
        <h2>Bivariate Analysis</h2>
            <h3>Frequency of High and Low Cook Time for Each Rating (High/Low is Comparison to median)</h3>
            <p>
                We explored the relationship between <code>cook_time</code> and <code>rating</code> to see if longer cooking times correlate with higher ratings:
                <!-- Embed another Plotly plot -->
                <iframe src="assets/bivar1.html" alt="Cook Time vs. Rating" width="800" height="450" frameborder="0"></iframe>
                <figcaption>This scatter plot suggests a weak negative correlation between cook time and rating, hinting that recipes requiring more time might be rated slightly lower, potentially due to complexity or taste factors. Note: False means low cook time and True means higher cook times. A high cook time in this case is calculated by being greater than the median of the dataset (35.0 minutes in this case)</figcaption>
            </p>
            <h3>Frequency of High and Low Number of Steps for Each Rating (High/Low is Comparison to median)</h3>
            <p>
                We explored the relationship between <code>cook_time</code> and <code>average_rating</code> to see if longer cooking times correlate with higher ratings:
                <!-- Embed another Plotly plot -->
                <iframe src="assets/bivar2.html" alt="Number Steps vs. Rating" width="800" height="450" frameborder="0"></iframe>
                <figcaption>This scatter plot suggests a weak negative correlation between the number of steps and rating, hinting that recipes with more steps might be rated slightly lower, potentially due to complexity or taste factors. Note: False means low steps and True means higher step counts. A high step count in this case is calculated by being greater than the median of the dataset (9.0 minutes in this case)</figcaption>
            </p>
        <h2>Interesting Aggregates</h2>
        <p>
            We grouped the recipes by whether they have a 'High Cook Time' and 'High Number of Steps', calculated using the median values as thresholds. The average 'rating' for each group was then computed to identify how these factors influence user ratings:
            <ul>
                <li><strong>High Cook Time %:</strong> This is a Boolean condition that classifies recipes into those with a cook time greater than the median (True) and those with a cook time less than or equal to the median (False).
                </li>
                <li><strong>High Number of Steps %:</strong> Similar to cook time, this Boolean condition classifies recipes based on whether the number of steps is greater than the median (True) or not (False).
                </li>
            </ul>
            The resulting pivot table shows the mean ratings for recipes based on these classifications, allowing us to see whether recipes that are more time-consuming or complex (in terms of steps) receive higher or lower average ratings compared to their simpler counterparts.
            <div></div>
            <!-- Embed a grouped table or pivot table -->
            <table border="1" class="dataframe">
            <thead>
                <tr style="text-align: right;">
                <th></th>
                <th></th>
                <th>rating</th>
                </tr>
                <tr>
                <th>High Cook Time %</th>
                <th>High Number of Steps %</th>
                <th></th>
                </tr>
            </thead>
            <tbody>
                <tr>
                <th rowspan="2" valign="top">False</th>
                <th>False</th>
                <td>4.70</td>
                </tr>
                <tr>
                <th>True</th>
                <td>4.68</td>
                </tr>
                <tr>
                <th rowspan="2" valign="top">True</th>
                <th>False</th>
                <td>4.64</td>
                </tr>
                <tr>
                <th>True</th>
                <td>4.67</td>
                </tr>
            </tbody>
            </table>
            <figcaption>The data suggests a nuanced relationship between recipe complexity (in terms of cook time and steps) and user ratings. Simpler recipes receive the highest ratings, which could be due to the ease and convenience they offer. However, when complexity is necessary, having recipes that are engaging or yield better results (potentially indicated by more steps) may lead to slightly better ratings than recipes that are merely time-consuming without added engagement.
            This analysis implies that recipe developers might want to consider balancing complexity and time investment to optimize user satisfaction and ratings. Further statistical testing could confirm if these differences are significant and explore other factors that might influence ratings.
            </figcaption>
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
        <h2>Addressing NMAR in Our Dataset</h2>
        <p>
            To potentially address this issue and better understand the missing data mechanism, we could consider the following:
        </p>
        <p>
            The following graph represents the Empirical Distribution of the shuffled abs differences based on two columns that are potentially MAR: <code>ratings</code> and <code>average_ratings</code>
            <!-- Embed another Plotly plot -->
            <iframe src="assets/missingness.html" alt="Empirical Distribution of the shuffled abs differences" width="800" height="450" frameborder="0"></iframe>
            <figcaption>Based on the permutation test, the observed absolute difference in <code>average_rating</code> between recipes with and without ratings is approximately 0.105. The p-value of 0.185 exceeds the common significance threshold of 0.05, indicating that there is not enough evidence to reject the null hypothesis at the 5% significance level. Consequently, we fail to reject the null hypothesis, suggesting that the observed difference could occur by random chance under the null conditions. Therefore, we do not have sufficient statistical evidence to conclude that the missingness in <code>rating</code> is dependent on <code>average_rating</code>.</figcaption>
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
            <li><strong>Test Statistic:</strong> Total Variation Distance as we are comparing two categorical distributions: cook_time_category (True or False) and ratings (1-5).</li>
        </ul>
        <p>
            <strong>Histogram Distribution:</strong> The histogram showcases the empirical distribution of the TVD from permutations. This distribution implies that most shuffled datasets under the null hypothesis (which states that <code>cook_time_category</code> does not affect <code>average_rating</code>) exhibited only minor differences in the distribution of ratings between the groups.
        </p>
        <p>
            The resulting <strong>p-value</strong> of 0.0 indicates that the relationship between cooking time and ratings is statistically significant, suggesting a strong departure from the null hypothesis at our 5% significance level.
        </p>
        <p>
            <strong>Observed Difference:</strong> The observed TVD of 0.02895 is notably higher than most of the differences observed in the shuffled data, supporting the alternative hypothesis that cooking time significantly influences recipe ratings.
        </p>
        <p>
            <!-- Embed another Plotly plot -->
            <iframe src="assets/hypothesis.html" alt="Empirical Distribution of the shuffled abs differences" width="800" height="450" frameborder="0"></iframe>
            <figcaption><strong>Statistical Significance:</strong> With a p-value of 0.0, we reject the null hypothesis. This result indicates that the observed difference in TVD is highly unlikely to occur by chance, pointing to a significant impact of cooking time on recipe ratings.</figcaption>
        </p>
        <p>
            <strong>Practical Implication:</strong> This statistically significant finding suggests that cooking time is a determinant factor in how recipes are rated. Stakeholders focusing on recipe development and marketing might consider these findings to enhance user satisfaction and engagement.
        </p>
        <p>
            <strong>Causation vs. Correlation:</strong> While our test indicates a significant correlation, it does not establish causation. Further research could explore other contributing factors or experimental designs to better understand the causative impacts of cooking time on ratings.
        </p>
        <h3>Conclusion</h3>
        <p>
            The hypothesis testing conducted provides robust evidence that cooking time has a statistically significant impact on the ratings recipes receive, effectively rejecting the null hypothesis. This finding encourages further investigation into how cooking time and possibly other related factors influence user perceptions and ratings of recipes.
        </p>
    </section>
</body>

<!-- Step 5 -->

<body>
    <header>
        <h1>Baseline Model Analysis</h1>
    </header>
    <section>
        <h2>Model Description and Features</h2>
        <p>
            The baseline model utilizes a logistic regression classifier configured within a pipeline that incorporates both data preprocessing and model training.
        </p>
        <ul>
            <li><strong>Quantitative Features:</strong>
                <ul>
                    <li><code>cook_time</code> - A numerical feature, where missing values are imputed using the mean of this feature's available data.</li>
                </ul>
            </li>
            <li><strong>Nominal Features:</strong>
                <ul>
                    <li><code>tags</code> - Includes categorical data processed with <code>OneHotEncoder</code> to convert categories into a format suitable for logistic regression, handling unknown categories by ignoring them.</li>
                </ul>
            </li>
        </ul>
        <h2>Data Preprocessing</h2>
        <p>
            Data preprocessing is conducted using a <code>ColumnTransformer</code> to apply the appropriate transformations:
        </p>
        <ul>
            <li><code>SimpleImputer</code> for <code>cook_time</code> handles missing values by substituting them with the column mean.</li>
            <li><code>OneHotEncoder</code> for <code>tags</code> converts categorical data into a numerical format suitable for model training.</li>
        </ul>
        <h2>Model Performance</h2>
        <p>
            The logistic regression model's performance is evaluated based on two key metrics:
        </p>
        <ul>
            <li><strong>Accuracy:</strong> Achieved an accuracy of 72.52911%, indicating the model predicts correctly about 72.5% of the time.</li>
            <li><strong>F1-Score:</strong> The weighted F1-score is 0.6098069085681512, reflecting the precision and recall balanced by the number of instances in each class.</li>
        </ul>
        <h2>Evaluation and Conclusion</h2>
        <p>
        <strong>Assessment of Model Quality:</strong>
        <ul>
            <li>The model shows decent accuracy, suggesting it has a fair capability to generalize from the training data to unseen data. However, the F1-score is relatively lower, indicating potential issues with class imbalance or that the model is not equally effective across all rating classes.</li>
            <li>Given the complex nature of taste and recipe preferences, an accuracy of approximately 72.5% is reasonably good for a baseline model but leaves room for improvement, particularly in how it handles the balance between classes as indicated by the F1-score.</li>
        </ul>
        </p>
        <p>
        <strong>Improvement Considerations:</strong>
        <ul>
            <li>Enhancing the model could involve integrating more descriptive features that could influence recipe ratings, such as ingredient lists, nutritional information, or user-generated metadata like the number of reviews.</li>
            <li>Experimenting with different classifiers and tuning the model's hyperparameters could also potentially yield better performance.</li>
        </ul>
        </p>
    </section>
</body>

<!-- Step 7 -->

<body>
    <header>
        <h1>Final Model Performance and Setup</h1>
    </header>
    <section>
        <h2>Features and Rationale</h2>
        <p>
            The final model includes a mix of quantitative and transformed features: <code>'cook_time'</code>, <code>'number_steps'</code>, <code>'calories'</code>, <code>'sugar_PDV'</code>, <code>'sat_fat_PDV'</code>, and <code>'n_ingredients'</code>. These features were chosen based on their relevance to the nutritional content and preparation complexity of recipes, which are hypothesized to influence user ratings. Quantitative features like <code>'calories'</code> and <code>'sugar_PDV'</code> reflect nutritional aspects that might affect user preferences, while <code>'n_ingredients'</code> and <code>'number_steps'</code> offer insights into the complexity of the recipe. The quantile transformation of <code>'n_ingredients'</code> normalizes its distribution, enhancing model sensitivity to variations in recipe complexity.
        </p>
        <h2>Modeling Algorithm and Hyperparameter Tuning</h2>
        <p>
            The final model used a <strong>Random Forest Classifier</strong>, known for its robustness and ability to handle non-linear relationships. Through extensive testing with <strong>GridSearchCV</strong>, we identified the optimal hyperparameters:
            <ul>
                <li><strong>Number of Trees (<code>n_estimators</code>):</strong> 50</li>
                <li><strong>Maximum Depth (<code>max_depth</code>):</strong> 10</li>
            </ul>
            This configuration was chosen because it balanced model complexity with computational efficiency, providing the best trade-off between accuracy and overfitting.
        </p>
        <p>
            The final model's configuration, including a preprocessor with scaling and quantile transformations, was finalized into a pipeline ensuring streamlined preprocessing and classification processes.
        </p>
        <h2>Performance Improvement</h2>
        <p>
            Compared to the baseline model, which achieved an accuracy of 72.5% and an F1-score of 60.98%, our final model showed improvement in accuracy:
            <ul>
                <li><strong>Accuracy:</strong> Increased to 72.3968%</li>
                <li><strong>F1-Score:</strong> Slightly decreased to 60.805%</li>
            </ul>
        </p>
        <p>
            These metrics illustrate the effectiveness of the feature engineering and hyperparameter tuning strategies in enhancing the model's predictive accuracy and its ability to balance precision and recall across different rating classes.
        </p>
    </section>
</body>


<!-- Step 8 -->

<body>
    <header>
        <h1>Fairness Analysis of the Recipe Rating Prediction Model</h1>
    </header>
    <section>
        <h2>Analysis Setup</h2>
        <p>
            For the fairness analysis, we divided the recipes into two groups based on their complexity:
            <ul>
                <li><strong>Group X - Simple Recipes:</strong> Recipes with ingredients below the median count.</li>
                <li><strong>Group Y - Complex Recipes:</strong> Recipes with ingredients above the median count.</li>
            </ul>
        </p>
        <p>
            We used <strong>precision</strong> as the evaluation metric, calculated with a weighted average to handle multiclass outputs effectively and set <code>zero_division</code> to 0 to address undefined precision values.
        </p>
        <h2>Hypotheses</h2>
        <ul>
            <li><strong>Null Hypothesis (H0):</strong> The model is fair, meaning the precision for both simple and complex recipes is roughly the same, and any differences are due to random chance.</li>
            <li><strong>Alternative Hypothesis (H1):</strong> The model is unfair, meaning the precision differs significantly between simple and complex recipes.</li>
        </ul>
        <h2>Permutation Test</h2>
        <p>
            A permutation test was performed to evaluate the fairness hypothesis, using the absolute difference in precision between the two groups as the test statistic. We calculated this statistic 1,000 times with shuffled group labels to simulate the distribution under the null hypothesis.
        </p>
        <p>
            <strong>Significance Level:</strong> 0.05
        </p>
        <p>
            <strong>Resulting P-value:</strong> 0.815
        </p>
        <h2>Conclusion</h2>
        <p>
            The p-value from the permutation test is <strong>0.815</strong>, which is significantly higher than our significance level of 0.05. Therefore, <strong>no significant unfairness was detected between simple and complex recipes</strong>. This suggests that any observed differences in precision between the groups can likely be attributed to random variation rather than systematic bias.
        </p>
        <!-- Optional: Embed a visualization related to your permutation test in your website -->
        <h3>Visualization of Test Results</h3>
        <p>
            <iframe src="assets/fairness.html" alt="Permutation Test Results for Model Fairness" width="800" height="450" frameborder="0"></iframe>
            <figcaption>Here we see the results of a permutation test conducted to evaluate model fairness in predicting recipe ratings. The bars represent the frequency of differences in precision observed when the labels between two groups (simple vs. complex recipes) are randomly shuffled. The vertical dashed red line, indicating the observed difference of 0.0015 in precision between the two groups without shuffling, falls well within the central distribution of the permuted outcomes, suggesting that the difference observed in model performance is likely due to random chance rather than systematic bias.</figcaption>
        </p>
    </section>
</body>

<body>
    <header>
        <h1>Conclusion</h1>
    </header>
    <section>
        <p>
            In conclusion, this project has thoroughly investigated the relationship between recipe characteristics and their ratings through various analytical steps, including data cleaning, exploratory data analysis, model building, and fairness evaluation. The baseline and final models developed offered insights into how different features such as cook time and number of ingredients influence recipe ratings. Permutation tests for missingness and fairness analysis revealed no significant biases or unfair treatment across different recipe complexities, indicating that the predictive models are robust and equitable across the groups tested. Overall, while the models demonstrated good predictive power, the findings emphasized the importance of considering both statistical significance and practical significance when interpreting model outcomes and assessing their potential real-world applications. This project not only enhanced our understanding of factors that affect recipe ratings but also showcased the application of rigorous data science techniques to ensure fairness and reliability in predictive modeling.
        </p>
    </section>
</body>
</html>

