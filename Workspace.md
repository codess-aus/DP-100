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

