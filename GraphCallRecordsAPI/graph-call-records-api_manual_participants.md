# PRODUCT MANUAL: HOW TO RETRIEVE ALL PARTICIPANTS WHO ATTENDED A CALL

There are multiple options to collect all participants who attended a call.

## Option 1: participants_v2 API

Use the List List participants_v2 API to collect the full list of participants for a requested call id.

## Option 2: participants property

Use the Get callRecord API. Retrieve the participants property from a call record response to collect the participants who attended the call. 
Please note that the participants property can contain a maximum of 60 participants because they are aggregated from the first 60 sessions. 60 is the maximum allowed page size for the returned sessions. If your call had more than 60 participants, the list will be incomplete.

## Option 3: custom participants list

To see all participants, implement a custom solution to build the participants list from the call records data:

1. Call Get callRecord API with expanded sessions endpoint: /communications/callRecords/{id}?$expand=sessions
2. Read the sessions@odata.nextLink property value from the response. For example, https://graph.microsoft.com/v1.0/communications/callRecords/{callId}/sessions?$skiptoken={abc}
3. Repeat the next steps until the sessions@odata.nextLink is empty or null
   1. Send the GET request to the sessions@odata.nextLink URL
   2. Read caller property from each session on the received sessions list
   3. Build the participants list based on the caller identity by collecting id, displayName, and other properties you require to collect for a participant
