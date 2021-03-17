---
title: "Projects"
weight: 610
---

A Project in vRealize Automation is used to scope user access to resources within the platform. For Code Stream this means grouping Administrator, Member or Viewer access to [Pipelines](/Pipelines), [Executions](/Executions), [User Operations](/User-Operations), [Endpoints](/Configure/Endpoints), [Variables](/Configure/Variables), and [Triggers](/Triggers). A user can be a member of many different projects, and hold different roles in each project.

{{< img src="projects.png" alt="Projects" >}}

## Project Member Permissions
* **Administrator** - Manage Pipelines, Manage Restricted Pipelines, Execute Pipelines, Execute Restricted Pipelines, Manage Executions, Read objects
* **Member** - Manage Pipelines, Execute Pipelines, Read objects
* **Viewer** - Read objects

## Restricted Endpoints/Variables
[Endpoints](/Configure/Endpoints) and [Variables](/Configure/Variables) can be marked as restricted, which means that only users with Administrator rights (either Code Stream Administrator, or Project Administrator) can manage them. A [Pipeline](/Pipelines) or [Execution](/Executions) that uses a restricted Endpoint or Variable will not be accessible to any other user role.

## References
* [How do I manage user access and approvals in Code Stream](https://docs.vmware.com/en/VMware-Code-Stream/services/Using-and-Managing-CodeStream/GUID-8EDC8310-232D-45FB-8C02-E4FB25687177.html#GUID-8EDC8310-232D-45FB-8C02-E4FB25687177)