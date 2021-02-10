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

Security rules include an option to identify groups of Azure cloud resource nodes (IP addresses) using service tags. This allows you to define security rules without having to manually identify the IP addresses for Azure resources that you want to allow to access your virtual network. As Azure Machine Learning relies on other Azure resources and services, you must ensure that a *security rule* is created using the **BatchNodeManagement** service tag.

The **BatchNodeMnagement** service tag requires a *destination port range of 29876 to 29877*. This allows core Azure resources required for machine learning processes to communicate with resources in your Azure Virtual Network.

The AzureMachineLearning service tag is only required if you use Azure-based compute targets. If you use your own compute targets, 
this service tag is not required.

Outbound security rules control resource access initiated from resources within your Azure Virtual Network.

You should run the az ml workspace sync-keys command right after you change the keys of a storage account that is associated to an Azure ML workspace, as it could take up to an hour before the workspace is updated with the new keys. You can use this CLI command to force the update and get the workspace operational.

The az ml workspace **share** command lets you share the workspace with users if you need to provide access to the workspace. 

The az ml workspace **update** command lets you modify the workspace attributes.

The az ml workspace **create** command lets you create a new workspace.

Azure Machine Learning workspaces can be provisioned as one of two editions, Basic or Enterprise, and the edition determines which features will be available for a workspace. You define the machine learning workspace edition when the workspace is created. You can also upgrade any existing Basic edition to Enterprise edition at any time.

Basic or Enterprise edition can use notebooks to create and run experiments. A notebook is essentially a development environment that has been specialized for data science tasks. Unlike a traditional object-oriented coding environment, notebooks support features such as data visualization and equation writing.

The most popular notebook application is Jupyter Notebook, which supports popular data science programming languages such as Python and R.

**Enterprise edition** *is required to create pipelines using Azure Machine Learning Designer*. Azure Machine Learning pipelines are workflows that represent a series of machine learning tasks. Pipeline tasks can be executed independently from the underlying data, and you can register new datasets for each pipeline run, if necessary. While Enterprise edition is required for this task, you can still create and manage pipelines using Azure Machine Learning SDK with the Basic edition.

Basic or Enterprise edition can be used to share compute instances. A compute instance is a single Azure-homed virtual machine (VM). Azure Machine Learning compute instances are highly scalable cloud compute resources, which support multiple CPUs and large amounts of RAM based on the VM size you select at deployment.

You can assign a custom role to the Azure ML workspace using the following options: 
* The **az ml workspace share CLI** command. You can install the Azure ML CLI and provide the role along with the users UPN to assign the role to the user. This will allow you to assign a custom role to the Azure ML workspace.
* Assign the role from the portal using the **Access Control (IAM) screen for the workspace**. You can use the IAM screen for the workspace resource. This will allow you to assign a custom role to the Azure ML workspace.
* **The az role assignment create CLI command**. You can use Azure CLI to assign a role to the workspace resource.

* You cannot assign a role using the Azure ML CLI update command. The update command lets you configure the attributes about the workspace, not about the role.
* You should not assign the role from the portal using the Access Control (IAM) screen for the resource group. You cannot assign the role to a resource group since the custom role is scoped for Azure ML workspace resources.

