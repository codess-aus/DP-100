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