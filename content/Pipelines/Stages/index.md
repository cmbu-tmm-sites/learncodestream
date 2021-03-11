---
title: "Stages"
weight: 10
---

Pipeline Stages are logical groupings of Tasks to reflect the structure of the process, for example your process has a **Build**, **Test** and **Release** phase, the Pipeline Stages can be configured to reflect this.

{{< img src="2021-03-11-14-36-51.png" alt="Pipeline Stages" >}}

Properties can be accessed from each stage and task using `${Stage.Task.Property}` - for example, in the "Build" Stage the "Trigger Image Enumeration" task is a REST API call with a JSON response. The response property "id" is referenced using `${Build.Trigger Image Enumeration.output.responseBody.id}`