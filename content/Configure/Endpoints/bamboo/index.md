---
title: "Bamboo"
---
The Bamboo endpoint provides configuration for use in the [Bamboo Task](/pipelines/tasks/bamboo).

* **Project** - endpoints are assigned to a Project to provide scope of access
* **Type** - Bamboo
* **Name** - a name to identify the Bamboo Endpoint
* **Description** - description of the Bamboo Endpoint
* **Mark restricted** - if enabled, only Code Stream or Project Administrators can execute Pipelines using this endpoint
* **Cloud proxy** - (vRA Cloud only) the Cloud Proxy appliance through which the endpoint should communicate
* **URL** - URL of the Bamboo server
* **Username** - Username to authenticate to the Bamboo server
* **Password** - Password to authenticate to the Bamboo server

{{< img src="bamboo-endpoint.png" alt="Adding a Bamboo Endpoint configuration" >}}

{{< hint warning >}}
* When adding an endpoint URL you'll be prompted to view and accept the certificate.
* You can validate the configuration using the VALIDATE button.
* You should create [Secret Variables](/configure/variables) to store your user credentials.
{{< /hint >}}
