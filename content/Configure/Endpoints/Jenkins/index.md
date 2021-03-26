---
title: "Jenkins"
---

The Jenkins endpoint provides integration to a Jenkins server and allows the use of a [Jenkins Task](/Pipelines/Tasks/Jenkins/) to execute a Job on the Jenkins server configured in the endpoint.

* **Project** - endpoints are assigned to a Project to provide scope of access
* **Type** - Jenkins
* **Name** - a name to identify the Jenkins Endpoint
* **Description** - description of the Jenkins Endpoint
* **Mark restricted** - as described in the [Projects](/Configure/Projects) page, if the Endpoint is marked as restricted only an Administrator can execute a Pipeline that uses it
* **URL** - URL of the Jenkins server
* **Username** - Username to authenticate to the Jenkins server
* **Password** - Password to authenticate to the Jenkins server
* **Folder Path** - Location of the Job folder
* **Polling interval (sec)** - Interval to poll the Jenkins server for Job responses
* **Request retries** - Number of times to request Job retries
* **Retry wait time (sec)** - Interval to wait before requesting a Job retry

{{< img src="jenkins-endpoint.png" alt="Adding a Jenkins Endpoint configuration" >}}

When adding a Jenkins endpoint you'll be prompted to view and trust the certificate. You can validate the configuration using the VALIDATE button. As with all sensitive information, you should create [Secret Variables](/Configure/Variables/) to store your user credentials.

## Links and References
* [https://www.jenkins.io/](https://www.jenkins.io/)