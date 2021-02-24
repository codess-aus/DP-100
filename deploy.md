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

Configure your VM size to the NCv2 series: In order for your model to run image classification deep learning model leveraging CUDA, you need to configure the VM that provides support for GPUs.

DSv2 series: DSv2 series VMS are general purpose VMS and don't support GPUs. For running image classification deep learning model leveraging CUDA, GPU-based graphic processing is recommended.

FS series VMs are compute optimized VMS and don't support GPUs. These are good for CPU intensive workloads. For running image classification deep learning model leveraging CUDA, GPU-based graphic processing is recommended.

Lsv2 series VMS are storaged optimized VMs. This type of VMS is good for high disk 10 operations like hosting databases. For running image classification deep learning model leveraging CUDA, GPU- based graphic processing is recommended.

An **inference cluster** can deploy trained models that will provide *real-time* predictive services at scale. In Azure Machine Learning, inference is also known as model scoring. Such models are trained on a data set and can analyze the data in real-time to provide predictions. For example, you could train a model on stock market data. Once trained, you could use the model to analyze stock prices in real-time and then make predictions on future prices. Inference clusters are built using Azure Kubernetes Service(AKS) and are sometimes referred to as **AKS clusters**.

Keywords: Inference Cluster = AKS Cluster = Realtime

**Compute clusters** cannot be used with models that offer predictive services because they use *low-priority VMS* and may *not scale* to the load required. Computer cluster *VM availability is not guaranteed*, thus the provided service is not real-time. 

**Attached compute** resources cannot be used for real-time inference because they do not scale to the workloads involved in real-time inference.
**Attached compute** can be used for Azure Databricks clusters. Attached compute supports linking to on-cloud Azure compute resources, including VMS and Azure Databricks clusters. Azure Databricks is a cloud-based Apache Spark-based analytics platform. **Databricks clusters** are often used to run *machine learning pipelines*. You might choose Azure Databricks if you are collaborating with other machine learning teams, or because it is based on the open-source Apache Spark ecosystem.

A **compute cluster** can support scalable, on-demand processing using low-priority VMs.

**Azure Machine Learning compute clusters** are scalable machine learning platforms consisting of one or more CPU or CPU nodes. Compute clusters can scale from zero to hundreds of nodes, depending on workload. *Compute clusters support the use of low-priority VMS, which do not have guaranteed availability*. Using low-priority VMS can help reduce machine learning costs.

Keywords: Compute Clusters scale but with low priority. Big but not real-time. Cheaper.

* AKS target could theoretically be used to Support scalable, on-demand processing. However, AKS is designed for compute-intensive operations at scale and is best suited for real-time predictive services.
* Attached compute should not be used to support scalable, on-demand processing because it does not provide scalability.
* Neither inference cluster nor compute clusters can use Azure Databricks clusters.

To deploy a model as a real-time web service using your *local* system, you must install Docker (on your *local* machine). Docker is a container creation and management platform that can be deployed on a variety of operating systems.

Models deployed locally as a web service will accept requests on an HTTP endpoint. Once your container has the required dependencies installed, you will need to define the port where the HTTP endpoint will listen for service requests. A container is a virtualized app that includes all the resources it needs to run, including file resources, dependencies, and services.

If you enable key-based authentication on your web service, all service connect attempts will be required to provide a valid Application Programming Interface (API) key prior to accessing the model.

When a machine learning model is deployed as a web service, a REST interface is defined, which client applications can use to consume the service. You determine the service endpoint by using the Azure Machine Learning SDK to retrieve the scoring_uri property of a Webservice object.

If the published model requires authentication, you will need to define an HTTP request header in your code that specifies bearer authentication. Once your code is complete, you can issue an HTTP POST request to the published service endpoint you discovered using the scoring_uri property.

The AmlComputeJobEvent log is just one of the logs that can be streamed to Azure Monitor. Information from this log is stored in the Azure Monitor AmlComputeJobEvents table. 

You can query the ExecutionState property to determine the state of a job.

AKS clusters are designed for heavy, real-time production workloads. One of the primary benefits of deploying to AKS is its support for autoscaling. This means that as workload increases or decreases, an AKS cluster can add or terminate cluster nodes.

