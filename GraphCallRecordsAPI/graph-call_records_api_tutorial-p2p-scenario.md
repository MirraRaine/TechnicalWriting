# TUTORIAL: CALL RECORD SCENARIO INTERPRETATION

This tutorial will guide you through interpreting a call record received from the Graph Call Records API. You will use an example call record to understand each component and what it signifies.

## Call Record Example

Note: The given JSON example is not complete and is provided just for the sake of this tutorial.

``` json
{
  "version": 1,
  "type": "peerToPeer",
  "modalities": [ "audio" ],
  "startDateTime": "2020-02-25T18:52:21.2169889Z",
  "endDateTime": "2020-02-25T18:52:46.7640013Z",
  "id": "e523d2ed-2966-4b6b-925b-754a88034cc5",
  "organizer_v2": {
    "identity": {
      "user": {
        "displayName": "Abbie Wilkins",
        "tenantId": "dc368399-474c-4d40-900c-6265431fd81f"
      }
    }
  },
  "sessions": [
    {
      "caller": {
          "platform": "android", "productFamily": "teams"
        },
        "associatedIdentity": {
          "displayName": "Abbie Wilkins",
          "tenantId": "dc368399-474c-4d40-900c-6265431fd81f",
        }
      },
      "callee": {
        "userAgent": {
          "platform": "windows", "productFamily": "teams"
        },
        "associatedIdentity": {
          "displayName": "Owen Franklin",
          "tenantId": "dc368399-474c-4d40-900c-6265431fd81f",
        },
        "feedback": { "rating": "poor" }
      },
      "segments": [
        {
          "media": [
            {
              "label": "main-audio",
              "callerDevice": {
                "receivedSignalLevel": -10
              },
              "streams": [
                {
                  "streamDirection": "callerToCallee",
                  "averageJitter": "PT0.016S"
                }
        ...
```

## Call Record Scenario Interpretation

In this section, you will break down the call record into its individual components and find out what each part represents. This will help you understand the context, participants, and any potential issues with the call.

### Interpret 'type' property

* **Desription**: the property shows call type
* **Value**: `peerToPeer`
* **Interpretation**: The call was between two people, one calling the other.

### Interpret 'modalities' property

* **Desription**: shows call modality
* **Value**: `["audio"]`
* **Interpretation**: The call was audio-only, with no video or screen sharing.

### Interpret 'organizer_v2' property
* **Desription**: shows organizer of the call
* **Value**: `{"displayName": "Abbie Wilkins", "tenantId": "dc368399-474c-4d40-900c-6265431fd81f"}`
* **Interpretation**: Abbie Wilkins organized the call, and she belongs to the tenant organization with ID dc368399-474c-4d40-900c-6265431fd81f.

### Interpret 'startDateTime', 'endDateTime' properties
* **Desription**: start and end time of the call; helps to calculate call duration
* **Value**: `"2020-02-25T18:52:21.2169889Z"`, `"2020-02-25T18:52:46.7640013Z"`
* **Interpretation**: The call started at 18:52:21 and ended at 18:52:46, lasting 25 seconds.

### Interpret 'sessions' property
* **Desription**: shows interaction between users
* **Value**: `{"displayName": "Abbie Wilkins", "platform": "android", "productFamily": "teams"}`
* **Interpretation**: Abbie Wilkins joined the call from an Android device using the Teams client

#### Interpret 'caller' property
* **Desription**: initiator of the peer-to-peer call
* **Value**: `{"displayName": "Abbie Wilkins", "platform": "android", "productFamily": "teams"}`
* **Interpretation**: Abbie Wilkins joined the call from an Android device using the Teams client

#### Interpret 'callee' property
* **Desription**: a person who answered the call
* **Value**: `{"displayName": "Owen Franklin", "platform": "windows", "productFamily": "teams", "feedback": {"rating": "poor"}}`
* **Interpretation**: Owen Franklin joined from a Windows device using the Teams client and rated the call as poor.

### Interpret 'segments/media' property
* **Desription**: shows information about media involved to the call
* **Value**: `{"label": "main-audio", "callerDevice": {"receivedSignalLevel": -10}, "streams": [{"streamDirection": "callerToCallee", "averageJitter": "PT0.016S"}]}`
* **Interpretation**:
   * Received Signal Level: The signal strength was -10, indicating weak audio signals.
   * Average Jitter: The jitter was 0.016 seconds, which could have caused audio instability.

## Conclusion

By analyzing each component of the call record, you can understand the call’s context, participants, and potential issues. In this example, the poor rating by Owen Franklin was due to weak audio signals and jitter.
