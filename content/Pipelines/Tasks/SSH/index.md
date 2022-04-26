---
title: "SSH"
---
The SSH task is similar in many ways to the [CI](/pipelines/tasks/ci) and [powershell](/pipelines/tasks/powershell) tasks - it allows you to execute code on a remote machine, in this case over SSH. The task can authenticate with username and password, or a private key.

* **Host** - the IP or FQDN of the SSH host
* **Username** - the username to authenticate to the SSH host 
* **Passsword** - the password to authenticate to the SSH host -or-
* **Private Key and Passphrase** - the private key and passphrase for the private key to authenticate to the SSH host
* **Environment variables** - can be used to make pipeline variables available to the SSH host script execution, if needed
* **Script** - the shell script to execute on the SSH host
* **Arguments** - arguments for the shell execution
* **Working Directory** - the directory in which to execute the script (defaults to the users home directory, if not specified)

{{< img src="ssh-task-config.png" alt="An example SSH task configuration" >}}

To use an SSH key to connect to the SSH host, the key must be a PEM encoded RSA key (it should start with `---begin rsa private key----`). it's recommended to generate a key specifically for codestream and store the key in a [variable](/configure/variables). You can enter a passphrase for additional security.

The following example generates a key pair called `id_codestream`. It is executed on the SSH host under the user profile that will be used to connect (`autotmm`)

```shell
# Generate the rsa key-pair
autotmm@smcg-sc2-docker-host:~$ ssh-keygen -t rsa
Generating public/private rsa key pair.
Enter file in which to save the key (/home/autotmm/.ssh/id_rsa): /home/autotmm/.ssh/id_codestream
Enter passphrase (empty for no passphrase): ***********
Enter same passphrase again: ***********
Your identification has been saved in /home/autotmm/.ssh/id_codestream.
Your public key has been saved in /home/autotmm/.ssh/id_codestream.pub.
The key fingerprint is:
SHA256:WJv9OkQ+byQmI5XePG+/FjlHxVt3B6JS0ptzXKJ0/uw autotmm@smcg-sc2-docker-host
The key's randomart image is:
+---[RSA 2048]----+
|        ... . .o |
|         oo.o.. B|
|        oo.B o  B|
|       oo=* +  ..|
|      .oS=.o o o |
|      . + X.. * .|
|       . = B.. + |
|          ..= E  |
|          .+ oo. |
+----[SHA256]-----+

# Add the new SSH key to the SSH agent
autotmm@smcg-sc2-docker-host:~$ ssh-add ~/.ssh/id_codestream
Identity added: /home/autotmm/.ssh/id_codestream (/home/autotmm/.ssh/id_codestream)

# Add the SSH public key to the authorized_keys file
autotmm@smcg-sc2-docker-host:~$ cat ~/.ssh/id_codestream.pub >> ~/.ssh/authorized_keys
```
The contents of `id_codestream` can then be used in the SSH task (along with the passphrase, if used) to connect to the SSH server.

{{< img src="ssh-task-key.png" alt="Using an SSH key to connect" >}}

{{< hint warning >}}
Secret [Variables](/configure/variables) should be used for authentication parameters to ensure they're kept secret and hidden from logs
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