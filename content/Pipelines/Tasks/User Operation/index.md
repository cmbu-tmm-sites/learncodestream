---
title: "User Operation"
---

User Operations provide a way to include approvals within a Pipeline Execution. The [User Operations dashboard](/user-operations) provides a view of all Active and Inactive user operations.

* **Approvers** - email addresses of users who can approve or reject the task. You can use the `${requestBy}` variable to access the requesting user's ID
* **Approver Groups** - *(Currently vRA Cloud)* email addresses of groups who can approve or reject the task
* **Summary** - summary of the approval, used for the subject of the email sent if configured
* **Description** - description of the approval task, the body of the email sent if configured
* **Exires after** - the time after which the approval task will expire and the pipeline execution will be cancelled
* **Send Email** - if enabled, the Email server option can be configured to send the email
* **Cancel pending tasks** - if enabled, this will cancel any outstanding previous approvals for this pipeline
* **Email server** - the [Email Endpoint](/configure/endpoints/email) used to send email notifications

{{< img src="user-operation-config.png" alt="User Operations" >}}

## Output Parameters
* `status`
* `responderRoles`
* `respondedByEmail`
* `comments`
* `respondedBy`
* `index`
* `respondedOnInMicros`