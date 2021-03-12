---
title: "Variables"
weight: 630
---

Variables are a great way to keep text, secrets etc. that you have to reuse, in your Pipelines, in one central place, to easily manage. 
It's also a good practice, if you need to export your pipelines, to make sure, that sensetive information is not exported as well.

## Create
![Create_Variable](images/create_variable.png)
### Type
- Regular - Value is not hidden
- Secret - Value is hidden
- Restricted - Pipelines containing Restricted variables, can only be run by administrators

### Project
Variables need to be attached to a project.

### Names
The name you use, when you reference the variable

### Value
The actual value of the variable

### Description
The description of the value, to easely identify the variable and the use of it.

## Use

When using the variable, all you need to do, is to write ${var.NameOfVariable} where you want to use it.

So a variable with the name of mysecret will look like 
```
${var.mysecret}
```
 in your pipeline
