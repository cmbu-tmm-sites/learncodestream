---
title: "Email"
---

The Email endpoint provides configuration for sending [Pipeline Notifications](/Pipelines/#notifications), [Task Notifications](/Pipelines/Tasks/#task-notifications), and [User Operation](/User-Operations) notifications.

* **Project** - endpoints are assigned to a Project to provide scope of access
* **Type** - Email
* **Name** - a name to identify the Email Endpoint
* **Description** - description of the Email Endpoint
* **Mark restricted** - if enabled, only Code Stream or Project Administrators can execute Pipelines using this endpoint
* **Cloud proxy** - (vRA Cloud only) the Cloud Proxy appliance through which the endpoint should communicate
* **Sender's addresss** - the address to send the email from
* **Encryption method** - TLS, SSL or NONE
* **Outbound host** - FQDN or IP address of the SMTP host
* **Outbound port** - Port of the SMTP host
* **Outbound protocol** - protocol for sending, SMTP or POP3
* **Outbound username** - Username to authenticate with the outbound host
* **Outbound password** - Password to authenticate with the outbound host

{{< img src="email-endpoint.png" alt="Adding an Email Endpoint configuration" >}}

{{< hint warning >}}
* You can validate the configuration using the VALIDATE button.
* You should create [Secret Variables](/Configure/Variables/) to store your user credentials.
{{< /hint >}}