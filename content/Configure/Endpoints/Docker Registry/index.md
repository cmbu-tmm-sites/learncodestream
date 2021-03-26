---
title: "Docker Registry"
---

The Docker Registry endpoint provides credentials for accessing a specific Registry in the context of a [Pipeline Workspace](/Pipelines/#pipeline-configuration). If a container image requires authentication to download, credentials can be added and the Endpoint assigned to the [Pipeline Workspace](/Pipelines/#pipeline-configuration) configuration. When the Pipeline is executed the Endpoint credentials will be used in the `docker pull`.


* **Project** - endpoints are assigned to a Project to provide scope of access
* **Type** - Docker Registry
* **Name** - a name to identify the Docker Registry Endpoint
* **Description** - description of the Docker Registry Endpoint
* **Mark restricted** - if enabled, only Code Stream or Project Administrators can execute Pipelines using this endpoint
* **Cloud proxy** - (vRA Cloud only) the Cloud Proxy appliance through which the endpoint should communicate
* **Server type** - DockerHub or Docker Trusted Registry
* **Repo URL** - the URL of the container image repository
* **Authentication**
    * Docker Hub uses Username and Password authentication
    * Docker Trusted Registry can use a Username and Password or Access token

{{< img src="docker-registry-endpoint.png" alt="Adding a Docker Registry Endpoint configuration" >}}

{{< hint warning >}}
* When adding an endpoint you'll be prompted to view and accept the certificate.
* You can validate the configuration using the VALIDATE button.
* You should create [Secret Variables](/Configure/Variables/) to store your user credentials.
{{< /hint >}}

{{< hint info >}}The Docker Registry endpoint can be used to avoid the Docker Hub rate limit by authenticating before downloading the container image. Authenticated user accounts have a higher rate limit on Docker Hub{{< /hint >}}