An HTTP 503 Service Unavailable error indicates that the service is operational but it is unable to respond to requests. This often indicates that the server is overloaded and does not have the resources to process the request.

By default, AKS scales up when cluster utilization exceeds 70 percent. If there is a sudden increase in requests, the cluster may not be able to add nodes quickly enough to handle the requests. By reducing this threshold, you allow the cluster to scale up under lighter loads.

You can also modify the autoscale_max_replicas parameter. By default, an AKS cluster can scale up to 10 containers (nodes). By increasing this parameter, you can ensure that your cluster can handle a higher number of simultaneous requests.

You can also change the minimum number of replicas. This parameter defines the minimum number of nodes that should be online in an AKS cluster. The default value is 1. By increasing this parameter, you can ensure that the cluster always has enough resources to deal with spikes in requests.

An HTTP 504 error indicates that a request has timed out. You can increase the request timeout threshold from one minute if requests are timing out too quickly. However, this will not reduce the incidence of HTTP 503 errors.

Key authentication only for ACI compute targets. ACI allows you to package and deploy your machine learning models using easy-to-manage containers. A container is a virtualized app that includes all the resources it needs to run, including fle resources, dependencies, and services. **ACI only supports key authentication**. This means that if authentication is enabled for a model's web service endpoints, all requests must be authenticated using a predefined key. This is similar to many REST Application Programming Interfaces (APIs) which support API keys for authentication.

Key or token authentication for AKS compute targets. AKS supports highly scalable compute options for Azure Machine Learning experiments. In addition to supporting multiple-node clusters, AKS can be used for experiments that require hardware acceleration via GPI_J or Field-programmable Gate Arrays (FPGA). Finally, AKS can dynamically scale compute availability based on workload, Token-based authentication relies on temporary tokens. Once enabled, users or services that connect to deployed model must submit an Azure Machine Learning JSON Web Token in order to be allowed Each token has a limited lifetime, and expired tokens must be refreshed prior to making new calls.

Deploy a Model as a realtime service making sure it's accessible to end-users:

You should perform the following actions:
* Create a real-time inference pipeline.
* Create an inferencing cluster.
* Deploy the real-time endpoint.
* Test the real-time endpoint.

You should also create an inferencing cluster where the pipeline will be hosted.

You should create a real-time inference pipeline from the trained model. You need to create the inference pipeline to deploy the model as a web service. You can perform these first two steps in any order.

Then, you need to select the Deploy button in the designer view for the inference model to deploy the services. Once deployed, you should go to the test tab to ensure that the real-time endpoints are accessible by providing a data row, and click the Test button.

In Azure Machine Learning, **inference** is also known as **model scoring**. Such models are trained on a dataset and can analyze data in real-time or on-demand to provide predictions. A batch inference pipeline is used to score datasets on-demand via web service.

This web service is defined when you publish a pipeline, and an HTTP endpoint that external applications and services can consume is created. Azure Machine Learning allows you to publish multiple pipelines under the same endpoint. When this occurs, each published pipeline is assigned to a version number, which can be provided in REST API calls.

If you want to preserve an existing pipeline, and then you can create a new pipeline that implements your changes, you can then publish this new pipeline under your existing endpoint. 

Finally, you can test you new pipeline by including its version in your REST calls. You should not determine the ID of the default published pipeline. Every endpoint has one default pipeline. When you publish a new pipeline under an existing endpoint, you can choose to make it the default pipeline for that endpoint.

Create a parameter for your dataset: This option allows consumers to provide a dataset to your pipeline at runtime. This is useful in scenarios where a model is trained on a dataset but is used to formulate predictions on new data. You can parameterize a pipeline by using the dataset module.

Connect a dataset to the pipeline: You connect a dataset to a pipeline when you need to provide data input. This process is manual and does not occur automatically at runtime.

Publish the pipeline to a new endpoint: A web service is defined when you publish a pipeline, and an HTTP endpoint is created that external applications and services can consume.

The **Convert to Dataset module** is used to ensure that data normalization changes can be used in other pipelines. Input data to this module must be tabular.

Service Principal authentication can be used in scenarios when prompting a user for credentials is not feasible, such as when automated processes need to interact with a published pipeline. A service principal is any directory object that can be used for authentication. User accounts are considered service principals.

ParallelRunStep can be used to process large amounts of data in parallel. ParallelRunStep works by breaking up the data into batches that are processed in parallel.

