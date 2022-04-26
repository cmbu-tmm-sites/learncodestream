---
title: "vRealize Orchestrator"
---

The vRealize Orchestrator endpoint provides integration to a vRealize Orchestrator server and allows the use of a [vRealize Orchestrator Task](/pipelines/tasks/vrealize-orchestrator).

* **Project** - endpoints are assigned to a Project to provide scope of access
* **Type** - vRealize Orchestrator
* **Name** - a name to identify the vRealize Orchestrator Endpoint
* **Description** - description of the vRealize Orchestrator Endpoint
* **Mark restricted** - if enabled, only Code Stream or Project Administrators can execute Pipelines using this endpoint
* **Cloud proxy** - (vRA Cloud only) the Cloud Proxy appliance through which the endpoint should communicate
* **URL** - URL of the vRealize Orchestrator server
* **Username** - Username to authenticate to the vRealize Orchestrator server
* **Password** - Password to authenticate to the vRealize Orchestrator server

{{< hint info >}}To access the local vRealize Orchestrator instance on the vRealize Automation appliance, just enter the appliance URL{{< /hint >}}


{{< img src="vro-endpoint.png" alt="Adding a vRealize Orchestrator Endpoint configuration" >}}

{{< hint warning >}}
* When adding an endpoint URL you'll be prompted to view and accept the certificate.
* You can validate the configuration using the VALIDATE button.
* You should create [Secret Variables](/configure/variables) to store your user credentials.
{{< /hint >}}

## Links and References
![](2021-03-26-14-24-00.png)