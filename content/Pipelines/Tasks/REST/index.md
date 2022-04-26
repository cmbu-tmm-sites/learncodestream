---
title: "REST"
---

The REST task is a powerful and adaptable task that lets us interact with any standard REST API - this means we can integrate almost any 3rd party system that has a REST API.

**Headers** are common accross all the REST action types and allow you to set the HTTP headers to be sent with the API request - often, but not always, these include `Content-Type`, `Accept` and `Authorization` headers - you'll need to a consult your API documentation to see which headers are required.

{{< hint info >}}
If your API requires specific configuration, you can often save time by creating repeatable API tasks as Pipelines, and nest them within your parent Pipeline using the [Pipeline Task](/pipelines/tasks/pipeline)
{{< /hint >}}

## REST Action types

{{< tabs "REST Task Actions" >}}
{{< tab GET >}}
The GET action is a simple GET request, which only needs the **URL** and any **Headers** to be configured.
{{< img src="rest-get.png" alt="Example REST GET request">}}
{{< /tab >}}

{{< tab POST >}}
The POST request needs the **URL** and **Headers**, as well as a **Payload** - the format of which is determined by the API you're interacting with. In the example below I'm using an output parameter from a previous task  to populate the **Payload**.

{{< img src="rest-post.png" alt="Example REST POST request">}}
{{< hint info >}}
Because Code Stream task outputs are already in JSON format it's normally much simpler to use JSON payloads, like you see in this screenshot. The exported `profileJson` output parameter is a JSON object that I can use directly in the Payload. If your API gives you a choice of Content-Types, I'd use JSON over XML or YAML.
{{< /hint >}}
{{< /tab >}}

{{< tab PUT >}}
{{< /tab >}}

{{< tab PATCH >}}
The PATCH action is most often used to modify an existing object within a REST API - in the example below I'm updating an image profile object. The object ID is supplied as part of the **URL** (`${input.Packer-Build-vRA-Url}/iaas/api/image-profiles/${Release.Create Image Profile JSON.output.exports.imageProfileId}`) and the Payload is the updated object specification.
{{< img src="rest-patch.png" alt="Example REST PATCH request">}}

{{< /tab >}}

{{< tab DELETE >}}
The DELETE action will delete an object, typically based on an identifier in the URL. In this example, the deploymentId is supplied from the output of a previous task - `${input.Packer-Build-vRA-Url}/iaas/api/deployments/${Test.Request Deployment.output.responseJson.deploymentId}`
{{< img src="rest-delete.png" alt="Example REST DELETE request">}}
{{< /tab >}}
{{< /tabs >}}

{{< hint warning >}}
The REST API task will execute more quickly than a [CI task](/pipelines/tasks/ci) or [Custom Integration task](/pipelines/tasks/custom) because it's executed directly within the vRealize Automation appliance (or the vRealize Automation Cloud Proxy Agent) rather than on a [Docker Endpoint](/configure/endpoints/docker). So, although you can often achieve the same outcome with any of these, the REST task might be preferrable.
{{< /hint >}}


## Output Parameters
* `status` - task status
* `responseHeaders` - JSON object representing the HTTP headers
* `responseBody` - String property for the API response
* `responseJson` - JSON object representing the responseBody
* `responseCode` - HTTP response code