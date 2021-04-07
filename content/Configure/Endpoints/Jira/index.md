---
title: "Jira"
icon: "notification"
---

The Jira endpoint provides configuration for sending [Pipeline Notifications](/Pipelines/#notifications) and [Task Notifications](/Pipelines/Tasks/#task-notifications).

* **Project** - endpoints are assigned to a Project to provide scope of access
* **Type** - Jira
* **Name** - a name to identify the Jira Endpoint
* **Description** - description of the Jira Endpoint
* **Mark restricted** - if enabled, only Code Stream or Project Administrators can execute Pipelines using this endpoint
* **Cloud proxy** - (vRA Cloud only) the Cloud Proxy appliance through which the endpoint should communicate
* **URL** -  the URL of the Jira instance
* **Username** - the username to authenticate to the Jira instance
* **Password** - the password to authenticate to the Jira instance

{{< img src="jira-endpoint.png" alt="Adding an Jira Endpoint configuration" >}}

{{< hint warning >}}
* When adding an endpoint URL you'll be prompted to view and accept the certificate.
* You can validate the configuration using the VALIDATE button.
* You should create [Secret Variables](/Configure/Variables/) to store your user credentials.
{{< /hint >}}