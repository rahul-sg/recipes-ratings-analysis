<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Recipe Ratings Analysis</title>
</head>
<body>
    <header>
        <h1>Welcome to Our Recipe Ratings Analysis!</h1>
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
</html>



# recipes-ratings-analysis
This repository contains a final project for the DSC 80 course at UC San Diego

Step 3:

Not Missing At Random (NMAR)
NMAR occurs when the probability of missingness in a data point is related to the value of the missing data itself, possibly in conjunction with observed data. For example, if people do not rate recipes that are too complex or time-consuming, and complexity or time required is not recorded, the missingness in ratings is related to this unobserved complexity.

In our dataset, examining columns like rating could reveal insights into NMAR. For instance:

Rating: Missing ratings might not be random but related to users' dissatisfaction or disappointment. If a user attempts a recipe and it turns out poorly, they might opt not to rate it to avoid leaving a negative review. Alternatively, users might skip rating because the recipe was unremarkable. Both scenarios suggest that the missing ratings could depend on the satisfaction level, which is not observed in the dataset.

Cook Time and Ingredients: Recipes with long cook times or requiring unusual ingredients might often go unrated. Users who plan but do not follow through with cooking such recipes (due to the high effort or ingredient unavailability) might not leave a rating. This missingness could also be NMAR if users avoid rating because they never attempted the recipe, influenced by the unobserved perceived difficulty or availability of ingredients.


Statement on NMAR: In the context of our dataset, which includes various attributes of recipes like 'rating', 'cook_time', 'ingredients', etc., it is plausible to consider that some missingness, particularly in the 'rating' column, could be NMAR. This hypothesis arises from the possibility that users might choose not to rate recipes based on subjective experiences or biases that are not captured in the data. For instance, if a recipe is too complex or requires hard-to-find ingredients, users might not complete it and thus not leave a rating, and these factors are not directly recorded in the dataset.

Reasoning: If users do not rate a recipe because they never attempted it, the missingness in 'rating' depends on unobserved factors related to the recipe's perceived complexity or ingredient accessibility. This kind of missingness would be NMAR as the likelihood of the data being missing depends on the unobserved data itself.
Additional Data for MAR Conversion: To potentially convert this NMAR scenario into an MAR (Missing At Random) scenario, additional data could be collected on user engagement with the recipe page, such as time spent on the page, clicks on the ingredient list, or whether the user added the recipe to a collection or shopping list. Collecting data on whether the user has rated similar recipes (in terms of complexity or cuisine type) might also help explain the missingness.


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

