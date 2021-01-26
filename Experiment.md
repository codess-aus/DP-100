# Run Experiments and Train Models (25-30%)

## Create models by using Azure Machine Learning Designer
* create a training pipeline by using Azure Machine Learning designer
* ingest data in a designer pipeline
* use designer modules to define a pipeline data flow
* use custom code modules in designer

## Run training scripts in an Azure Machine Learning workspace
* create and run an experiment by using the Azure Machine Learning SDK
* configure run settings for a script
* consume data from a dataset in an experiment by using the Azure Machine Learning SDK

## Generate metrics from an experiment run
* log metrics from an experiment run
* retrieve and view experiment outputs
* use logs to troubleshoot experiment run errors

## Automate the model training process
* create a pipeline by using the SDK
* pass data between steps in a pipeline
* run a pipeline
* monitor pipeline runs

The **scikit-learn estimator** provides a simple way of launching an SKLearn training job on a compute target. It is implemented through the scikit-learn class, which can be used to support single-node CPU training.

Azure Machine Learning pipeline modules can validate, analyze, and transform your data to ensure your models are accurate. As you link pipeline modules, you control what data flows from one module to the next in your workflow.

**Select Columns in Dataset module** to identify the columns that should be processed and sent to the next pipeline element. By default, no columns are selected, and you will receive an error indicating that a value is required until you select at least one column.

The Select Columns in Dataset module supports several methods for identifying columns. You can select columns by name, type, or column index. As part of this process, you can define conditions that can filter your data based on type. For example, you could create a condition to exclude all string column types.

Select Column in Dataset is used to specify which columns are included in the next activity of the training pipeline. It will not allow you to remove rows that do not contain values.

**Clean Missing Data module**: You use the Clean Missing Data module to ensure that your data is as complete as possible prior to machine learning processing. When configuring this module, you need to specify the columns that contain missing values that you need to modify. You can configure the module to remove the entire row when the revenue column is empty. This keeps the rows in the original dataset, but the removed rows are not to be used in the model training.

A substitution value is an explicit value that is used to replace missing values. For example, you may replace missing values with a zero.

**SMOTE** is a statistical technique used to append number of cases to your dataset and ensure balance for the new samples created. This technique can be used to remove imbalance of a certain class in your dataset.

**Normalize Data module** is used to normalize columns within the dataset to eliminate bias that might be caused by large differences in the unit of values present in a column.You can normalize column values in such cases to fall between O and 1.

*Normalization* is a technique that is often applied as part of data preparation for machine learning. You would change the numeric data in the columns to use a common scale without distorting differences in the range of values or losing information.

Normalize Data allows you to configure all columns that contain numerical data to have the same scale without losing information. This will allow the training step to eliminate bias that could be associated with higher values because of certain column value units.

**Partition and Sample module**. This module helps create partition of the source dataset and maintain the same ratio of values. This is useful to reduce the size of the dataset and not eliminate imbalance of the source data. This module performs sampling on a dataset and 
analyzes the data without losing meaning.

**Split Data module**. The Split Data module is used to divide the dataset into two distinct sets based on the splitting mode provided. This is useful when training models by creating a training set and a testing set.

**Split Data module**. This module is used when you need to separate data into training and testing sets. You can customize the way data is divided. The module also provides options to randomize data selection.

**Join Data module**. This module is used to merge two datasets using a database-style join operation.

**Clip Values module**. This module allows you to replace data values that are above or below a specified threshold with a mean, a constant, or other substitute value.

**Inference cluster**. In order to host a real-time web service endpoint, you would have to create a cluster consisting of an Azure Kubernetes Service (AKS) instance or Azure Container Instance (ACI) managed by Azure. AKS is recommended for production use, while ACI is used primarily for small models or for development/testing purposes. This is the only type of cluster that is supported for deploying an 
inference pipeline as a hosted real-time service.

Compute instance, compute cluster, and attached compute are not supported to run inference pipelines as a real-time service. These clusters are more suited to host training and batch pipelines.

Specify a virtual network and ensure **head and worker nodes** can communicate with each other. Training video game machine learning models uses a process known as reinforcement learning (RL). RL machine learning agents take actions and then observe the results as a way of seeking rewards. Because RL is compute intense, it is typically performed across multiple compute nodes, known as head and worker nodes. In Azure Machine Learning, RL requires that you specify a virtual network that does not block the ports that nodes need to communicate.

You create a file dataset to reference the unstructured file or files you want to use in your machine learning experiments. In machine learning experiments, a FileDataset may be downloaded to compute targets or stored elsewhere and mounted to the experiment.

The **Estimator class** can be used when a predefined machine learning framework estimator does not already exist in Azure Machine Learning. For reinforcement learning, Azure Machine Learning provides the ReinforcementLearningEstimator class.

**SKLearn class** is used when running Scikit-learn training scripts. Scikit-learn is a Python-based machine learning library that only supports single-node compute targets.

When a new workspace is created, it contains a *default datastore*, **workspaceblobstore**. In order to retrieve the default datastore, you can use the **get_default_datastore** Workspace method. The workspaceblobstore datastore cannot be removed from the workspace.

You can also create a reference to workspaceblobstore using the datastore class. You can use the get method from the datastore class to retrieve a datastore by name. The following code retrieves a datastore named workspaceblobstore:

    my_datastore = Datastore.get(workspaceblobstore) 

**set_default_datastore method**: You can use this command to set a new default datastore.

All workspaces include an automatically registered blob container and file share. The file share - **workspacefilestore** - is used to store notebooks.

Azure Machine Learning allows you to track multiple metrics for your experiments. These metrics are stored in the experiment's **run record** for later retrieval and analysis, and the same metric can be logged within a run more than once. The run.log method can be used to log string or numerical scalar values and accepts three parameters, the metric name, the value to be logged, and an optional description.

The Experiment.submit method can be configured with the show_output parameter to enable local logging during the training process.

The Experiment.start_logging() enables logging for run-related data within the experiment. This will not show the logs generated during the training process.

The ComputeTarget.wait_for_completion method configures logging during a compute target creation. This will not show the logs generated during the training process.

The services.get_logs() enables logs to be retrieved for a previously deployed web service. The logs may contain detailed information about a past run, but they do not show the logs generated during the training process.

You plan to configure logging for an experiment that explores data associated with gender distribution within organizations across the world. The experiment must draw a box plot of genders by country. You need to use the appropriate logging method to render the plot for the experiment run object.
**log_image()** This method logs a .PNG image file or a matplotlib plot to the run. These images will be visible and comparable in the run record.

**log_table()** This method can be used to log a dictionary object to the run with the given name. This method will not render a plot.
**log()** This method is used to log a numerical or a string value to the run with a given name. This method will not render a plot.
**log_list()** This method is used to log a list of values to the run with a given name. This method will not render a plot.
**log_row()** This method creates a metric with multiple columns. Each named parameter generates a column with the value specified. This method will not render a plot.

**get_file_names()** function. This function will list all the files that are associated with the experiment run object. 
**get_status()** function is used to fetch the status of the last run.
**get_details_with_logs()** This function is used to get the status of the last run, along with log file contents. 
**get_details()** This function is used to get the definition, status information, current log files, and other details of the run.

