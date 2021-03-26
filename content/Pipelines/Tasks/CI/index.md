---
title: "CI"
---

The CI task enables almost any action in your pipeline by pulling a specific Docker image from a registry endpoint, and deploying it to a Docker host configured as an Endpoint. It then executes the CI task script in the context of the running container. It is an incredibly powerful and flexible task type, because the image can have almost any tool or program in it.

The CI task runs using parameters configured in the [Pipeline Workspace configuration](/Pipelines/#pipeline-configuration), including the Container Image, Docker Registry, Docker Host, directory, cache, environment variables and CPU/Memory limits.

The CI task container will run for the lifespan of the entire pipeline, so subsequent CI tasks within a pipeline will be executed in the same environment - this means that you can, for example, write files in container that will be preserved between Tasks.

If a Pipeline has been executed from a [Git Trigger](), and has been [configured to clone the repository with the correct Inputs](/Pipelines/#pipeline-configuration), the Git repository will be automatically cloned into the Working Directory.

## Creating a CI task
As well as the [common configurations](/Pipelines/Tasks/#common-configuration) available to all tasks, the CI task has:
* **Steps** - the script to execute in the container
* **Preserve artifacts** - the paths of artifacts to preserve in the shared path (on the Docker host) - e.g. a compiled binary, configuration file or SSH key
* **Export** - exported variable names to be made available to the Pipeline after the task executes
* **Process configurations** - configuration elements for JUnit, JaCoCo, Checkstyle, FindBugs processing

### Steps
The steps stage is essentially a Shell script that will be executed on the CI container image. This means it's relatively easy to convert any exisitng Shell scripts into a repeatable CI task by using [Pipeline Inputs](), [Variables](), and [Pipeline Variable Binding](/Pipelines/#variables-in-pipelines).

{{< img src="bash-steps.png" alt="An example CI Task steps">}}

### Preserve Artifacts
Artifacts (files) specified here will be stored in a Shared Folder on the Docker host configured in the Pipeline workspace. The full path of the preserved file will be available in the Task output JSON for later use. If, for example, my CI task writes to a file "preserve.txt" and specifies the file name/path in the Perserve Artifacts setting, the full path to "preserve.txt" will be available in `${Stage0.Task0.output.artifacts[0]}`

{{< img src="preserve-artifacts.png" alt="Preserved Artifact Path in Output JSON" >}}
### Exports
You can use the Exports feature when you want the result of a CI task to be available to the Pipeline. These are *simple* string exports that must be compatible with the JSON output format that the task returns. Exporting multiline strings, for example, does not export correctly.

An example use might be a `BUILDTIME` variable that will be used in naming throughout the pipeline - in the CI task steps the variable must be declared with the `export` keyword:
```shell
export BUILDTIME="$(date "+%Y%m%d-%H%M%S")"
```
Then the `BUILDTIME` variable can be added to the Export list and accessed later using [Pipeline Variable Binding](/Pipelines/#variables-in-pipelines)

{{< img src="export-variable.png" alt="Export BUILDTIME variable from a CI task" >}}


## Links and References
* [What variables and expressions can I use when binding pipeline tasks in VMware Code Stream](https://docs.vmware.com/en/VMware-Code-Stream/services/Using-and-Managing-CodeStream/GUID-5094086E-AF44-456D-AB35-6853FB780F42.html)