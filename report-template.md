# Report: Predict Bike Sharing Demand with AutoGluon Solution
#### NAME HERE
Arian Abdi
## Initial Training
### What did you realize when you tried to submit your predictions? What changes were needed to the output of the predictor to submit your results?
When submitting predictions, I encountered a NameError due to the submission DataFrame submission_new_features not being defined. Additionally, a No space left on device error occurred while saving the submission CSV. These issues required:

Defining or reloading the submission format correctly (e.g., from a sample submission).

Freeing up disk space by deleting large intermediate files or old model artifacts.

### What was the top ranked model that performed?
After training, the top-performing model based on validation RMSE was WeightedEnsemble_L3 with a score of -33.156950, which outperformed all individual models.

## Exploratory data analysis and feature creation
### What did the exploratory analysis find and how did you add additional features?
Exploratory analysis showed that some numerical features were correlated and had potential interaction effects. Additional features were created by:

Binning continuous variables.

Adding ratios and differences between selected columns.

Encoding categorical features with domain-informed groupings.

### How much better did your model preform after adding additional features and why do you think that is?
The model improved from an RMSE of approximately -34.0 to -33.2. The improvement came from better capturing nonlinear interactions and domain-specific patterns, which enriched the feature space and improved learning efficiency for tree-based models.
## Hyper parameter tuning
### How much better did your model preform after trying different hyper parameters?
Hyperparameter optimization with hyperparameter_tune_kwargs improved the base model slightly. For example, the tuned LightGBM variant (T1) improved to -33.858996, which was slightly better than its untuned counterpart.

### If you were given more time with this dataset, where do you think you would spend more time?
Ensemble optimization: Custom ensembling rather than relying solely on AutoGluon’s default.

Advanced feature selection: Using SHAP to eliminate uninformative features.

Outlier detection: Handle anomalous training points that degrade performance.

Time/resource efficient HPO: Tuning under tighter constraints using Bayesian optimization.

### Create a table with the models you ran, the hyperparameters modified, and the kaggle score.
| model         | hpo1                     | hpo2               | hpo3       | score      |
| ------------- | ------------------------ | ------------------ | ---------- | ---------- |
| initial       | default                  | default            | default    | \~-34.7    |
| add\_features | feature\_engineering=yes | default            | default    | \~-33.9    |
| hpo           | tuned\_LightGBM/CatBoost | early\_stopping=on | rounds=100 | **-33.16** |

## Summary
The project demonstrated the importance of structured feature engineering and iterative tuning in boosting AutoML model performance. Starting from a basic AutoGluon pipeline, the performance improved significantly after thoughtful feature enhancements and targeted hyperparameter optimization. The best model was an ensemble leveraging LightGBM, CatBoost, and tree-based models. Further gains could be realized with custom ensembling, outlier handling, and computationally optimized tuning.
