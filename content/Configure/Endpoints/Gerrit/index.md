---
title: "Gerrit"
---

The Gerrit endpoint provides configuration for use in the [Gerrit Trigger](/Triggers/Gerrit/).

* **Project** - endpoints are assigned to a Project to provide scope of access
* **Type** - Gerrit
* **Name** - a name to identify the Gerrit Endpoint
* **Description** - description of the Gerrit Endpoint
* **Mark restricted** - as described in the [Projects](/Configure/Projects) page, if the Endpoint is marked as restricted only an Administrator can execute a Pipeline that uses it
* URL - URL of the Gerrit server
* Username - Username to authenticate to the Gerrit server
* Password - Password to authenticate to the Gerrit server
* Private key - Private key (RSA) to authenticate to the Gerrit server
* Pass phrase - Pass phrase to decrypt the Private key

{{< img src="gerrit-endpoint.png" alt="Adding a Gerrit Endpoint configuration" >}}

You can validate the configuration using the VALIDATE button. As with all sensitive information, you should create [Secret Variables](/Configure/Variables/) to store your user credentials.