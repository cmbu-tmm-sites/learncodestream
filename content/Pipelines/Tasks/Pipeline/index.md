---
title: "Pipeline"
---

The Pipeline task allows you to nest existing Pipelines within a parent pipeline, which is really useful for chaining together smaller units of work within a larger parent process. The Pipeline task will automatically generate fields for the Inputs of the nested Pipeline, and the Output parameters will be available to the parent Pipeline as the output properties of the Pipeline task.

The Task configured below will execute a Pipeline called "vra-POST", the three Input parameters (`vraaccesstoken`, `vrarequestpayload`, `vrarequesturi`) for the Pipeline have been automatically added to the task and the one output paramter `vraResponseJSON` has been added to the output parameters.

{{< img src="nested-pipeline.png" alt="Nested Pipeline Configuration" >}}

When viewing a parent Pipeline Execution, nested Pipeline tasks will have an icon to indicate they are nested. When you examine the Task in the Execution, there is a link to the nested Pipeline execution in the **Result** section. You can also details of the nested Pipeline in the **Pipeline Output** section.

{{< img src="nested-pipeline-execution.png" alt="Nested Pipeline Execution" >}}
