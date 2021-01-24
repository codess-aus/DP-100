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

Azure Machine Learning pipeline modules can validate, analyze, and transform your data to ensure your models are accurate. As you link pipeline modules, you control what data flows from one module to the next in your workflow. You can use the **Select Columns in Dataset module** to identify the columns that should be processed and sent to the next pipeline element. By default, no columns are selected, and you will receive an error indicating that a value is required until you select at least one column.

The Select Columns in Dataset module supports several methods for identifying columns. You can select columns by name, type, or column index. As part of this process, you can define conditions that can filter your data based on type. For example, you could create a condition to exclude all string column types.

**Clean Missing Data module**: You use the Clean Missing Data module to ensure that your data is as complete as possible prior to machine learning processing. When configuring this module, you need to specify the columns that contain missing values that you need to modify.

A substitution value is an explicit value that is used to replace missing values. For example, you may replace missing values with a zero.

**SMOTE** is a statistical technique used to append number of cases to your dataset and ensure balance for the new samples created. This technique can be used to remove imbalance of a certain class in your dataset.

**Normalize Data module** is used to normalize columns within the dataset to eliminate bias that might be caused by large differences in the unit of values present in a column.You can normalize column values in such cases to fall between O and 1.

*Normalization* is a technique that is often applied as part of data preparation for machine learning. You would change the numeric data in the columns to use a common scale without distorting differences in the range of values or losing information.

**Partition and Sample module**. This module helps create partition of the source dataset and maintain the same ratio of values. This is useful to reduce the size of the dataset and not eliminate imbalance of the source data.

**Split Data module**. The Split Data module is used to divide the dataset into two distinct sets based on the splitting mode provided. This is useful when training models by creating a training set and a testing set.

**Split Data module**. This module is used when you need to separate data into training and testing sets. You can customize the way data is divided. The module also provides options to randomize data selection.

**Join Data module**. This module is used to merge two datasets using a database-style join operation.

**Clip Values module**. This module allows you to replace data values that are above or below a specified threshold with a mean, a constant, or other substitute value.

