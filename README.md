# DP-100 Exam DP-100: Designing and Implementing a Data Science Solution on Azure

## Set up an Azure Machine Learning Workspace (30-35%)
* create an Azure Machine Learning workspace
* configure workspace settings
* manage a workspace by using Azure Machine Learning studio

## Manage data objects in an Azure Machine Learning workspace
* register and maintain datastores
* create and manage datasets

## Manage experiment compute contexts
* create a compute instance
* determine appropriate compute specifications for a training workload
* create compute targets for experiments and training

[My Notes on Setting up an Azure Machine Learning Workspace]()

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

[My Notes on Running Experiments and Training Models]()

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

[My Notes on Optimizing and Managing Models]()

# Deploy and Consume Models (20-25%)

## Create production compute targets
* consider security for deployed services
* evaluate compute options for deployment

## Deploy a model as a service
* configure deployment settings
* consume a deployed service
* troubleshoot deployment container issues

## Create a pipeline for batch inferencing
* publish a batch inferencing pipeline
* run a batch inferencing pipeline and obtain outputs

## Publish a designer pipeline as a web service
* create a target compute resource
* configure an Inference pipeline
* consume a deployed endpoint

[My Notes on Deploying and Consuming Models]()