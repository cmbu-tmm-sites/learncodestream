---
title: "Condition"
---

Conditions are a way, to make sure that a task, only runs, if a certain condition is met.

{{< img src="images/condition.png" alt="Precondition" >}}

An example could be, that you have an input value, in your pipeline, with the name of "run"

In your task, you put in the Precondition of 
```
${input.run} == "true"
```
which means that this task, will only run, if the value if run = true
