# recipes-ratings-analysis
This repository contains a final project for the DSC 80 course at UC San Diego

Step 3:

NMAR Analysis:

Statement on NMAR: In the context of our dataset, which includes various attributes of recipes like 'rating', 'cook_time', 'ingredients', etc., it is plausible to consider that some missingness, particularly in the 'rating' column, could be NMAR. This hypothesis arises from the possibility that users might choose not to rate recipes based on subjective experiences or biases that are not captured in the data. For instance, if a recipe is too complex or requires hard-to-find ingredients, users might not complete it and thus not leave a rating, and these factors are not directly recorded in the dataset.
Reasoning: If users do not rate a recipe because they never attempted it, the missingness in 'rating' depends on unobserved factors related to the recipe's perceived complexity or ingredient accessibility. This kind of missingness would be NMAR as the likelihood of the data being missing depends on the unobserved data itself.
Additional Data for MAR Conversion: To potentially convert this NMAR scenario into an MAR (Missing At Random) scenario, additional data could be collected on user engagement with the recipe page, such as time spent on the page, clicks on the ingredient list, or whether the user added the recipe to a collection or shopping list. Collecting data on whether the user has rated similar recipes (in terms of complexity or cuisine type) might also help explain the missingness.


Step 6:

1. Prediction Problem and Type:

Prediction Problem: The objective is to classify recipes into one of five rating categories based on available pre-rating information.
Type of Prediction: Multiclass classification. This approach is apt for predicting which of the several rating categories a recipe will fall into based on its characteristics.
2. Response Variable:

Response Variable: The 'rating' of a recipe, categorized into 1, 2, 3, 4, or 5 stars. Using ratings as categorical data allows for precise classification into predefined quality levels.
3. Evaluation Metric:

Metric Choice: Accuracy and F1-Score. Accuracy will be the primary metric to determine the overall effectiveness of the classifier across all categories. However, given the likely imbalance among the categories (some ratings may be more common than others), the F1-Score, which balances precision and recall, will also be crucial.
Comparison: While accuracy gives a straightforward percentage of correct predictions, F1-Score provides a better measure of the model's performance in terms of balancing false positives and false negatives, which is important in an unbalanced dataset.
