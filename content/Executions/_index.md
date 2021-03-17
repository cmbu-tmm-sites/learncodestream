---
title: "Executions"
weight: 300
---

The Executions page provides a detailed account of every Pipeline Execution that can be filtered by Pipeline, Status, Tag, or any other pipeline property. It provides an at-a-glance view of which pipelines have failed, where they've failed, and the error messages returned.

{{< img src="execution-view.png" alt="Pipeline Execution Overview" >}}

Clicking into an Execution will give you a detailed view of the Pipeline [Stages](/Pipelines/Stages), [Tasks](/Pipelines/Tasks), [Configuration](/Pipelines/#pipeline-configuration), Inputs, Task Inputs, Task Outputs, Task execution logs, and the output JSON object from the execution.
{{< hint info >}}
The Output JSON view is very useful for identifying variables from one task to pass to another - see [Variables in Pipelines](/Pipelines/#variables-in-pipelines)
{{< /hint >}}
{{< img src="execution-details.png" alt="Pipeline Execution Detail" >}}

## Nested Executions
Nested executions are Pipeline Executions that have been run as part of the Pipeline Task within a parent Pipeline. By default they're hidden from view in the Executions pane, however if you add the **Show: Nested Executions** filter to the view, you can identify them by the **Comments** section, and they will be tagged with the parent Execution ID.

{{< img src="nested-executions.png" alt="Nested Executions with their Parent Execution" >}}