# Optimize and Manage Models (20-25%)

## Use Automated ML to create optimal models
* use the Automated ML interface in Azure Machine Learning studio
* use Automated ML from the Azure Machine Learning SDK
* select pre-processing options
* determine algorithms to be searched
* define a primary metric
* get data for an Automated ML run
* retrieve the best model

## Use Hyperdrive to tune hyperparameters
* select a sampling method
* define the search space
* define the primary metric
* define early termination options
* find the model that has optimal hyperparameter values

## Use model explainers to interpret models
* select a model interpreter
* generate feature importance data

## Manage models
* register a trained model
* monitor model usage
* monitor data drift

**AUC_Weighted** metric. AUC_Weighted is a metric that can be used for classification models. AUC_Weighted is the arithmetic mean of the score for each class, weighted by the number of true instances in each class. This works well when the datasets are imbalanced.

**accuracy** metric. This metric provides the effciency of the model against the training data. However, you should not use this metric when the dataset is imbalanced, because it may provide inconsistent weight to certain rows of the dataset.

**normalized_root_mean_squared_error** metric. This metric is well suited for the evaluation of regression algorithms. This metric is not optimal for classification model evaluation.

**log_loss** metric. This metric is used for logistic regressions and similar extensions, such as neural networks. This metric is not optimal for classification model evaluation.