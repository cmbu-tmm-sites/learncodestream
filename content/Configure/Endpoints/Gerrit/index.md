---
title: "Gerrit"
---

The Gerrit endpoint provides configuration for use in the [Gerrit Trigger](/Triggers/Gerrit/).

* **Project** - endpoints are assigned to a Project to provide scope of access
* **Type** - Gerrit
* **Name** - a name to identify the Gerrit Endpoint
* **Description** - description of the Gerrit Endpoint
* **Mark restricted** - if enabled, only Code Stream or Project Administrators can execute Pipelines using this endpoint
* **Cloud proxy** - (vRA Cloud only) the Cloud Proxy appliance through which the endpoint should communicate
* **URL** - URL of the Gerrit server
* **Username** - Username to authenticate to the Gerrit server
* **Password** - Password to authenticate to the Gerrit server
* **Private key** - Private key (RSA) to authenticate to the Gerrit server
* **Pass phrase** - Pass phrase to decrypt the Private key

{{< img src="gerrit-endpoint.png" alt="Adding a Gerrit Endpoint configuration" >}}

{{< hint warning >}}
* When adding an endpoint URL you'll be prompted to view and accept the certificate.
* You can validate the configuration using the VALIDATE button.
* You should create [Secret Variables](/Configure/Variables/) to store your user credentials.
{{< /hint >}}
