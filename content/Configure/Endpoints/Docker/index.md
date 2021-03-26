---
title: "Docker"
---

The Docker Endpoint provides an execution environment for [CI Tasks](/Pipelines/Tasks/CI) and [Custom Integrations](/Custom-Integrations) which are executed inside a container image on the configured Docker host. 

* **Project** - endpoints are assigned to a Project to provide scope of access
* **Type** - Docker
* **Name** - a name to identify the Docker Endpoint
* **Description** - description of the Docker Endpoint
* **Mark restricted** - as described in the [Projects](/Configure/Projects) page, if the Endpoint is marked as restricted only an Administrator can execute a Pipeline that uses it
* **URL** - the address including protocol (HTTP/HTTPS) and port for the Docker API
* **Shared Path** - a folder on the Docker host where the logs and artefacts generated in executions will be stored

{{< img src="docker-endpoint.png" alt="Adding a Docker Endpoint configuration" >}}

When adding a Docker host over TLS, you'll be prompted to view and trust the certificate. You can validate the configuration using the VALIDATE button. As with all sensitive information, you should create [Secret Variables](/Configure/Variables/) to store your user credentials.

## Links and References
* [Creating a Docker host for vRealize Automation Code Stream](https://blogs.vmware.com/management/2020/08/creating-a-docker-host-for-vra-code-stream.html)