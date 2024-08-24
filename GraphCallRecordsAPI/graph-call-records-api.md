# API: MICROSOFT GRAPH CALL RECORDS API

Microsoft Graph Call Records API offers usage and diagnostic insights for calls made within a business organization that uses Microsoft Teams or Skype for Business. A call record provides detailed information about the call, such as start and end time, joined participants, devices, network, and other aspects. Additionally, the call record reflects user feedback on call quality and captures quality metrics for audio, video, and screen sharing during the call. The Call Records API offers many more details that can be used by administrators to assess overall call quality and troubleshoot issues.

## Resource

GET /communications/callRecords/{id}

Get call diagnostic information by call id

## Parameters

This section covers all parameters to cnfigure in order to call Graph Call Records API.

### Path parameters

| Parameter     | Required/Optional     | Description   |
| ------------- | ------------- | ------------- |
| id | Required | Id of the call made in the organization |

### Query string parameters

| Parameter     | Required/Optional     | Description   |
| ------------- | ------------- | ------------- |
| $expand | Optional | Use the $expand query parameter to include the expanded resource of participants_v2, sessions or segments.  |
| $select | Optional | Use the $select query parameter to return a set of properties, for example, to overview id and startDateTime. Only supported for callRecord and session resources. |

### Request Header parameters

| Parameter     | Required/Optional     | Description   |
| ------------- | ------------- | ------------- |
| Authorization | Required | Bearer token. How to get the token instruction.|
| Prefer: odata.maxpagesize={x} | Optional | Specifies a preferred integer {x} page size for paginated results. This value must be equal to or less than 60.|
| Prefer: omit-values=nulls | Optional | Removes null or empty values from the call record response. |

## Example Request

<table border="0" style="border:2px solid #4169E1;" >
 <tr>
    <td>
    GET https://graph.microsoft.com/v1.0/communications/callRecords/e523d2ed-2966-4b6b-925b-754a88034cc5
    </td>
 </tr>
</table>

> ![NOTE]
> Replace e523d2ed-2966-4b6b-925b-754a88034cc5 with your actual call id

## Example Response

This is a sample response from the /communications/callRecords/{id} endpoint:

``` json
HTTP/1.1 200 OK
Content-type: application/json
{
  "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#communications/callRecords/$entity",
  "version": 1,
  "type": "peerToPeer",
  "modalities": [
    "audio"
  ],
  "lastModifiedDateTime": "2020-02-25T19:00:24.582757Z",
  "startDateTime": "2020-02-25T18:52:21.2169889Z",
  "endDateTime": "2020-02-25T18:52:46.7640013Z",
  "id": "e523d2ed-2966-4b6b-925b-754a88034cc5",
  "organizer_v2@odata.context": "https://graph.microsoft.com/v1.0/$metadata#communications/callRecords('e523d2ed-2966-4b6b-925b-754a88034cc5')/organizer_v2/$entity",
  "organizer_v2": {
    "id": "821809f5-0000-0000-0000-3b5136c0e777",
    "identity": {
      "user": {
        "id": "821809f5-0000-0000-0000-3b5136c0e777",
        "displayName": "Abbie Wilkins",
        "tenantId": "dc368399-474c-4d40-900c-6265431fd81f"
      }
    }
  },
  "participants_v2@odata.context": "https://graph.microsoft.com/v1.0/$metadata#communications/callRecords('e523d2ed-2966-4b6b-925b-754a88034cc5')/participants_v2/$entity"
}
```

## Response Schema

Table 1: The table describes each item in the response.

|    Element            | Type          | Description                                                                                   |
| -------------- | ------------- | ----------------------------------------------------------------------------------------------- |
| id             | String        | A unique identifier for the call, which also serves as the identifier for the call record.   |
| version        | Int64         | Represents the version of the call record, which increases each time the system generates a new call record. The higher the version of a call record, the more data it contains. |
| type           | Enum          | Indicates the type of the call. Values are unknown, groupCall, peerToPeer, unknownFutureValue. |
| modalities     | Array[String] | List of all the modalities used in the call. Values are unknown, audio, video, videoBasedScreenSharing, data, screenSharing, unknownFutureValue. |
| lastModifiedDateTime | String (timestamp) | UTC time when the call record was created. |
| startDateTime  | String (timestamp) | UTC time when the first user joined the call. |
| endDateTime    | String (timestamp) | UTC time when the last user left the call. |
| organizer_v2   | Object        | Information about the call organizer. |
| organizer_v2/id | String        | Unique identifier for the call organizer. |
| organizer_v2/identity | Object  | The identity of the call organizer. |
| organizer_v2/identity/user | Object | The user associated with the organizer. |
| organizer_v2/identity/user/id | String | The organizer's unique identifier (object id). |
| organizer_v2/identity/user/displayName | String | The organizer’s name. |
| organizer_v2/identity/user/tenantId | String | The organizer’s tenant id (organization id). |
| sessions       | Array[Object] | List of sessions involved in the call. Peer-to-peer calls usually have one session, while group calls have at least one session per participant. |
| sessions[0]    | Object        | Represents a user-user communication of a per-to-peer call or a user-server communication in the case of a conference call. |
| participants_v2 | Array        | List of distinct participants in the call. |
| participants_v2[0] | Object      | Represents the identity of a participant attended a call record. |
| joinWebUrl     | String        | Meeting URL associated with the call. |
| sessionsNextLink | String       | The link to access the next page of sessions. |
| participantsNextLink | String   | The link to access the next page of participants_v2. |

## Multiple Request Examples

Table 2: The table provides example uses and their corresponding URL with the query parameters.

| URL | Usage |
| --- | --- |
| GET /communications/callRecords/{id} | Retrieves call diagnostic information by call id. |
| GET /communications/callRecords/{id}?$select=type,startDateTime,endDateTime | Retrieves call type, start and end time of the call by its id. |
| GET /communications/callRecords/{id}/sessions | Retrieves a list of sessions associated with a specific call record. |
| GET /communications/callRecords/{id}/sessions?$expand=segments | Retrieves sessions associated with a specific call record, including the segments within each session. |
| GET /communications/callRecords/{id}?$expand=sessions | Retrieves a call record by its id, including the sessions associated with the call record. |
| GET /communications/callRecords/{id}?$expand=sessions($expand=segments) | Retrieves a call record by its id, including the sessions and segments within each session. |
| GET /communications/callRecords/{id}/participants_v2 | Retrieves a list of participants attended a peer-to-peer or a meeting call. |
| GET /communications/callRecords/{id}/?$expand=participants_v2 | Retrieves a call record by its id, including the participants associated with the call. |
| GET /communications/callRecords | Retrieves a list of call records that occurred in the tenant organization for the past 30 days. |
| GET communications/callRecords?$filter=participants_v2/any(p:p/id eq '{participantId}') | Retrieves call records of the calls that occurred in the organization tenant over the past 30 days and include a specific participant id. |
| GET /communications/callRecords?$filter=startDateTime ge {startDate} and startDateTime lt {endDate} | Retrieves call records that occurred in the organization tenant within a specified date range. |
| GET /communications/callRecords?$filter=startDateTime ge {startDate} and startDateTime lt {endDate} and participants_v2/any(p:p/id eq '{participantId}') | Retrieves call records of the calls that occurred in the organization tenant within a specified date range for a specific participant id. |

