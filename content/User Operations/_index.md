---
title: "User Operations"
weight: 300
---

User Operations provide a way to include approvals within a Pipeline Execution, using the [User Operation Task](/Pipelines/Tasks/User-Operation). The User Operations page provides a dashboard of all Active and Inactive user operations that the logged on user is named in the Approvers list for. Users with administrative rights in Code Stream or the [Project](/Configure/Projects) can view, approve or reject User Operations that they are not in the Approvers lists for.

{{< img src="user-operation-approval.png" alt="Approve or Reject an Active User Operation" >}}

Until a user in the Approvers list approves or rejects the pipeline task, the pipeline remains stopped. If the required user does not address the User Operation in the time allowed, the pipeline will expire.

The Inactive Items list shows a historical view of all the User Operations that are not Active.

For more information on configuring User Operatiosn, see the [User Operation task](/Pipelines/Tasks/User-Operation) page.