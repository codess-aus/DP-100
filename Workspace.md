# Set up an Azure Machine Learning Workspace (30-35%)
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

With a **Machine Learning compute cluster**, you can easily create a single or multi-node compute instance. A Machine Learning compute cluster is the only type supported by Azure Machine Learning studio to associate a Machine Learning designer training pipeline.

**Azure Databricks** is an Apache Spark-based environment in the Azure cloud. It can be used as a target with an Azure Machine Learning pipeline, but you cannot set it as a target in Azure Machine Learning designer.

**Azure HDlnsight** is a platform for big-data analytics. It provides Apache Spark, which can be used to train your model, but you cannot set it as a target in Azure Machine Learning designer.

Azure Virtual Networks serve as security boundaries between your Azure resources and the Internet. You can control inbound and outbound access to or from an Azure Virtual Network by defining security rules that act like network firewall rules. To ensure that only required communications from the Internet are allowed, you should define an inbound security rule.

Security rules include an option to identify groups of Azure cloud resource nodes (IP addresses) using service tags. This allows you to define security rules without having to manually identify the IP addresses for Azure resources that you want to allow to access your virtual network. As Azure Machine Learning relies on other Azure resources and services, you must ensure that a security rule is created using the BatchNodeManagement service tag.

The BatchNodeMnagement service tag requires a destination port range of 29876 to 29877. This allows core Azure resources required for machine learning processes to communicate with resources in your Azure Virtual Network.

The AzureMachineLearning service tag is only required if you use Azure-based compute targets. If you use your own compute targets, 
this service tag is not required.

Outbound security rules control resource access initiated from resources within your Azure Virtual Network.

You should run the az ml workspace sync-keys command right after you change the keys of a storage account that is associated to an Azure ML workspace, as it could take up to an hour before the workspace is updated with the new keys. You can use this CLI command to force the update and get the workspace operational.

The az ml workspace share command lets you share the workspace with users if you need to provide access to the workspace. 

The az ml workspace update command lets you modify the workspace attributes.

The az ml workspace create command lets you create a new workspace.

Azure Machine Learning workspaces can be provisioned as one of two editions, Basic or Enterprise, and the edition determines which features will be available for a workspace. You define the machine learning workspace edition when the workspace is created. You can also upgrade any existing Basic edition to Enterprise edition at any time.

Basic or Enterprise edition can use notebooks to create and run experiments. A notebook is essentially a development environment that has been specialized for data science tasks. Unlike a traditional object-oriented coding environment, notebooks support features such as data visualization and equation writing.

The most popular notebook application is Jupyter Notebook, which supports popular data science programming languages such as Python and R.

Enterprise edition is required to create pipelines using Azure Machine Learning Designer. Azure Machine Learning pipelines are workflows that represent a series of machine learning tasks. Pipeline tasks can be executed independently from the underlying data, and you can register new datasets for each pipeline run, if necessary. While Enterprise edition is required for this task, you can still create and manage pipelines using Azure Machine Learning SDK with the Basic edition.

Basic or Enterprise edition can be used to share compute instances. A compute instance is a single Azure-homed virtual machine (VM). Azure Machine Learning compute instances are highly scalable cloud compute resources, which support multiple CPUs and large amounts of RAM based on the VM size you select at deployment.

