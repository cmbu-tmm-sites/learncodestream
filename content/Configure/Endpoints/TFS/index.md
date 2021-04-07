---
title: "TFS"
---

The TFS endpoint provides integration to a TFS server and allows the use of a [TFS Task](/Pipelines/Tasks/TFS/).

* **Project** - endpoints are assigned to a Project to provide scope of access
* **Type** - TFS
* **Name** - a name to identify the TFS Endpoint
* **Description** - description of the TFS Endpoint
* **Mark restricted** - if enabled, only Code Stream or Project Administrators can execute Pipelines using this endpoint
* **Cloud proxy** - (vRA Cloud only) the Cloud Proxy appliance through which the endpoint should communicate
* **URL** - URL of the TFS server
* **Username** - Username to authenticate to the TFS server
* **Password** - Password to authenticate to the TFS server
* **Domain name** - Domain name to authenticate to the TFS server
* **Polling interval (sec)** - Interval to poll the TFS server
* **TFS Server Version** - 2015 or 2017

{{< img src="tfs-endpoint.png" alt="Adding a TFS Endpoint configuration" >}}

{{< hint warning >}}
* When adding an endpoint URL you'll be prompted to view and accept the certificate.
* You can validate the configuration using the VALIDATE button.
* You should create [Secret Variables](/Configure/Variables/) to store your user credentials.
{{< /hint >}}

## Links and References
