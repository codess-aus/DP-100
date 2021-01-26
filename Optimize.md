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

**AUC_weighted** is the correct metric to evaluate unbalanced datasets. It measures the area under the curve with consideration to the mean for each class, weighted by the number of true instance evaluated in each class.

Set featurization to **auto** if you want Automated ML to identify the features. Normalization and scaling are feature engineering transformations that the Automated ML experiment will conduct.

The **get_output** method returns the best pipeline based on the primary metric when no parameters are specified.

The **summary** method gets a table containing a summary of all algorithms attempted, as well as their scores.

The **get_runs** method allows the experiment to retrieve a reference to a given execution. This code will fail if executed with the AutoMLRun class.

The **get_metrics** method returns the metrics logged against the run. It does not provide details on the best run from an experiment.

**MaxAbsScaler** ensures that each feature is scaled by its maximum absolute value.

**PCA** ensure linear dimensionality reduction. It uses singular value decompositions of the data and reduces the dimensional space.

**StandardScaleWrapper** ensures that the features are standardized by altering the dataset, removing the mean, and scaling to unit variance.
