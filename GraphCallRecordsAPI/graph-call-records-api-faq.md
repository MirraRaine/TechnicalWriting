# FAQ: FREQUENTLY ASKED QUESTIONS

## What is the Microsoft Graph Call Records API?

Microsoft Graph Call Records API (also known as Call Records API) offers usage and diagnostic insights for calls made within a business organization, called a tenant, using Microsoft Teams or Skype for Business. Tenants can leverage the call records API to subscribe to, list, and retrieve call records by their ids, as well as to look up calls for a participant. For more details, please refer to the [Working with the call records API in Microsoft Graph](https://learn.microsoft.com/graph/api/resources/callrecords-api-overview).

## How do I request a call record using the Graph Call Records API?

To request a call record, you need to make a GET request to the `/communications/callRecords/{id}` endpoint, where `{id}` is the unique identifier of the call. Ensure you have the necessary __CallRecords.Read.All__ permission and include the Authorization header with a valid bearer token. For more details, please refer to the  [Get callRecord documentation](https://learn.microsoft.com/graph/api/callrecords-callrecord-get).

## What permissions are required to use the Call Records API?

To access call records in Microsoft Graph, the administrator must grant the __CallRecords.Read.All__ permission. For more details, please refer to the [Microsoft Graph permissions reference](https://learn.microsoft.com/graph/permissions-reference).

## How long are call records retained?

Call records are retained for 30 days after a call ends.

## Can I retrieve call records older than 30 days?

No, the Call Records API does not return call records older than 30 days. Requests for such records will result in a 404 Not Found response.

## Where can I find the call ids of calls that occurred in my organization?

Four options to find and collect call ids exist.

**Option 1**: You can subscribe to [change notifications feed](https://learn.microsoft.com/graph/changenotifications-for-callrecords). This will allow you to receive notifications containing call ids whenever a new call record is created.

**Option 2**: You can request [List callRecords API](https://learn.microsoft.com/graph/api/callrecords-cloudcommunications-list-callrecords) that will supply you with the call ids list.

**Option 3**: If you are a [Call Analytics](https://learn.microsoft.com/microsoftteams/use-call-analytics-to-troubleshoot-poor-call-quality) customer, you can manually search for a call id in a user’s history. However, there is no automated system available to retrieve all call ids from Call Analytics.

**Option 4**: You can use the callChainId of a [Get call](https://learn.microsoft.com/graph/api/resources/call) API to look up the call id once the call is completed. However, note that [Get call API](https://learn.microsoft.com/graph/api/resources/call) is not served by Graph Call Records API and in some cases, the `callChainId` may differ from the call id of your call record. Therefore, this method is less preferred compared to other options.

## Why does a call record have missing fields?

A call record can have missing fields due to delayed telemetry from a client. When new telemetry data becomes available, the system generates a new call record with the updated information and increments the version property number. If you are missing properties on your call record, please wait for the next version to become available. 
If the new call record version does not arrive, please, open a [Support Ticket](https://developer.microsoft.com/en-us/graph/support) the Graph Call Records API team.

## When will my call record be available?

On average, Graph Call Records service generates a new call record and [sends a notification](https://learn.microsoft.com/graph/api/resources/subscription?#latency) within 15 minutes after a call ends. However, it can take up to 60 minutes for the service to make the call record available.

## Why is my call record notification delayed?

It can take up to 60 minutes for the service to make the call record available. If you experience a longer delay, check for any reported outages by the Graph Call Records API team by navigating to the “Health” tab in the [Teams Admin Portal](https://admin.teams.microsoft.com/). Additionally, you can open [Support Ticket](https://developer.microsoft.com/en-us/graph/support) the Graph Call Records API team.

## I had hundreds of users on a meeting call. Why do I see only 60 users in participants property of a call record?

When you request a call record, the participants property is populated based on participants from the first 60 session where 60 is the maximum page size allowed on sessions. For more details, please refer to the [How to retrieve all participants who attended a call](graph-call-records-api_manual_participants.md).

## How to interpret/understand a scenario?

Please, refer to the [step-by-step call record scenario](graph-call_records_api_tutorial-p2p-scenario.md) interpretation tutorial.

### Why do I receive a 404 Not Found error?

There are several reasons you might encounter a 404 Not Found error:

**Recent Call**: If the call was made within the last 60 minutes, the call record might not have been generated yet. Please wait and try again in an hour.

**Old Call**: If the call is older than 30 days, the Graph Call Records API returns a 404 Not Found error by design.

**Other Issues**: If neither of the recent or old call reasons apply, check for any reported outages by the Graph Call Records API team by navigating to the “Health” tab in the [Teams Admin Portal](https://admin.teams.microsoft.com/)

Additionally, you can open [Support Ticket](https://developer.microsoft.com/en-us/graph/support) the Graph Call Records API team for the assistance.
