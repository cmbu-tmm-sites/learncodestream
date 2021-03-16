---
title: "Poll"
---

The Poll task is most commonly used in combination with the REST task to Poll for a job completion status, however, it can be used to Poll any HTTP server and wait for a success or failure criteria to be evaluated - or a timeout to expire.

### Poll Request
* **URL** - this is the URL that the Poll task should poll
* **Count** - how many times should the Poll task attempt to access the URL
* **Interval (in seconds)** - how long should the Poll task pause between attempts to access
* **Ignore Intermediate Failure** - ignore intermediate failures, useful if you're waiting for a service to become available before you can poll it
* **Headers** - which headers should be sent with the request (e.g. `Accept: application/json`, `Content-Type: application/json`, `Authorization: Bearer 4DFJGR...`)

### Exit Criteria

* **Success Condition** - if this evaluates to `true` then the task will return a success, and the pipeline will continue.
* **Failure Condition** - if this evaluates to `true` then the task will return a failure, and the pipeline will halt (unless [Continue on failure](/Pipelines/Tasks/#precondition-and-continue-on-failure) is checked)

For example, the below Poll task is configured to query the status of an Image Enumeration task in Cloud Assembly, and wait for either a status of `FINISHED` or `FAILED`. 

{{< img src="poll-configuration.png" alt="Poll task configuration" >}}

The JSON values returned in the body of the response will are available as properties to test, so in the JSON response below the property `status` can be evaluated for both the success and failure condition, with the value determining which condition is triggered.

```json
{
    "progress":100,
    "status":"FINISHED",
    "name":"Private image enumeration",
    "id":"fb719d5a-f30d-4467-9622-31b765b9d369",
    "selfLink":"/iaas/api/request-tracker/fb719d5a-f30d-4467-9622-31b765b9d369"
}
```

## Task Outputs
* `status`
* `iterationCount`
* `pollCount`
* `expectedResponse`
* `responseHeaders`
* `responseBody`
* `interval`
* `processedUrl`
* `responseJson`
* `inputHeaders`
* `responseCode`