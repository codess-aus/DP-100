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

**RandomParameterSampling** object and specify a parameter_space dictionary. The random parameter sampling method allows you to define a parameter search space and Azure Machine Learning will randomly choose hyperparameters from within this space. Random parameter sampling supports early termination.

Both **Random** and **Grid** sampling configurations will let you associate an early cancellation policy.

Hyperparameters are used to control the training process for machine learning models, and these parameters can have a significant impact on how a trained model performs. Azure Machine Learning includes a hyperparameter tuning service which supports three parameter sampling methods, and the method selected determines whether early termination is supported.

**BanditPolicy** object. A BanditPolicy object allows you to create an early termination policy which will terminate training jobs that are not likely to result in an accurate machine learning model. As part of a BanditPolicy configuration, you can specify how frequently jobs are evaluated and the amount of slack between the best performing job and the job being evaluated. This can greatly reduce training job runtimes and conserve compute resources.

A **BanditPolicy** object allows you to create an early termination policy which will terminate training jobs that are not likely to result in an accurate machine learning model. As part of a BanditPolicy configuration, you can define the amount of slack between the best performing job and the job being evaluated.

**Bayesian sampling**method selects hyperparameters based on the performance of previous runs. The Bayesian sampling method does not support early termination.

**Bayesian sampling**. This sampling method selects hyperparameters based on the performance of previous runs. The Bayesian sampling method does not support early termination. When using Bayesian parameter sampling, you should set early_termination_policy = 
None, or leave the early_termination_policy parameter out.

**BayesianParameterSampling** will try to intelligently pick values for hyperparameters based on a provided parameter space. It will not allow you to specify specific discrete values.

A **truncation selection** policy is an early termination policy that cancels a percentage of low-performing runs. Each run's performance is evaluated using a primary metric, and the percentage of jobs to cancel is specified when you define the policy. As part of its calculations, a truncation selection policy considers previous performance for runs with less run time.

**GridParameterSampling** allows you to set discrete values for your hyperparameters.

**RandomParameterSampling** the tuning parameter values are selected randomly over a parameter space provided. It will not allow you to specify specific discrete values. Random sampling is used to control the hyperparameter space that is used during model training.

A **median stopping** policy calculates running averages across training runs that cancels any runs whose performance falls below the median of the running average.

You can allow other users to run the pipeline using custom inputs by publishing the pipeline. To do this, you must first create a pipeline parameter using the **PipelineParameter** class, which allows to specify the default value of the pipeline parameter.

Automated machine learning in Azure Machine Learning uses the primary metric you define to optimize model training. The metrics you can configure are dependent on the machine learning task type, such as regression or classification.

The **accuracy** metric can be used for *classification* tasks, and it calculates the proportion of instances that have been correctly classified.

As you want your model to be as accurate as possible, you should set the *primary metric goal* to **MAXIMIZE**, meaning Azure Machine Learning will attempt to maximize the model's classification accuracy.

**Spearman correlation** calculates the monotonic relationship between two values. For example, two stock tickers may have a monotonic relationship where stock A's price decreases when stock B's price increases.

Set the *primary metric goal* to **MINIMIZE**. This metric goal is useful when you are tracking experiment errors and you want to minimize the number of errors a model reports.

Explainers, also known as interpretability techniques, are used to interpret or explain machine learning models. These explanations are used by data scientists to understand how a machine learning model works. For example, if a model is used to predict which type of person is inclined to commit a crime, its users may want to understand how the model makes that prediction. TabularExplainer is used with tabular datasets.

TabularExplainer is categorized as a meta explainer, which means that it chooses an explainer based on how the referenced model is structured. For example, TabularExplainer will use LinearExplainer when a linear model is being evaluated.

A **global surrogate** is meant to be an interpretable approximation of a **black box** model. Black box models are those for which no explanation exists, which means that the public does not know how the model makes its predictions. Once a surrogate model is trained, the mimic explainer interpretability technique can be used to interpret the model. global surrogate model and use mimic explainer to explain the model. A global surrogate is meant to be an interpretable approximation of a black box model. Black box models are those for which no explanation exists, which means that the public does not know how the model makes its
predictions. Once a surrogate model is trained, mimic explainer can be used to interpret the model.

**PFI**. Features are data fields that are used to train a model. If you need to determine which fields - or features - have the largest impact on a model's predictions, you should use an interpretability technique that calculates and tracks feature importance. *Azure Machine Learning* supports the PFI for this purpose. PFI randomly shuffles features during model training and then calculates the impact on the model's performance.

**Azure Machine Learning SDK** to generate *feature importance*. Features are data fields that are used to train a model. If you need to determine which fields or features have the largest impact on a model's predictions, you should use an interpretability technique that calculates and tracks feature importance. Azure Machine Learning supports the **Permutation Feature Importance Explainer (PFI)** for this purpose. **PFI** randomly shuffles features during model training, and then calculates the impact on the model's performance.

**SHAP linear explainer**. SHAP is a model-specific interpretability technique used for linear models. SHAP explainers use calculates based on coalitional game theory. SHAP is not model-agnostic and is used for tree-based models.

