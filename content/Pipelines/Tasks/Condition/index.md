---
title: "Condition"
---

The Condition Task is very similar to the [Precondition setting](/Pipelines/Tasks/#precondition-and-continue-on-failure) available for all Tasks, without having an additional task attached to it. It can be used to evaluate the success of previous Stages before moving on with the Pipeline, or to trigger the failure of a pipeline based on a set of conditions. Simple operators can be used to compare Pipeline task output, Variables, Inputs, or any other property that is accessible in the Pipeline.

{{< img src="images/condition.png" alt="Precondition" >}}

An example could be, that you have an input value, in your pipeline, with the name of "run". In your task, you put in the Precondition of `${input.run} == "true"` which means that this task will only run if the value if `run` is `true`