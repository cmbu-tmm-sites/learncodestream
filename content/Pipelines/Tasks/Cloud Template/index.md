---
title: "VMware Cloud Template"
---
The VMWare Cloud Template task can be used to Create, Update, Delete, and Rollback Deployments in vRealize Automation Cloud Assembly.

**API token** - the only common setting across all actions in this task is the API token. This is an API token with permissions to vRealize Automation Cloud Assembly API to perfom the Action on a Deployment. You can enter the token directly in the field, however you should use a Secret or Restricted variable to avoid the token being visible in pipeline logs. The Generate Token button will open a form to generate an API token from credentials you enter

## Actions
There are four different actions you can perform against the VMware Cloud Templates

{{< tabs "Cloud Template Task Actions" >}}
{{< tab Create >}}
Create a new deployment from a VMware Cloud Template

* **Deployment Name** - the name of the deployment to create (you can use the `${executionId}` to provide a unique ID if required)
* **Cloud template source**
    * select a **Cloud template** and **Version** directly from vRealize Automation Cloud Assembly, -or-
    * select a **Git** endpoint and **File path** to the blueprint YAML
* **Parameters** - blueprint inputs and default values will be loaded into the table. You can keep the defaults, use [Pipeline Variables](/Pipelines/#variables-in-pipelines), or manually populate the answers
{{< img src="cloud-template-create.png" alt="Create a new deloyment">}}
{{< /tab >}}

{{< tab Update >}}
Update an existing deployment with an updated VMware Cloud Template

* **Select existing deployments** - populates Deployment Name with a dropdown of existing Cloud Assembly deployments
* **Allow deletion during update** - depending on what has changed in the Cloud Template, the blueprint may need to delete and re-create components, enable this option to allow deletion
* **Deployment Name** - the name of the deployment to update
* **Cloud template source**
    * select a **Cloud template** and **Version** directly from vRealize Automation Cloud Assembly, -or-
    * select a **Git** endpoint and **File path** to the blueprint YAML
* **Parameters** - blueprint inputs and default values will be loaded into the table. You can keep the defaults, use [Pipeline Variables](/Pipelines/#variables-in-pipelines), or manually populate the answers

{{< img src="cloud-template-update.png" alt="Update an existing deployment" >}}
{{< /tab >}}

{{< tab Delete >}}
Delete an existing deployment
* **Select existing deployments** - populates Deployment Name with a dropdown of existing Cloud Assembly deployments
* **Deployment Name** - the name of the deployment to delete
{{< img src="cloud-template-delete.png" alt="Delete an existing deployment" >}}

{{< /tab >}}

{{< tab Rollback >}}
Roll an existing deployment back to a previous version of a VMware Cloud Template
* **Select existing deployments** - populates Deployment Name with a dropdown of existing Cloud Assembly deployments
* **Deployment Name** - the name of the deployment to roll back
* **Rollback Version** - the version of the deployment to roll back to

{{< img src="cloud-template-rollback.png" alt="Roll back an existing deployment" >}}

{{< /tab >}}
{{< /tabs >}}