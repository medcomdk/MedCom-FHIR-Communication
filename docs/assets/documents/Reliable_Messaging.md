# Reliable Messaging

When reliable messaging is implemented , the Receiver SHALL check the incoming Bundle.id and MessageHeader.id against a cache of previously received messages. The correct action to take depends on what is received:

| Case                                                            | Description                 |
|:----------------------------------------------------------------|:---------------------------|
| Both Bundle.id and MessageHeader.id have not been received      | This is the normal case, and the message should be processed            |
| Both Bundle.id and MessageHeader.id have already been received  | The original response has been lost (failed to return to the request issuer), and the original response SHALL be resent|
| MessageHeader.id has already been received, but Bundle.id is new | A previously seen message has been resubmitted for processing again. The server may either reprocess the message, or reject the message|
| The Bundle.id has already been received, but the MessageHeader.id is new | This is an error - Bundle.id values should never be reused |

The duration period for caching does generally not need to be very long. At a minimum, it could be 1 minute longer than the timeout of the sending system, though it may need to be longer depending on the re-sending policies of the sending system.

Applications that implement reliable messaging declare their reliable cache period in their Capability Statement.
