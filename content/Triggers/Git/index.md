---
title: "Git"
weight: 720
---

## Activity

The activity tab shows a log of the Git events that have been recieved by Code Stream. You can see details of the Git commit details, repository and messages, as well the [Pipeline](/pipeline) that has been executed in response and it's status. you can also click directly through to the [execution](/executions) of the Pipeline.

{{< img src="git-trigger-activity.png" alt="Git Trigger Activity" >}}

## Webhook Configuration

When creating a new Webhook for Git, the following options are available:

* **Project** - webooks are assigned to a Project to provide scope of access
* **Name** - a name to identify the Webhook configuration
* **Description** - description of the Webhook configuration
* **Endpoint** - the Git Endpoint on which to configure the Webhook
* **Branch** - the Git Branch on which the webhook should be configured
* **Secret token** - a secret token that will be used to identify the webhook is valid
* **File** - configure PLAIN or REGEX file filters
    * **Inclusions** - include any files that match a PLAIN search string or REGEX
    * **Exclusions** - exclude any files that match a PLAIN search string or REGEX
    * **Prioritise Exclusion** - if enabled, files that match both the include and exclude filters will be excluded
* **Trigger** - configuration of the webhook on the Git endpoint
    * **For Git** - Trigger the webhook when a Push is made to the repository branch, or when a Pull Request is made against the branch
    * **API token** - a vRealize Automation API token that has permissions to execute the Pipeline configured in the trigger
    * **SSL verification** - if enabled, will enable SSL verification for the webhook (the repository must trust the vrealize automation ssl certificate)
    * **Pipeline** - the Code Stream Pipeline to execute
    * **Execution trigger delay** - time to wait from recieving the event until executing the pipeline

{{< hint info >}}When you click create, vRealize Automation will connect to the [Git Endpoint]() using the credentials configured in that endpoint. It will automatically configure a new webhook on the repository, using the settings specified, and will use the API token to authenticate webhooks back to vRealize Automation. The API token is stored as a Repository secret.{{< /hint >}}

{{< tabs "Git Webhook Config" >}}
{{< tab "Trigger Configuration" >}}
{{< img src="git-trigger-config.png" alt="Git Trigger Configuration" >}}
{{< /tab >}}
{{< tab "GitLab - Configured Webhook" >}}
{{< img src="git-trigger-gitlab.png" alt="Git Trigger Configuration" >}}
{{< /tab >}}
{{< /tabs >}}


## Links and References
* [Configuring Git Endpoints and WebHooks for vRealize Automation Code Stream](https://blogs.vmware.com/management/2020/11/configuring-git-endpoints-and-webhooks-for-vrealize-automation-code-stream.html)