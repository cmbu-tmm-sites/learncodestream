---
title: "REST"
---

The REST task is a powerful and adaptable task that lets us interact with any REST API.

Headers are common accross all the REST action types and allow you to set headers to be sent with the API request - typically these include a `Content-Type`, `Accept` and `Authorization` headers - however, you'll need to a consult your API documentation to see which headers are required.

{{< hint info >}}
If your API requires specific configuration, you can often save time by creating repeatable API tasks as Pipelines, and nest them within your parent Pipeline using the [Pipeline Task](/Pipelines/Tasks/Pipeline)
{{< /hint >}}

## REST Action types

{{< tabs "REST Task Actions" >}}
{{< tab GET >}}
{{< img src="rest-get.png" alt="Example REST GET request">}}
{{< /tab >}}

{{< tab POST >}}
{{< img src="rest-post.png" alt="Example REST POST request">}}
{{< /tab >}}

{{< tab PUT >}}
{{< /tab >}}

{{< tab PATCH >}}
`${input.Packer-Build-vRA-Url}/iaas/api/image-profiles/${Release.Create Image Profile JSON.output.exports.imageProfileId}`
{{< img src="rest-patch.png" alt="Example REST PATCH request">}}

{{< /tab >}}

{{< tab DELETE >}}
`${input.Packer-Build-vRA-Url}/iaas/api/deployments/${Test.Request Deployment.output.responseJson.deploymentId}`
{{< img src="rest-delete.png" alt="Example REST DELETE request">}}
{{< /tab >}}
{{< /tabs >}}

{{< hint info >}}
The REST API task will execute more quickly than a [CI task](/Pipelines/Tasks/CI) or [Custom Integration task](/Pipelines/Tasks/Custom) because it's executed directly within the vRealize Automation appliance, or the vRealize Automation Cloud Proxy Agent, rather than on a [Docker Endpoint](/Configure/Endpoints/Docker). So, although you can often achieve the same outcome with any of these, the REST task might be preferrable.
{{< /hint >}}


## Output Parameters
* `status` - task status
* `responseHeaders` - JSON object representing the HTTP headers
* `responseBody` - String property for the API response
* `responseJson` - JSON object representing the responseBody
* `responseCode` - HTTP response code