---
title: "Pipelines"
weight: 500
---
A Pipeline is the primary mechanism for sequencing all the tasks that need to be performed, and is composed of one or more Stage, with one or more tasks in each stage. When editing a Pipeline there are four tabs to configure:

{{< tabs "pipelineConfig" >}}
{{< tab "Workspace" >}} 
The workspace tab configures the environment in which the pipeline runs
* **Host** specifies a [Docker endpoint](/Configure/Endpoints/docker) on which [CI tasks](/Pipelines/Tasks/ci) and [Custom Integrations](/Custom-Integrations) will execute
* **Builder image URL** configures the container image that will be used for CI tasks or Custom Integrations. You can specify using the just an official image (e.g. `python`), the image and a tag (e.g. `python:3.10.0a6-alpine`) or a full URL (e.g. `projects.registry.vmware.com/antrea/prom-prometheus:v2.19.3`)
* **Image Registry** selects the [Docker Registry endpoint](/Configure/Endpoints/dockerregistry) to use to pull the **Builder image** - if the registry requires credentials to pull an image you can specify them as part of the endpoint and those will be used.
* **Working directory** is the directory within a container image that will be used when running commands in a [CI task](/Pipelines/Tasks/ci) - more often than not, you can leave this blank to default to `/build`
* **Cache** 
* **Environment Variables** can be used to pass environment variables to a container (similar to the `-e VAR_NAME="value"` flag in the `docker run` command)
* **CPU limit** if a CI task requires significant resources, the container's allocated CPU can be increased - it's not often required
* **Memory limit** if a CI task requires significant resources, container's allocated Memory can be increased - it's not often required
* **Git clone** - if the pipeline is triggered by a [Git webhook](/Triggers/Git), [CI tasks](/Pipelines/Tasks/ci) will automatically clone the Git repository. {{< hint warning >}}
Note: You will need to configure the pipeline Inputs with the Git auto-inject parameters for this to work!
{{< /hint >}}

![Pipeline Workspace Configuration](images/pipeline-workspace-config.png)
{{< /tab >}}
{{< tab "Input" >}} 
![Pipeline Input Configuration](images/pipeline-input-config.png)
{{< /tab >}}
{{< tab "Model" >}}
- A [Stage](/Pipelines/Stages) is an encapsulation mechanism for tasks and are used for grouping the individual task execution statuses and results. 

- A [Task](/Pipelines/Tasks) performs individual actions based on its type and configuration.  Tasks can deploy [VMware Cloud Templates](Tasks/cloudtemplate), and perform actions on configured endpoints, or more generic tasks such as prompting for user interations with [User Operation](/User-Operations), polling a 3rd party data source with the [Poll](/Pipelines/Tasks/poll/) task, or even perform a REST call.
 {{< /tab >}}
{{< tab "Output" >}} 
Outputs can be mapped to values produced by tasks in a pipeline and can be useful when you're nesting pipelines using the [Pipeline task](/Pipelines/Tasks/pipeline) to return the results to the parent pipeline.
![Pipeline Output Config](images/pipeline-output-config.png)
{{< /tab >}}
{{< /tabs >}}


### More
{{< toc-tree >}}


### Reference
* [Creating and using pipelines in vRealize Automation Code Stream](https://docs.vmware.com/en/vRealize-Automation/8.3/Using-and-Managing-CodeStream/GUID-A2BB3A55-E42D-428C-8F7F-9EBE4AECD5FD.html)