PythonScriptStep is a basic, built-in step that is used to run a Python Script on a compute target. It takes a script name and other optional parameters, such as arguments for the script, compute target, inputs, and outputs. PythonScriptStep can be used to execute the scoring script; however, it will not run parallel instances partitioning the data.

AdlaStep works only with data stored in the default Data Lake Storage of the the Azure Data Lake Analytics account.

The **wait_for_completion** method is used to monitor the status and by default, it will stream the logs to the output determined by the sys.stdout configuration.

The **get_status** method retrieves the status of the run, however, it will not provide streaming logs while the pipeline is being executed.

The **get_graph** renders the graph of the pipeline run. 

The **get_steps** method lists the generated step runs. The method provides a list of all the pipeline steps that have completed or have started running.

You should use init() for any costly or common preparation for later inference. 
You should use run(mini_batch) to write code that would evaluate and append the outputs of the evaluation.

* You should perform training tasks only on an Azure Machine Learning compute cluster. 
* Azure Machine Learning compute clusters are scalable machine learning platforms consisting of one or more CPU or GPU nodes. 
* Compute clusters can scale from zero to hundreds of nodes, depending on workload. 
* Compute clusters support the use of low-priority virtual machines (VMS), which do not have guaranteed availability.
* Using low-priority VMS can help reduce machine learning costs. 
* Azure Machine Learning compute clusters can be used for training pipelines, but not for pipeline deployment because this functionality is not supported.

* You should perform training tasks only on an Azure Machine Learning compute instance. 
* A compute instance is a single Azure-homed virtual machine (VM). 
* Azure Machine Learning compute instances are highly scalable cloud compute resources, which support multiple CPUs and large amounts of RAM based on the VM size you select at deployment. 
* Unlike a compute cluster, a compute instance cannot scale down to zero, meaning that usage charges accrue unless you power off the VM. 
* Azure Machine Learning compute instances can be used for training pipelines, but not for pipeline deployment because this functionality is not supported.

* You should perform deployment only on AKS. 
* AKS clusters are designed for heavy, real-time production workloads. 
* One of the primary benefits of deploying to AKS is its support for autoscaling. This means that as workload increases or decreases, an AKS cluster can add or terminate cluster nodes. 
* In addition to supporting multiple-node clusters, AKS can be used for experiments that require hardware acceleration via GPU or Field-Programmable Gate Arrays (FPGAs).

In Azure Machine Learning, inference is also known as model scoring. Such models are trained on a dataset and can then analyze data in real-time to provide predictions. Once your pipeline has trained a model, you convert the training pipeline into a real-time inference pipeline. This adds the supporting Web Service Input and Web Service Output modules to your pipeline.

An endpoint is the port-to-service mapping that is created when you deploy a web service. As part of deploying a real-time endpoint, you are required to specify a compute target, and publishing an autoscaling inference pipeline is only supported on AKS inference clusters. If you have not created an AKS cluster prior to this step, you will need to define one before you can complete the deployment.

Once the real-time endpoint has been deployed, applications and services can access the endpoint as they would any other REST API.

A **Service Principal** is any directory object that can be used for authentication. Once an SP is created, it can be used in Azure Machine Learning to facilitate token-based authentication. As part of the creation process for an SP, a client secret is generated, which is comparable to a password. You can supply the client secret in an HTTP POST to retrieve an authentication token. This token, also known as a JSON Web Token (JWT), can then be used to authenticate with an Azure Machine Learning web service. By default, a JWT is valid for one hour, and must be refreshed when it expires.

In addition to token-based authentication, Azure Machine Learning also supports **key-based web-service authentication**. Keys, comparable to Application Programming Interface (API) keys, are statically generated. If a key needs to be replaced, you can use the **regen_key** method to regenerate authentication keys.

**get_keys** method is used to retrieve the primary and secondary authentication keys. You used keys to authenticate to an Azure Machine Learning web service that has been configured with key-based authentication.

**AciWebservice.deploy_configuration** to set auth_enabled to True. This method is used to enable key-based authentication on an Azure Container Instances (ACI) web service.

