---
title: "Kubernetes"
---

The Kubernetes Task allows for interation and execution of Get, Create, Apply, Delete and Rollback actions against a [Kubernetes Endpoint](/Configure/Endpoints/Kubernetes). You can use a [Git Endpoint](/Configure/Endpoints/Git) for the YAML manifest definitions. The combination of [Git Endpoints](/Configure/Endpoints/Git), use of a [Git Triggers](/Triggers/Git) and the Kubernetes task allows you to build complex Kubernetes application deployment strategies.

Common across all the Kubernetes actions is are:
* **Kubernetes Cluster** - the Kubernetes endpoint that the task will execute against
* **Timeout** - the task timeout while waiting for a response from Kubernetes
* **Source Type**
  * *Local definition* uses the YAML entered in the Local YAML Definition field - this allows you to use variables, properties and inputs directly in the YAML definition to customise the YAML
  * *Source Control* uses the YAML loaded from a Git repository specified as a Git Endpoint, which can be customised by using variables in the YAML source file and parameters in the task configuration. e.g. by creating a YAML template with the `$${NAMESPACE}` variable below, the namespace name can be customised with a parameter:
    ```yaml
        apiVersion: v1
        kind: Namespace
        metadata:
            name: $${NAMESPACE}
    ```
    {{< img src="create-with-parameters.png" alt="YAML from Source Control, with Parameters" >}}

{{< tabs "Kubernetes Task Actions" >}}
{{< tab Get >}}
The Get action allows us to retrieve objects from Kubernetes based on a YAML specification - the minimum we need to specify is the object type, the name of the object and the namespace that the object resides, for example the query `kubectl get deployment controller --namespace metallb-system` translates to the following YAML:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: controller
  namespace: metallb-system
```

{{< img src="kubernetes-get-task.png" alt="Kubernetes Get Task" >}}

When the Kubernetes task runs the returned JSON object is accessible as part of the Task response object. This means that you can access properties of the requested object in subsequent tasks - e.g. to examine the number of deployments in the replica spec, I could access `${Stage0.Kubernetes.output.response.deployments.controller.spec.replicas}`

{{< img src="get-task-response.png" alt="Kubernetes Get Task Response" >}}

{{< /tab >}}
{{< tab Create >}}

{{< /tab >}}
{{< tab Apply >}}

{{< /tab >}}
{{< tab Delete >}}

{{< /tab >}}
{{< tab Rollback >}}

{{< /tab >}}
{{< /tabs >}}