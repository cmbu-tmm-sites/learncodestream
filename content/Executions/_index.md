---
title: "Executions"
weight: 300
---

In Executions, you’ll find a detailed account of every pipeline execution that can be filtered by Pipeline, Status, Tag - or any other property. You can view at a glance which pipelines have failed, where and the error messages returned.

{{< img src="2021-03-11-13-51-22.png" alt="Pipeline Execution Overview" >}}

Clicking into an Execution will give you a detailed view of the Pipeline [Stages](Pipelines/Stages), [Tasks](Pipelines/Tasks), [Configuration](/Pipelines/#pipeline-configuration), Inputs, Task Inputs, Task Outputs, Task execution logs, and the output JSON object from the execution.
{{< hint info >}}
The Output JSON view is very useful for identifying variables from one task to pass to another - see [Variables in Pipelines](/Pipelines/#variables-in-pipelines)
{{< /hint >}}
{{< img src="2021-03-11-14-09-13.png" alt="Pipeline Execution Detail" >}}

It's also worth noting that from the [Pipelines](/Pipelines) view you can access the previous 5 executions directly, by clicking on the icons

{{< img src="2021-03-11-13-47-56.png" alt="Pipeline Executions" >}}

## Nested Executions
Nested executions are Pipeline Executions that have been run as part of the Pipeline Task within a parent Pipeline. By default they're hidden from view in the Executions pane, however if you add the **Show: Nested Executions** filter to the view, you can identify them by the **Comments** section, and they will be tagged with the parent Execution ID.

{{< img src="nested-executions.png" alt="Nested Executions with their Parent Execution" >}}