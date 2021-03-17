---
title: "PowerShell"
---

The PowerShell task allows you to execute PowerShell scripts on a remote PowerShell server using PSRemoting.

* **Host** - FQDN or IP address of the PowerShell host
* **Username** - username to access the PowerShell host
* **Password** - password to access the PowerShell host
* **Use TLS** - enable to connect over TLS
* **Trust self signed certificates** - enable to trust self-signed certificates over TLS
* **Script** - the PowerShell script to execute
* **Arguments** - arguments to the PowerShell script
* **Working Directory** - directory in which to execute the script

{{< img src="powershell-task-config.png" alt="Configure the PowerShell task" >}}
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