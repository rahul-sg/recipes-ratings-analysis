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



# recipes-ratings-analysis
This repository contains a final project for the DSC 80 course at UC San Diego
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NMAR Analysis in Recipe Ratings</title>
</head>
<body>
    <header>
        <h1>Understanding NMAR in Recipe Ratings</h1>
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

Step 5:

1. Prediction Problem and Type:

Prediction Problem: The objective is to classify recipes into one of five rating categories based on available pre-rating information.
Type of Prediction: Multiclass classification. This approach is apt for predicting which of the several rating categories a recipe will fall into based on its characteristics.
2. Response Variable:

Response Variable: The 'rating' of a recipe, categorized into 1, 2, 3, 4, or 5 stars. Using ratings as categorical data allows for precise classification into predefined quality levels.
3. Evaluation Metric:

Metric Choice: Accuracy and F1-Score. Accuracy will be the primary metric to determine the overall effectiveness of the classifier across all categories. However, given the likely imbalance among the categories (some ratings may be more common than others), the F1-Score, which balances precision and recall, will also be crucial.
Comparison: While accuracy gives a straightforward percentage of correct predictions, F1-Score provides a better measure of the model's performance in terms of balancing false positives and false negatives, which is important in an unbalanced dataset.


Step 6:

Model Description: The baseline model is a logistic regression classifier trained to predict the categorical ratings of recipes. It uses two types of features: one quantitative ('cook_time') and one nominal ('tags', which has been one-hot encoded).

Performance Evaluation:

  Metrics Used: Accuracy and F1-Score.

  Performance Results: The model achieved an accuracy of 72.52911% and an F1-Score of 60.98069% on the test set (replace XX with actual values from the notebook output).

  Assessment: The current model's performance can be considered a basic benchmark. The accuracy may provide a quick glance at how often the model predicts correctly, but the F1-Score is particularly valuable due to the potential class imbalance across different ratings. Depending on these metrics, the model’s effectiveness in a real-world scenario can be preliminary evaluated.
This baseline model serves as a foundational step. It is straightforward, making it a good starting point for understanding basic relationships in the data before moving on to more complex models in the subsequent steps.

</html>

