---
title: "Pipelines"
weight: 500
---
A Pipeline is the primary mechanism for sequencing all the tasks that need to be performed, and is compose of one or more Stage, with one or more tasks in each stage:

- A [Stage](/Pipelines/Stages) is an encapsulation mechanism for tasks and are used for grouping the individual task execution statuses and results. 

- A [Task](/Pipelines/Tasks) performs individual actions based on its type and configuration.  Tasks can deploy [VMware Cloud Templates](Tasks/cloudtemplate), and perform actions on configured endpoints, or more generic tasks such as prompting for user interations with [User Operation](/User-Operations), polling a 3rd party data source with the [Poll](/Pipelines/Tasks/poll/) task, or even perform a REST call.



### Pages in this section
{{< toc-tree >}}


Refs:
[Creating and using pipelines in vRealize Automation Code Stream](https://docs.vmware.com/en/vRealize-Automation/8.3/Using-and-Managing-CodeStream/GUID-A2BB3A55-E42D-428C-8F7F-9EBE4AECD5FD.html)