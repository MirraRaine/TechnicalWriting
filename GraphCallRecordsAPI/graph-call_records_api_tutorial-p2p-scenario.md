# TUTORIAL: STEP-BY-STEP CALL RECORD SCENARIO INTERPRETATION

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

1. Property: type – [shows call type
   1. Value: peerToPeer
   2. Interpretation: The call was between two people, one calling the other.
2. Property: modalities – [shows call modality]
   1. Value: ["audio"]
   2. Interpretation: The call was audio-only, with no video or screen sharing.
3. Property: organizer_v2 – [shows call organizer]
   1. Value: {"displayName": "Abbie Wilkins", "tenantId": "dc368399-474c-4d40-900c-6265431fd81f"}
   2. Interpretation: Abbie Wilkins organized the call, and she belongs to the tenant organization with ID dc368399-474c-4d40-900c-6265431fd81f.
4. Properties: startDateTime, endDateTime – [start and end time; helps to calculate call duration]
   1. Values: "2020-02-25T18:52:21.2169889Z", "2020-02-25T18:52:46.7640013Z"
   2. Interpretation: The call started at 18:52:21 and ended at 18:52:46, lasting 25 seconds.
5. Property: sessions – [shows interaction between users]
   1. Property: caller – [initiator of the peer-to-peer call]
      1. Value: {"displayName": "Abbie Wilkins", "platform": "android", "productFamily": "teams"}
      2. Interpretation: Abbie Wilkins joined the call from an Android device using the Teams client
   2. Property: callee – [a person who answered the call]
      1. Value: {"displayName": "Owen Franklin", "platform": "windows", "productFamily": "teams", "feedback": {"rating": "poor"}}
      2. Interpretation: Owen Franklin joined from a Windows device using the Teams client and rated the call as poor.
6. Property: segments/media – [shows information about media involved to the call]
   1. Value: {"label": "main-audio", "callerDevice": {"receivedSignalLevel": -10}, "streams": [{"streamDirection": "callerToCallee", "averageJitter": "PT0.016S"}]}
   2. Interpretation:
      1. Received Signal Level: The signal strength was -10, indicating weak audio signals.
      2. Average Jitter: The jitter was 0.016 seconds, which could have caused audio instability.

## Conclusion

By analyzing each component of the call record, you can understand the call’s context, participants, and potential issues. In this example, the poor rating by Owen Franklin was due to weak audio signals and jitter.
