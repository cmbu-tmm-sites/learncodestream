---
title: "Git"
---

The Git endpoint provides configuration for use in [Pipelines](/pipelines/#pipeline-configuration), [CI Tasks](/pipelines/tasks/ci), [Kubernetes Tasks](/pipelines/tasks/kubernetes), [VMware Cloud Template Tasks](/pipelines/tasks/cloud-template), and [Git Triggers](/triggers/git). A Git Endpoint provides access to a specific branch of a specific repository.

* **Project** - endpoints are assigned to a Project to provide scope of access
* **Type** - Git
* **Name** - a name to identify the Git Endpoint
* **Description** - description of the Git Endpoint
* **Mark restricted** - if enabled, only Code Stream or Project Administrators can execute Pipelines using this endpoint
* **Cloud proxy** - (vRA Cloud only) the Cloud Proxy appliance through which the endpoint should communicate
* **Git server type** - GitHub, GitLab, Bitbucket, GitHub Enterprise, GitLab Enterprise, or Bitbucket Enterprise
* **Repo URL** - URL of the repository to add ([see this blog post for more detail](https://blogs.vmware.com/management/2020/11/configuring-git-endpoints-and-webhooks-for-vrealize-automation-code-stream.html))
* **Branch** - Git branch to use
* **Authentication Type** - Private Token or Password
    * **Username** - Username to authenticate to the Git repository
    * **Password** - Password to authenticate to the Git repository
    * **Private token** - API token to authenticate to the Git repository

{{< img src="git-endpoint.png" alt="Adding a Git Endpoint configuration" >}}

{{< hint warning >}}
* When adding an endpoint URL you'll be prompted to view and accept the certificate.
* You can validate the configuration using the VALIDATE button.
* You should create [Secret Variables](/configure/variables) to store your user credentials.
{{< /hint >}}

## Links and References
* [Configuring Git Endpoints and WebHooks for vRealize Automation Code Stream](https://blogs.vmware.com/management/2020/11/configuring-git-endpoints-and-webhooks-for-vrealize-automation-code-stream.html)