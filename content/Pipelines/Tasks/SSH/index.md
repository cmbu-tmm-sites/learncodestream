---
title: "SSH"
---
The SSH task is similar in many ways to the [CI]() and [PowerShell]() tasks - it allows you to execute code on a remote machine, in this case over SSH. The task can authenticate with username and password, or a private key.

* **Host** - the IP or FQDN of the SSH host
* **Username** - the username to authenticate to the SSH host 
* **Passsword** - the password to authenticate to the SSH host -or-
* **Private Key and Passphrase** - the private key and passphrase for the private key to authenticate to the SSH host
* **Environment variables** - can be used to make pipeline variables available to the SSH host script execution, if needed
* **Script** - the shell script to execute on the SSH host
* **Arguments** - arguments for the shell execution
* **Working Directory** - the directory in which to execute the script (defaults to the users home directory, if not specified)

{{< img src="ssh-task-config.png" alt="An example SSH task configuration" >}}

{{< hint warning >}}
Secret [Variables](/Configure/Variables) should be used for authentication parameters to ensure they're kept secret and hidden from logs
{{< /hint >}}

## Script Response File
The script response file is the method for making information from an SSH task available to subsequent Pipeline Tasks. Values written to `$SCRIPT_RESPONSE_FILE` in the script will be available in the `${Stage.SSHTask.output.response}` variable, or the response file itself can be found using the `responseFilePath` parameter.

{{< hint info >}}
To make multiple response properties available you can create a JSON string with property names and values and write this to the `$SCRIPT_RESPONSE_FILE`. Subsequent tasks can access the properties as sub-properties of the `${Stage.SSHTask.output.response}` output.

For example, writing the below JSON string to the script response file means that the values of `test1` and `test2` can be accessed later using `${Stage.SSHTask.output.response.test1}` and `${Stage.SSHTask.output.response.test2}`
{{< img src="response-json.png" alt="Writing JSON to the script response file" >}}
{{< /hint >}}
## Output Parameters
* `status`
* `userFolder`
* `response`
* `responseFilePath`
* `errorMessage`
* `logFilePath`
* `exitCode`
* `scriptExecutionId`
* `completed`
* `error`
* `logs`
* `errorFilePath`