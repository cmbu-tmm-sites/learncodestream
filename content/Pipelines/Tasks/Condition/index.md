---
title: "Condition"
---

The Condition Task is very similar to the [Precondition setting](/Pipelines/Tasks/#precondition-and-continue-on-failure) available for all Tasks, without having an additional task attached to it. It can be used to evaluate the success of previous Stages before moving on with the Pipeline, or to trigger the failure of a pipeline based on a set of conditions. Simple operators can be used to compare Pipeline task output, Variables, Inputs, or any other property that is accessible in the Pipeline.

{{< img src="condition-config.png" alt="Condition Task configuration" >}}