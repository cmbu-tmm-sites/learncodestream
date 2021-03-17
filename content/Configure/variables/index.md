---
title: "Variables"
weight: 630
---

Variables are a great way to keep reusable text values or secrets for use in Pipelines in one central place. Variables are scoped to a [Project](/Configure/Projects) and can be used to provide secure access to credentials or configuration information. Using Variables ensures that if you need to export your pipelines that sensitive information is not exported, and allows you to control access to that sensitive information.

{{< img src="variables.png" alt="Variables" >}}

* **Type** (see )
    - REGULAR - Value is plain text and accessible to any Project role
    - SECRET - Value is hidden but can be used in Pipelines by Project members and administrators
    - RESTRICTED - Value is hidden and can only be accessed in Pipelines by administrators
* **Project** - Variables need to be attached to a project.
* **Names** - The name you use, when you reference the variable
* **Value** - The actual value of the variable
* **Description** - The description of the value, to easely identify the variable and the use of it.

{{< img src="variable-create.png" alt="Create a new SECRET variable" >}}

{{< hint info >}}
Variables are accessed in Pipelines by typing the `$` symbol which opens the [Pipeline Variables](/Pipelines/#variables-in-pipelines) menu. A Variable with the name of `mysecret` will be access using `${var.mysecret}` in your pipeline
{{< /hint >}}