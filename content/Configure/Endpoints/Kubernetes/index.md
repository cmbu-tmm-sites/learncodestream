---
title: "Kubernetes"
---

The Kubernetes endpoint provides configuration for a Kubernetes cluster to use with the [Kubernetes Task](/Pipelines/Tasks/Kubernetes/).

* **Project** - endpoints are assigned to a Project to provide scope of access
* **Type** - Kubernetes
* **Name** - a name to identify the Kubernetes Endpoint
* **Description** - description of the Kubernetes Endpoint
* **Mark restricted** - if enabled, only Code Stream or Project Administrators can execute Pipelines using this endpoint
* **Cloud proxy** - (vRA Cloud only) the Cloud Proxy appliance through which the endpoint should communicate
* **Kubernetes cluster URL** -  the URL of the Kubernetes instance
* **Authentication type**
    * **Token** - Kubernetes user token
    * **Basic Auth**
        * **Username** - the username to authenticate to the Kubernetes instance
        * **Password** - the password to authenticate to the Kubernetes instance
    * **Certificate**
        * **Certificate authority data** - `certificate-authority-data` from a kubeconf file
        * **Certificate data** - `client-cerificate-data` from a kubeconf file
        * **Client key data** - `client-key-data` from a kubeconf file


{{< img src="kubernetes-endpoint.png" alt="Adding an Kubernetes Endpoint configuration" >}}

{{< hint warning >}}
* When adding an endpoint you'll be prompted to view and accept the certificate.
* You can validate the configuration using the VALIDATE button.
* You should create [Secret Variables](/Configure/Variables/) to store your user credentials.
{{< /hint >}}