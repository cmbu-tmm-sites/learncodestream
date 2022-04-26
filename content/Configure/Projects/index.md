---
title: "Projects"
weight: 610
---

A Project in vRealize Automation is used to scope user access to resources within the platform. For Code Stream this means grouping Administrator, Member or Viewer access to [Pipelines](/pipelines), [Executions](/executions), [User Operations](/user-operations), [Endpoints](/configure/endpoints), [Variables](/configure/variables), and [Triggers](/triggers). A user can be a member of many different projects, and hold different roles in each project.

{{< img src="projects.png" alt="Projects" >}}

## Project Member Permissions
* **Administrator** - Manage Pipelines, Manage Restricted Pipelines, Execute Pipelines, Execute Restricted Pipelines, Manage Executions, Read objects
* **Member** - Manage Pipelines, Execute Pipelines, Read objects
* **Viewer** - Read objects

## Restricted Endpoints/Variables
[Endpoints](/configure/endpoints) and [Variables](/configure/variables) can be marked as restricted, which means that only users with Administrator rights (either Code Stream Administrator, or Project Administrator) can manage them. A [Pipeline](/pipelines) or [Execution](/executions) that uses a restricted Endpoint or Variable will not be accessible to any other user role.

## Links and References
* [How do I manage user access and approvals in Code Stream](https://docs.vmware.com/en/VMware-Code-Stream/services/Using-and-Managing-CodeStream/GUID-8EDC8310-232D-45FB-8C02-E4FB25687177.html#GUID-8EDC8310-232D-45FB-8C02-E4FB25687177)