---
title: "Email"
---

The Email endpoint provides configuration for sending [Pipeline Notifications](/Pipelines/#notifications) and [Task Notifications](/Pipelines/Tasks/#task-notifications), as well as [User Operation](/User-Operations) notifications.

* **Project** - endpoints are assigned to a Project to provide scope of access
* **Type** - Email
* **Name** - a name to identify the Email Endpoint
* **Description** - description of the Email Endpoint
* **Mark restricted** - as described in the [Projects](/Configure/Projects) page, if the Endpoint is marked as restricted only an Administrator can execute a Pipeline that uses it
* **Sender's addresss** - the address to send the email from
* **Encryption method** - TLS, SSL or NONE
* **Outbound host** - FQDN or IP address of the SMTP host
* **Outbound port** - Port of the SMTP host
* **Outbound protocol** - protocol for sending, SMTP or POP3
* **Outbound username** - Username to authenticate with the outbound host
* **Outbound password** - Password to authenticate with the outbound host

{{< img src="email-endpoint.png" alt="Adding an Email Endpoint configuration" >}}

You can validate the configuration using the VALIDATE button. As with all sensitive information, you should create [Secret Variables](/Configure/Variables/) to store your user credentials.