**multi-label image classification** project. Multi-label projects are used when multiple labels might be applied to a single image. For example, if an image included a dog and a cat, it may receive a label for each, dog and cat.

**Explainers**, also known as **interpretability techniques**, are used to interpret or explain machine learning models. These explanations are used by data scientists to understand how a machine learning model works. For example, if a model is used to predict which type of person is inclined to commit a crime, its users may want to understand how the model makes that prediction. In order to create an explainer for your local machine learning model, you need to install the azureml-interpret Python package.

**Security rules** allow you to isolate and protect your experiments by controlling access to Azure Machine Learning resources. If you are going to implement security rules, you must ensure that a security rule is created using the BatchNodeManagement service tag. This allows Azure Machine Learning to interact with other Azure services.

You create a file dataset to reference the file or files you want to use in your machine learning experiments. The from_files method is used to identify the path and file specification that will be used when the dataset is created.

Azure Machine Learning provides the capability to run experiments on different compute targets without requiring scripts to be rewritten. This is done by creating a run configuration, which serves as a template for a training environment. The easiest way to generate a run configuration is to use the az ml folder attach command.

When configuring a pipeline using Azure Machine Learning SDK, you can define automated machine learning settings that control how the experiment is run. These settings are typically defined in dictionary format and passed to an AutoMLConfig object. If the **featurization** parameter is set to auto, *input data will automatically be preprocessed, and missing values will be handled*. To ensure this doesn't happen, the featurization parameter should be added to the automl_experiment data dictionary and configured with a value of off.

The **RunDetails** class can be used in a Jupyter notebook to view how model training is progressing.

Deploy to an **Azure Machine Learning compute cluster** target for models that perform **batch inference**. In Azure Machine Learning, **inference** is also known as **model scoring**. Azure Machine Learning compute clusters are scalable machine learning platforms consisting of one or more CPU or GPU nodes.

Compute clusters can scale from zero to hundreds of nodes, depending on workload. Compute clusters support the use of low-priority virtual machines (VMS), which do not have guaranteed availability. Using low-priority VMS can help reduce machine learning costs.

AKS target could theoretically be used to perform batch inference. However, **AKS** is designed for *compute-intensive operations at scale*, while **batch inference** requires compute resources on an *intermittent* basis. By contrast, batch inference requires the scalability that an Azure Machine Learning compute instance web service would not provide.

You should deploy to **AKS** target for models that perform *real-time inference*. In Azure Machine Learning, *inference is also known as model scoring*. Such models are trained on a data set and can analyze the data in real-time to provide predictions. For example, you could train a model on stock market data. Once trained, you could use the model to analyze stock prices in real-time and then make predictions on future prices.

Inference clusters are built using Azure AKS and are sometimes referred to AKS clusters.

Azure machine learning compute clusters cannot be used for real-time inference because they use low-priority VMS and may not scale to the load required. Additionally, VM availability is not guaranteed, thus the provided service is not real-time. Similarly, Azure Machine Learning compute instance web services cannot be used for real-time inference because they typically lack hardware acceleration capabilities and do not scale to the workloads involved in real-time inference.

You should deploy to an Azure Machine Learning compute instance web service target for models that need to be tested and debugged. Azure Machine Learning compute instances are highly scalable cloud compute resources. Compute instances support AutoML and machine learning pipelines. Testing and debugging is best done on local resources or using low-cost cloud compute resources. The per-hour costs associated with Azure Machine Learning compute clusters and AKS make them poor candidates for testing and debugging.

Data drift is the phenomenon where the data used to train a model diverges from later model input data. This can occur for a variety of reasons, and the concern is that, if left unchecked, data drift can lead to model performance degradation over time.

You can define a **dataset monitor** if you want to *monitor for statistical changes and data drift* in your datasets. Each dataset monitor requires a baseline dataset, which is typically the dataset that was used to initially train the model. You must also specify a target dataset, which is where new data is stored and 
compared with the baseline dataset. This target dataset must have the **timeseries trait** set, which is typically done by adding a timestamp column. Once the dataset monitor is created and configured, you can view drift analysis information in the Azure Machine Learning portal.

**Azure Event Hub** is a stand-alone platform that, like Azure Monitor, can ingest logging and other information from a variety of Azure Services. However, Event Hub is focused on data analysis to discover actionable insights, sometimes referred to as business intelligence.

The **ScriptRunConfig** class is used to create an object that contains both training environment configuration information, as well as a training script. This ScriptRunConfig object can be used to initiate a fully configured training run as part of a machine learning experiment.

**Logging** functions to your pipeline with the Execute Python Script module. This module can be added to a drag-and-drop designer pipeline to run Python code. This is useful in cases where an existing Azure Machine Learning designer module does not provide the functionality you need for your experiments.

**TabularExplainer** calls one of the three **SHAP explainers** underneath **(TreeExplainer, DeepExplainer, or KernelExplainer)**.
TabularExplainer automatically selects the most appropriate one for your use case, but you can call each of its three underlying explainers directly.

