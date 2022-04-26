---
title: "Kubernetes"
---

The Kubernetes Task allows for interation and execution of Get, Create, Apply, Delete and Rollback actions against a [Kubernetes Endpoint](/configure/endpoints/kubernetes). you can use a [git endpoint](/configure/endpoints/git) for the yaml manifest definitions. the combination of [git endpoints](/configure/endpoints/git), use of a [git triggers](/triggers/git) and the Kubernetes task allows you to build complex Kubernetes application deployment strategies.

Common across all the Kubernetes actions is are:
* **Kubernetes Cluster** - the Kubernetes endpoint that the task will execute against
* **Timeout** - the task timeout while waiting for a response from Kubernetes, this can be useful if, for example, your deployment task needs to download several large container images that may exceed the default timeout, or your deployment has readiness checks that take time to return OK.
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

## Actions
There are five different actions you can perform against the Kubernetes endpoint.

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
The Create action allows us to create objects based on a YAML specification, and as is common accross all tasks you can use locally defined or Git sourced YAML definitions. There is also an option to **Continue on conflict** - if enabled, and the object you are trying to create already exists, then the Task will not fail the Pipeline but continue on to the next Task or Stage. This can be useful if you want to ensure an object exists but you are not sure if it already does - a common example would be creating a `namespace`.

You *can* also use YAML files with multiple documents, separated with `---` to conform with YAML specifications - for example, the definition below creates two `namespace`:

{{< hint warning>}}Creating all the kubernetes resources with a single manifest file may be appropriate in some cases, however any failure of a single object creation will result in the whole task failing. If you need to respond to specific failures, or for ease of troubleshooting, it's normally a better idea to split the objects into multiple tasks and manifests.
{{< /hint>}}

{{< img src="create-multiple-ns.png" alt="Create multiple Kubernetes Namespaces" >}}

When this Create task is executed, the response JSON will include responses for each object creation (or associated failure)

{{< img src="create-multiple-ns-response.png" alt="Response for multiple Kubernetes Namespaces" >}}

{{< /tab >}}

{{< tab Apply >}}
The Apply action allows us to modify existing objects by applying an updated manifest YAML - this can be useful in a GitOps scenario when we are using Git as the single source of truth for an application. In this case when a YAML file is updated, a [Git Trigger](/triggers/git) will start the pipeline and apply the updated YAML manifest to the existing object.

If we take the `namespace` from in the Create task, `ns-01`, and want to update the `metadata` with a `label` we can apply an updated manifest:

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: ns-01
  labels:
    app: learn-code-stream
```

When this task executes, the response shows that the existing object has been updated with the new label:

{{< img src="update-ns-label-result.png" alt="Updated namespace includes the label">}}
{{< /tab >}}

{{< tab Delete >}}
The Delete action allows us to delete objects from Kubernetes based on a YAML specification - as with the Get action we need to specify enough information to identify the object we wish to delete. Most often, this is the object type, the name of the object and the namespace that the object resides - however to delete the namespace we created in the previous task we would use `kubectl delete namespace ns-01`, which translates to the following YAML:

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: ns-01
```

When executed, the task succeeds if the object has been removed and fails if the deletion fails. The JSON output will reflect the new status:

{{< img src="delete-success.png" alt="Successfully deleted">}}

{{< /tab >}}
{{< tab Rollback >}}
The Rollback action relates to the management of `deployment`, `statefulset` and `daemonset` objects in kubernetes. Whenever the Pod template (`.spec.template`) properties for these objects are modified a rollout is triggered and a record of the previous state is recorded so that you can roll back to a previous state if required. The Rollback action allows you trigger a rollback to one of the previous five states and would typically be used to recover from a failed update to an existing `deployment`, `statefulset` or `daemonset`.

{{< img src="rollback-deployment.png" alt="Rollback the controller deployment to the previous version">}}
{{< /tab >}}
{{< /tabs >}}


## Links and References
* [Rolling Back a Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-back-a-deployment)
