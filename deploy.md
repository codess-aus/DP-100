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