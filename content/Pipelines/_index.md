---
title: "Pipelines"
weight: 500

---
A Pipeline is the primary mechanism for sequencing all the tasks that need to be performed, and is composed of one or more Stage, with one or more tasks in each stage.

## General Pipeline Settings

The pipeline settings allow you to set the pipeline name, concurrency, description, icon and tags.{{<hint info>}}Being able to change the concurrency of the pipeline is often useful if you're using shared resources that either don't have the capcity to host multiple running executions, or there are resources that cannot be shared{{</hint>}}
{{< img src="/images/pipeline-general-settings.png" alt="Pipeline general settings" >}}

## Pipeline configuration

When editing a Pipeline there are four tabs to configure:

{{< tabs "pipelineConfig" >}}
{{< tab "Workspace" >}} 
The workspace tab configures the environment in which the pipeline runs
* **Host** specifies a [Docker endpoint](/Configure/Endpoints/docker) on which [CI tasks](/Pipelines/Tasks/ci) and [Custom Integrations](/Custom-Integrations) will execute
* **Builder image URL** configures the container image that will be used for CI tasks or Custom Integrations. You can specify using the just an official image (e.g. `python`), the image and a tag (e.g. `python:3.10.0a6-alpine`) or a full URL (e.g. `projects.registry.vmware.com/antrea/prom-prometheus:v2.19.3`){{< hint warning >}}
The container image can be almost any image but it needs to have `wget` or `curl` in order to download and install the Code Stream CI Agent, which is installed when the container is spun up. 
{{< /hint >}}
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
The Model tab is where you configure the Stages and Tasks of the pipeline - it's where you spend most of your time when creating and editing pipelines.

- A [Stage](/Pipelines/Stages) is an encapsulation mechanism for tasks and are used for grouping the individual task execution statuses and results. 
- A [Task](/Pipelines/Tasks) performs individual actions based on its type and configuration.  Tasks can deploy [VMware Cloud Templates](Tasks/cloudtemplate), and perform actions on configured endpoints, or more generic tasks such as prompting for user interations with [User Operation](/User-Operations), polling a 3rd party data source with the [Poll](/Pipelines/Tasks/poll/) task, or even perform a REST call.

![Pipeline Model Configuration](images/pipeline-model-config.png)
{{< /tab >}}
{{< tab "Output" >}} 
Outputs can be mapped to values produced by tasks in a pipeline and can be useful when you're nesting pipelines using the [Pipeline task](/Pipelines/Tasks/pipeline) to return the results to the parent pipeline.

![Pipeline Output Config](images/pipeline-output-config.png)
{{< /tab >}}
{{< /tabs >}}

## Variables in Pipelines
Most configurable fields within a Pipeline can also use [Variables], references to Input parameters, the output of other tasks or general pipeline properties by using a reference.

These can be accessed using by typing `$`, which will bring up the auto-completion:
<!-- ![Reference auto-completion](images/pipeline-references.gif) -->
{{< img src="/images/pipeline-references.gif" alt="Reference auto-completion" >}}

Referring back to previous tasks is done using a heirarchy that matches the structure of the pipeline, for example: `${Build Stage.Build Task.output.exports.variableName}` would refer to the value of a variable called `variableName` that was exported from a task called `Build Task` in the stage `Build Stage`.

Tasks return their output as JSON, and it's often useful to look at a previously executed task to find the correct path to an output variable - if you look at the [Execution]() of a Pipeline and examine the task details, you can click "View Output JSON" and use the "Path finder" option to discover the correct path:
![Find the correct output path](images/pipeline-find-path.gif)

## Notifications

The notifications tab allows you to configure notifications for pipeline events (completion, waiting for [user interaction](), failure, cancellation, and starting) using either an [Email endpoint](/Configure/Endpoints/email), [Jira endpoint](/Configure/Endpoints/jira), or by creating a Webhook with a POST, PUT or PATCH payload.

### More
{{< toc-tree >}}


### Reference
* [Creating and using pipelines in vRealize Automation Code Stream](https://docs.vmware.com/en/vRealize-Automation/8.3/Using-and-Managing-CodeStream/GUID-A2BB3A55-E42D-428C-8F7F-9EBE4AECD5FD.html)

