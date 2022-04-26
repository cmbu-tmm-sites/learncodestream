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


The workspace tab configures the environment in which the pipeline runs. 

**Type** Tasks can execute on a [Kubernetes endpoint](/configure/endpoints/kubernetes) or a [Docker endpoint](/configure/endpoints/docker). Some configurations is common to both types of workspace, other parts are specific.
* **Kubernetes API Endpoint** specifies a [Kubernetes endpoint](/configure/endpoints/kubernetes) on which [CI tasks](/pipelines/tasks/ci) and [Custom Integrations](/custom-integrations) will execute
* **Host Endpoint** specifies a [Docker endpoint](/configure/endpoints/docker) on which [CI tasks](/pipelines/tasks/ci) and [Custom Integrations](/custom-integrations) will execute

**Builder image URL** is common accross both workspace types and configures the container image that will be used for CI tasks or Custom Integrations. You can specify using the just an official image (e.g. `python`), the image and a tag (e.g. `python:3.10.0a6-alpine`) or a full URL (e.g. `projects.registry.vmware.com/antrea/prom-prometheus:v2.19.3`)

{{< hint warning >}}The container image can be almost any image but it needs to have `wget` or `curl` in order to download and install the Code Stream CI Agent, which is installed when the container is spun up.{{< /hint >}}

**Image Registry** selects the [Docker Registry endpoint](/configure/endpoints/docker-registry) to use to pull the **Builder image** - if the registry requires credentials to pull an image you can specify them as part of the endpoint and those will be used.

{{< hint info >}}
#### Kubernetes workspace only
The following settings are available for the Kubernetes type workspace only

**Namespace** specifies a Kubernetes Namespace in which the Kubernetes Deployment running the container image will be created. If the Namespace does not already exist, then Code Stream will automatically create it.

**Proxy type** Code Stream communicates tasks with the CI Agent running on the container image Pod via a NodePort on the Kubernetes Worker, or a Load Balancer, however the NodePort requires each Kubernetes Node to be accessible to Code Stream. Most managed Kubernetes will not allow this, so you will need to specify Load Balancer instead.

* **Node port** if you select the Node port proxy type you can leave this value blank to use an ephemeral port number, or specify a port between 30000-32767 (for example if you are using a managed Kubernetes cluster or are in an environment where you need to open a firewall port). Any Pipeline with its workspace configured using the same Namespace and Node Port will re-use the Node Port, or you can specify a different combination to use a different port.

**Persistent Volume Claim** Code Stream will use this Persistent Volume Claim to store the logs and output of the CI Agent running on the container image Pod and persist them beyond the lifespan of a Pipeline run. If you do not specify a Persistent Volume Claim then an ephemeral volume type will be used.

{{< img src="images/kubernetes-workspace-options.png" alt="Kubernetes Workspace Options" >}}
{{< /hint >}}

**Working directory** is the directory within a container image that will be used when running commands (`workingDir`, by default) in a [CI task](/pipelines/tasks/ci) - more often than not, you can leave this blank to default to `/build`

**Cache** is accessible to each Pipeline run and can be used to cache files and folders that are common between Pipeline runs - for example if you download dependencies before building a Go project, those dependencies could be cached to speed up future executions of the same pipeline.

**Environment Variables** can be used to pass environment variables to a container (similar to the `-e VAR_NAME="value"` flag in the `docker run` command)

**CPU limit** if a CI task requires significant resources, the container's allocated CPU can be increased - it's not often required

**Memory limit** if a CI task requires significant resources, container's allocated Memory can be increased - it's not often required

**Git clone** - if the pipeline is triggered by a [Git webhook](/triggers/git), [CI tasks](/pipelines/tasks/ci) will automatically clone the Git repository. {{< hint warning >}}
You will need to configure  Pipeline Inputs with the Git auto-inject parameters for automatic cloning to work{{< /hint >}}

{{< img src="/images/pipeline-workspace-config.png" alt="Pipeline Workspace Configuration" >}}

{{< /tab >}}
{{< tab "Input" >}} 
{{< img src="/images/pipeline-input-config.png" alt="Pipeline Input Configuration" >}}
{{< /tab >}}
{{< tab "Model" >}}
The Model tab is where you configure the Stages and Tasks of the pipeline - it's where you spend most of your time when creating and editing pipelines.

- A [Stage](/pipelines/stages) is an encapsulation mechanism for tasks and are used for grouping the individual task execution statuses and results. 
- A [Task](/pipelines/tasks) performs individual actions based on its type and configuration.  Tasks can deploy [VMware Cloud Templates](tasks/cloudtemplate), and perform actions on configured endpoints, or more generic tasks such as prompting for user interations with [User Operation](/user-operations), polling a 3rd party data source with the [Poll](/pipelines/tasks/poll) task, or even perform a REST call.

{{< img src="/images/pipeline-model-config.png" alt="Pipeline Model Configuration" >}}
{{< /tab >}}
{{< tab "Output" >}} 
Outputs can be mapped to values produced by tasks in a pipeline and can be useful when you're nesting pipelines using the [Pipeline task](/pipelines/tasks/pipeline) to return the results to the parent pipeline.

{{< img src="/images/pipeline-output-config.png" alt="Pipeline Output Configuration" >}}
{{< /tab >}}
{{< /tabs >}}

## Variables in Pipelines
Most configurable fields within a Pipeline can also use [Variables], references to Input parameters, the output of other tasks or general pipeline properties by using a reference.

These can be accessed using by typing `$`, which will bring up the auto-completion:
<!-- ![Reference auto-completion](images/pipeline-references.gif) -->
{{< img src="/images/pipeline-references.gif" alt="Reference auto-completion" >}}

Referring back to previous tasks is done using a heirarchy that matches the structure of the pipeline, for example: `${Build Stage.Build Task.output.exports.variableName}` would refer to the value of a variable called `variableName` that was exported from a task called `Build Task` in the stage `Build Stage`.

Tasks return their output as JSON, and it's often useful to look at a previously executed task to find the correct path to an output variable - if you look at the [Execution]() of a Pipeline and examine the task details, you can click "View Output JSON" and use the "Path finder" option to discover the correct path:
![Find the correct output path](/images/pipeline-find-path.gif)

## Notifications

The notifications tab allows you to configure notifications for pipeline events (completion, waiting for [user interaction](), failure, cancellation, and starting) using either an [Email endpoint](/configure/endpoints/email), [Jira endpoint](/configure/endpoints/jira), or by creating a Webhook with a POST, PUT or PATCH payload.

{{< tabs "Notification Types" >}}
{{< tab Email >}}
{{< img src="images/email-notification.png" alt="Pipeline Email Notifications" >}}
{{< /tab >}}
{{< tab Ticket >}}
{{< img src="images/jira-notification.png" alt="Pipeline Jira Notifications" >}}
{{< /tab >}}
{{< tab Webhook >}}
{{< img src="images/webhook-notification.png" alt="Pipeline Webhook Notifications" >}}
{{< /tab >}}
{{< /tabs >}}

You can create a rich user experience with HTML templates, or custom formatting in your notifications:
* [Creating HTML email templates for vRealize Automation Code Stream](https://blog.v12n.io/creating-html-email-templates-for-vrealize-code-stream)
* [Creating Slack Notifications](/getting-started/slack-notifications)


### Reference
* [Creating and using pipelines in vRealize Automation Code Stream](https://docs.vmware.com/en/vRealize-Automation/8.3/Using-and-Managing-CodeStream/GUID-A2BB3A55-E42D-428C-8F7F-9EBE4AECD5FD.html)

### In this section