l. az **extension add** -n azure-cli-ml 
2. az **group create** --name (resource-group-name> --location 
3. az ml **workspace create** -w cworkspace-name> -g cresource-group-name» 

* The first Step should be to *register the Machine Learning extension to run the az ml commands*.
* Then you should *create the resource group* where the Machine Learning workspace will reside.
* Finally, you should use the az ml CLI command to *create the workspace* in the resource group created in the second Step.

**az ml workspace list** command: This command just lists any existing Azure Machine Learning workspaces currently present in the Azure subscription.
**ml workspace update** command. This command allows updates to an existing workspace and does not create a workspace.

An Azure Machine Learning workspace is tightly integrated with Azure Event Grid. While Azure Event Hub is designed for ingesting large 
amounts of data that can be used to glean business intelligence, Event Grid is focused on discrete events generated by applications and aids in application automation.

Event Grid supports several event endpoint destinations, including web hooks. Webhooks enable applications to receive real-time data from a server or service. When a webhook is triggered, Event Grid sends a notification to a preregistered Uniform Resource Identifier (URI) using HTTP.

A real-time endpoint is the port-to-service mapping that is created when you deploy a web service. As part of deploying a real-time
endpoint, you are required to specify a compute target. Once the real-time endpoint has been deployed, applications and services can consume the endpoint in the same way as they would any other REST API.

A service principal (SP) is any directory object that can be used for authentication. Once an SP is created, it can be used in Azure Machine Learning to facilitate token-based authentication.

Azure Event Hub is a stand-alone platform that, like Azure Monitor, can ingest logging and other information from a variety of Azure Services. However, Event Hub is focused on data analysis to discover actionable insights, sometimes referred to as business intelligence.

Authentication to your Azure Machine Learning workspace is based on Azure Active Directory (Azure AD) for most things. In general, there three authentication workflows that you can use when connecting to the workspace:

* Interactive: You use your account in Azure Active Directory to either directly authenticate, or to get a token that is used for authentication. Interactive authentication is used during experimentation and iterative development. Interactive authentication enables you to control access to resources (such as a web service) on a per-user basis.

* Service principal: You create a service principal account in Azure Active Directory, and use it to authenticate or get a token. A service principal is used when you need an automated process to authenticate to the service without requiring user interaction. For example, a continuous integration and deployment script that trains and tests a model every time the training code changes.

* Managed identity: When using the Azure Machine Learning SDK on an Azure Virtual Machine, you can use a managed identity for Azure. This workflow allows the VM to connect to the workspace using the managed identity, without storing credentials in Python code or prompting the user to authenticate. Azure Machine Learning compute clusters can also be configured to use a managed identity to access the workspace when training models.

An Azure Machine Learning compute cluster:
Azure Machine Learning compute clusters are scalable machine learning platforms that consist of one or more CPU or GPU nodes. Cluster resources can be shared with other users in the machine learning workspace. Compute clusters support:

* AutoML, which is used to automate the process of training and tuning machine learning models.
* Machine learning pipelines, which are machine learning workflows.
* Azure Machine Learning designer, which facilitates graphical, drag-and-drop creation of machine learning models.

An Azure Machine Learning compute target is a computing resource where machine learning experiments can be run. Azure supports a variety of compute target types, including your local computer, a remote virtual machine (VM), and Azure Machine Learning compute clusters. You can create an Azure Machine Learning compute target cluster using the az ml computetarget create amlcompute command.

Compute clusters are highly scalable targets that consist of one or more compute nodes, and a cluster can scale up or down dynamically based on workload. You can control the maximum number of nodes in the cluster by using the required --max-nodes parameter. By specifying the minimum number of nodes as O, you can ensure that all active nodes will be terminated when jobs are not running. This will prevent Azure compute costs from accruing during idle times.

The idle seconds parameter allows you to control how long a compute cluster must be idle before unneeded resources are deprovisioned. This allows you to ensure that intermittent pauses in machine learning jobs do not cause unnecessary waiting time as nodes are provisioned and deprovisioned.

A compute instance is a single Azure-based VM used for machine learning experiments. You can use compute instances to support automated machine learning (AutoML) and machine learning pipelines.

An Azure Data Factory (ADF) compute target is used to create machine learning pipelines. ADF facilitates ingestion and batch processing of data in order to provide predictive analytics.

Use Azure ML compute cluster to tune hyperparameters using Azure ML designer. This is the only training target that is supported by Azure ML designer for Automated ML jobs running hyperparameter tuning.

Select Remote VM when using your own virtual machine (VM) for hyperparameter tuning. Azure ML supports bringing in a VM that is reachable by Azure ML. You can have the VM attached to your virtual network. This provides the benefit of leveraging environments like conda or Python as well as running training in a containerized environment.

Select Azure HDlnsight to use Apache Spark to train your models. Azure HDlnsight provides a pre-configured environment with Apache Spark.

Select Azure ML compute cluster to auto scale instances for models based on compute requirements. Azure ML compute cluster can be configured to scale up when training jobs are submitted.

After logging in, you see a list of subscriptions associated with your Azure account. The subscription information with isDefault: true is the currently activated subscription for Azure CLI commands. This subscription must be the same one that contains your Azure Machine Learning workspace. You can find the subscription ID from the Azure portal by visiting the overview page for your workspace. You can also use the SDK to get the subscription ID from the workspace object. For example, Workspace.from_config().subscription_id.

To select another subscription, use the az account set -s <subscription name or ID> command and specify the subscription name or ID to switch to. For more information about subscription selection, see Use multiple Azure Subscriptions.

*Deleting a workspace does not delete the application insight, storage account, key vault, or container registry used by the workspace.* 

Azure Machine Learning workspaces can be provisioned as one of two editions, **Basic** or **Enterprise**, and the edition determines which features will be available for a workspace. You define the machine learning workspace edition when the workspace is created. You can also upgrade any existing Basic edition to Enterprise edition at any time.

**Basic or Enterprise edition can use notebooks to create and run experiments**. A notebook is essentially a development environment that has been specialized for data science tasks. Unlike a traditional object-oriented coding environment, notebooks support features such as data visualization and equation writing. 

The most popular notebook application is Jupyter Notebook, which supports popular data science programming languages such as Python and R.

**Enterprise edition is required to create pipelines using Azure Machine Learning Designer**. Azure Machine Learning pipelines are workflows that represent a series of machine learning tasks. Pipeline tasks can be executed independently from the underlying data, and you can register new datasets for each pipeline run, if necessary. While Enterprise edition is required for this task, you can still create and manage pipelines using Azure Machine Learning SDK with the Basic edition. 

**Basic or Enterprise edition can be used to share compute instances**. A compute instance is a single Azure-homed virtual machine (VM). Azure Machine Learning compute instances are highly scalable cloud compute resources, which support multiple CPUs and large amounts of RAM based on the VM size you select at deployment.

