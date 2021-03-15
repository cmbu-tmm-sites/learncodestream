---
title: "Custom Integrations"
weight: 600
---

Custom Integrations allow you write custom code in Python, Shell or NodeJS, and execute your code as a Custom [Task]() in a [Stage]() of a [Pipeline](). When the Custom Integration task is executed, it uses the [Docker Host]() endpoint and Container Image configured for the parent [Pipeline]().

## Creating a Custom Integration
The Custom Integration is essentially a YAML file with four sections:

- **Runtime** - defines the runtime for the Custom Integration (`nodejs`, `python2`, `python3`, `shell`)
- **Code** - this is a multi-line scalar (any indented text after the `|` symbol should be interpreted as a multi-line scalar value) of the code to execute
- **Input Properties** - an array of input properties that are used in the execution of the Code
- **Output Properties** - an array of output properties that are returned by the execution of the Code

### Input Properties
The available input types are documented in article linked the [reference](/Custom-Integrations/#refs) section below, one of the easiest ways to understand the different types is to create a new Custom Integration, select the runtime of your choice, then view the generated placeholder content. 

{{< tabs "Binding Inputs" >}}
{{< tab Shell >}}
```shell
echo $inputPropertyName
```
{{< /tab >}}
{{< tab Python >}}
```python
from context import getInput # Import the getInput function from context.py
myInput = getInput("inputPropertyName")
```
{{< /tab >}}
{{< tab NodeJS >}}
```javascript
var context = require("./context.js") // Import the getInput function from context.js
var myInput = context.getInput("inputPropertyName");
```
{{< /tab >}}
{{< /tabs >}}

### Output Properties
Output properties are used to return values from the Custom Integration task - currently only one type (`label`) is supported. To return a value it should be out to the Output Property

{{< tabs "Binding Outputs" >}}
{{< tab Shell >}}
```shell
export outputPropertyName = "outputPropertyValue"
```
{{< /tab >}}
{{< tab Python >}}
```python
from context import setOutput # Import the setOutput function from context.py
setOutput("outputPropertyName", "outputPropertyValue")
```
{{< /tab >}}
{{< tab NodeJS >}}
```javascript
var context = require("./context.js") // Import the setOutput function from context.js
context.setOutput("outputPropertyName", "outputPropertyValue");
```
{{< /tab >}}
{{< /tabs >}}

### Versioning and Releasing
When you create a new Custom Integration it will be created as a Draft. In order to use the Custom Integration in a Pipeline Task you must release a version - this means that the released version can't be changed and cause the Pipeline to fail. When you create a Custom Task type in a Pipeline Stage you can select which version you wish to use.

{{< img src="custom-integration-create-version.png" alt="Version and release a Custom Integration" >}}

## Example Custom Integration - Create a Basic Authentication Header

The below example code takes a `username` and `password` input and returns a `basicAuthHeader` output for each of the runtimes - it's a very simple use case that helps me when working with a REST API that only accepts a basic authentication headers.

{{< hint warning >}}The Container image you specify in the [Pipeline Workspace configuration](/Pipelines/#pipeline-configuration) must support the runtime you're using for the Custom Integration code{{< /hint >}}

{{< tabs "Create a Basic Authentication Header" >}}
{{< tab Shell >}}
```yaml
---
runtime: shell
code: |
  export basicAuthHeader=$(echo -n $username:$password | base64)

inputProperties:
  # Username input
  - name: 'username'
    type: text
    title: 'Username'
    placeHolder: 'Enter basic authentication usename'
    required: true
    bindable: true
  # Password input
  - name: 'password'
    type: password
    title: 'Password'
    placeHolder: 'Enter basic authentication password'
    defaultValue: ''
    required: true
    bindable: true


outputProperties:
  - name: basicAuthHeader
    type: label
    title: Basic Authentication Header
    ```
{{< /tab >}}
{{< tab Python >}}
```yaml
---
runtime: "python3"
code: |
  from base64 import b64encode
  from context import getInput, setOutput
  
  username = getInput('username')
  password = getInput('password')
  
  usernameAndPassword = b64encode(bytes(f'{username}:{password}',encoding='ascii')).decode('ascii')

  setOutput('basicAuthHeader', "Basic "+usernameAndPassword)

inputProperties:
  # Username input
  - name: 'username'
    type: text
    title: 'Username'
    placeHolder: 'Enter basic authentication usename'
    required: true
    bindable: true
  # Password input
  - name: 'password'
    type: password
    title: 'Password'
    placeHolder: 'Enter basic authentication password'
    defaultValue: ''
    required: true
    bindable: true


outputProperties:
  - name: basicAuthHeader
    type: label
    title: Basic Authentication Header
```
{{< /tab >}}
{{< tab NodeJS >}}
```yaml
---
runtime: "nodejs"
code: |
  var context = require("./context.js")

  var username = context.getInput("username");;
  var password = context.getInput("password");;
  
  const buff = Buffer.from(username+':'+password, 'utf-8');
  const base64 = buff.toString('base64');
  
  context.setOutput("basicAuthHeader", base64);

inputProperties:
  # Username input
  - name: 'username'
    type: text
    title: 'Username'
    placeHolder: 'Enter basic authentication usename'
    required: true
    bindable: true
  # Password input
  - name: 'password'
    type: password
    title: 'Password'
    placeHolder: 'Enter basic authentication password'
    defaultValue: ''
    required: true
    bindable: true


outputProperties:
  - name: basicAuthHeader
    type: label
    title: Basic Authentication Header
```
{{< /tab >}}
{{< /tabs >}}

To use my new task in a Pipeline stage, I create a new Task, select Type `Custom` and select my Custom Integration and released version. This automatically creates an input form for the `username` and `password` input properties. Because I have set `bindable: true` for these properties, I can bind them to [Pipeline variables](/Pipelines/#variables-in-pipelines), or [Variables](/Configure/variables)

{{< img src="custom-integration-in-pipeline.png" alt="Using a Custom Integration in a Custom task" >}}

To access the output property `basicAuthHeader` later on in my REST task, I can access the task properties by using the Stage name, Task name, then `output.properties.propertyName` - e.g:

`${Authenticate.Create Auth Header.output.properties.basicAuthHeader}`

### Reference
 * [How do I integrate my own build, test, and deploy tools with vRealize Automation Code Stream](https://docs.vmware.com/en/vRealize-Automation/8.3/Using-and-Managing-CodeStream/GUID-AB3CF709-D725-4CF2-90E5-144E0162DA59.html?hWord=N4IghgNiBcIMYFcDOAXA9gWwAQEsB2KApgOYBOYKOaeIAvkA)