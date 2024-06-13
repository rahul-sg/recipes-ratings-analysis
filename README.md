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

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prediction Model for Recipe Ratings</title>
</head>
<body>
    <header>
        <h1>Predicting Recipe Ratings</h1>
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

<html lang="en">
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
</html>