**Azure Stack Edge** is a hardware-as-a-service platform offered by Microsoft. As part of an Azure Stack Edge subscription, Microsoft provides a hardware-accelerated compute device that can process and analyze data collected by IOT devices before it is sent to the cloud. In addition to applying your machine learning models to IOT data, Stack Edge can filter, aggregate, and optimize data in order to reduce bandwidth requirements.

AKS supports highly scalable compute options for Azure Machine Learning experiments. In addition to supporting multiple-node clusters, AKS can be used for experiments that require hardware acceleration via GPU or Field-Programmable Gate Arrays (FPGA).

**Azure Machine Learning SDK** preview package and deploy your machine learning model as an app in Azure Functions. Once machine learning training is complete, you can create a Docker image based on the trained model. This model can then be deployed as an Azure Functions as containerized code.

The Publish button creates a REST endpoint to the pipeline that other users/developers/data scientists can make calls to. It provides an endpoint with a key-based authentication.

**NCv2 series**: In order for your model to run image classification deep learning model leveraging **CUDA**, you need to configure the VM that provides support for GPU's. 

**DSv2 series** VMS are **general purpose VMS** and dont support GPU's. 

**For running image classification deep learning model leveraging CUDA, GPU-based graphic processing is recommended.**

**FS series** VMS are **compute optimized** VMS and don't support GPU's. These are good for CPU intensive workloads.

**Lsv2 series** VMS are **storaged optimized** VMs. This type of VMS is good for high disk I0 operations like hosting databases.

You should create an **inference cluster** to deploy trained models that will provide **real-time predictive services at scale**. In Azure Machine Learning, inference is also known as model scoring. Such models are trained on a data set and can analyze the data in real-time to provide predictions. For example, you could train a model on stock market data. Once trained, you could use the model to analyze stock prices in real-time and then make predictions on future prices. 

**Inference clusters are built using Azure Kubernetes Service (AKS) and are sometimes referred to as AKS clusters**. 

**Compute clusters cannot be used with models that offer predictive services because they use low-priority VMS and may not scale to the load required**. Additionally, **inference clusters are used for real-time predictive services** and computer cluster VM availability is not guaranteed, thus the provided service is not real-time. Similarly, *attached compute resources cannot be used for real-time inference because they do not scale to the workloads involved in real-time inference*. 

You should create a **compute cluster to support scalable, on-demand processing using low-priority VMs**. Azure Machine Learning compute clusters are scalable machine learning platforms consisting of one or more CPU or CPU nodes. Compute clusters can scale from zero to hundreds of nodes, depending on workload. Compute clusters support the use of low-priority VMS, which do not have guaranteed availability. Using low-priority VMS can help reduce machine learning costs. 

AKS target could theoretically be used to Support scalable, on-demand processing. However, AKS is designed for compute-intensive operations at scale and is best suited for real-time predictive services. 

Attached compute should not be used to support scalable, on-demand processing because it does not provide scalability. 

You should use attached compute to use Azure Databricks clusters. Attached compute supports linking to on-cloud Azure compute resources, including VMS and Azure Databricks clusters. Azure Databricks is a cloud-based Apache Spark-based analytics platform. Databricks clusters are often used to run machine learning pipelines. You might choose Azure Databricks if you are collaborating with other machine learning teams, or because it is based on the open-source Apache Spark ecosystem. Neither inference cluster nor compute clusters can use Azure Databricks clusters. 

You should configure key authentication only for ACI compute targets. ACI allows you to package and deploy your machine learning models using easy-to-manage containers. A container is a virtualized app that includes all the resources it needs to run, including file resources, dependencies, and services. **ACI only supports key authentication**. This means that if authentication is enabled for a model's web service endpoints, all requests must be authenticated using a predefined key. This is similar to many REST Application Programming Interfaces (APIs) which support API keys for authentication.

You should configure **key or token authentication for AKS compute targets**. AKS supports highly scalable compute options for Azure Machine Learning experiments. In addition to supporting multiple-node clusters, AKS can be used for experiments that require hardware acceleration via CPU or Field-Programmable Gate Arrays (FPGA). Finally, AKS can dynamically scale compute availability based on workload. 

Token-based authentication relies on temporary tokens. Once enabled, users or services that connect to your deployed model must submit an Azure Machine Learning JSON Web Token in order to be allowed access. Each token has a limited lifetime, and expired tokens must be refreshed prior to making new calls. 
