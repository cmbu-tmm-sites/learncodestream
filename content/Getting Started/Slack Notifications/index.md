---
Title: "Slack Notifications"
---

Using the webhook function for Pipeline Notifications or Task Notifications and the [Slack Incoming Webhooks app](https://vmware.slack.com/apps/A0F7XDUAZ-incoming-webhooks) it's possible to get a rich set of notifications on pipeline events.

Once your Incoming Webhooks app is configured you will get a URL to post your messages to, and the notification is a simple configuration:

{{< img src="slack-notification-config.png" alt="Configure a Slack Notification" >}}

The Slack payload can be configured as simply, or as complex, as you like:


```json
{
   // Override the default channel and DM - "channel": "@${requestBy}",
   "attachments":[
      {
         "fallback":"[vra8-test-ga] <${executionUrl}|${name}#${executionIndex}> ${status}",
         "pretext":"[vra8-test-ga] <${executionUrl}|${name}#${executionIndex}>",
         "color":"#01FF00",
         "fields":[
            {
               "title":"Details",
               "value":"Pipeline: ${name} (Execution ID: ${executionId})\nExecution Index: ${executionIndex}\nUser: ${requestBy}\nStatus: ${statusMessage}",
               "short":false
            }
         ]
      }
   ]
}
```
{{< img src="slack-notifications.png" alt="Detailed Slack Notification" >}}
