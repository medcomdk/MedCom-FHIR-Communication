# Reliable Messaging using VANSEnvelope

Reliable Messaging in VANSEnvelope

The Reliable Messaging Model and how the flow is laid out using VANSEnvelope is shown below:

![VANSEnvelope reliable messaging](https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/vansenvelope-reliable-messaging.png "VANSEnvelope-reliable-messaging")

A VansEnvelope consists of the following elements:

![VANSEnvelope_schema-reliable](https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/VANSEnvelope_schema-reliable.png  "VANSEnvelope_schema-reliable")

A VansEnvelope's Reliale Messaging part can be found in the VANSEnvelope/Message/MetaInformation/Transport/Type-element:

![VANSEnvelope_schema-reliable-type](https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/VANSEnvelope_schema-reliable-type.png "VANSEnvelope_schema-reliable-type")

Reliable Messaging in VANSEnvelope is the default mode, but can explicitly be turned on and off by setting this VANSEnvelope/Message/MetaInformation/Transport/Type-element to "reliable" or "unreliable".

In FHIR Messaging this element **MUST** be "reliable" or left in default mode.

When "reliable" the receiver of the VANSEnvelope **MUST** send a VANSEnvelopeAcknowledgment return to the original Sender.

When Reliable Messaging is implemented , the Receiver **SHALL** check the incoming EnvelopeIdentifier and Message/MetaInformation/Identifier (hereafter MessageIdentifier) against a cache of previously received VANSEnvelopes. The correct action to take depends on what is received:

| Case                                                            | Description                 |
|:----------------------------------------------------------------|:---------------------------|
| Both EnvelopeIdentifier and MessageIdentifier have not been received      | This is the normal case, and the message **SHALL** be processed            |
| Both EnvelopeIdentifier and MessageIdentifier have already been received  | The original VANSEnvelope has server may either reprocess the message, or reject the message|
| MessageIdentifier has already been received, but EnvelopeIdentifier is new | The original VANSEnvelopeAcknowledgement has been lost (failed to return to the request issuer) and thus the previously received Message in a VANSEnvelope has been resubmitted with a new EnvelopeIdentifier for processing again. The original VANSEnvelopeAcknowledgement **SHALL** be resent|
| The EnvelopeIdentifier has already been received, but the MessageIdentifier is new | This is an error - EnvelopeIdentifier values should never be reused |

The duration period for caching does generally not need to be very long. At a minimum, it could be 1 minute longer than the timeout of the sending system, though it may need to be longer depending on the re-sending policies of the sending system.

Applications that implement Reliable Messaging declare their reliable cache period in their Capability Statement.

### Different Reliable Messaging scenarios using VANSEnvelope

**Update this section with VANSEnvelope specific details**

This section provides a description of the different types of Reliable Messaging scenarios.

Scenario # 1a - Normally successful unsolicidated message or request message flow with acknowledgment request
Scenario # 1b - Duplicate an unchanged message with a positive acknowledgment request
Scenario # 2a - (Re) Sending Unchanged Message
Scenario # 2b - Message is sent normally, acknowledgment is lost along the way
Scenario # 2c - (Re) Sending Modified Message

### Scenario # 1a - Normally successful unsolicidated message or request message flow with acknowledgment request (Google translated)

An unsolicidated message or request message is sent with a new request for a positive acknowledgment from the Sending System to a Receiving System.
The Receiving System **SHALL** always send a positive acknowledgment to the Sending System.

### Scenario # 1b - Duplicate an unchanged message with a positive acknowledgment request (Google translated)

Duplication of an unchanged message can be done in one of the following ways:
• An error may have occurred in the flow from the Sending System to the Receiving System with subsequent duplication of a message in scenario 1a.
• The Sending System may inadvertently send a duplicate of message
The messages are completely identical and as a consequence the message with request for positive acknowledgment arrives at the Receiving System more than once.

The Receiving System **SHALL** ignore the contents of the duplicate instances of the message, but **SHALL** acknowledge a duplicate message in the same way as the original message. A positive acknowledgment may not be sent first and then a negative acknowledgment or vice versa. The Receiving System **SHALL** never display several instances of a message in a message overview, but **SHALL** log in a system log that reception of a duplicate message has taken place. If the Sending System of the message has received acknowledgment already after the Receiving System's acknowledgment of a message's first instance, the Sending System **SHALL** similarly ignore the duplicate instances of the acknowledgment. The Sending System **SHALL** never display multiple instances of the same acknowledgment in a message summary, but **SHALL** log in a system log that acknowledgment of a duplicate has taken place.

### Scenario # 2a - (Re) Sending Unchanged Message (Google translated)

Correct retransmission of a message A.
The Sending System **SHALL** form a new envelope with a new ID and time of dispatch. Since there has been no change in the letter section, the rest of the message remains identical. The message is sent and acknowledged as a completely new message according to Scenario # 1a or # 1b.
Re-dispatches are always done manually and should be in accordance with the normal response time for the specific message flow.

### Scenario # 2b - Message is sent normally, acknowledgment is lost along the way (Google translated)

As Scenario # 1a, but where acknowledgment is lost along the way from the Sending System to the Receiving System.
The shipping pattern is like Scenario # 2a.

### Scenario # 2c - (Re-) Sending Modified Message (Google translated)

If the content of the letter part is changed, the message is considered a completely new message with the consequent change of both EnvelopeId, LetterId and timestamp, where relevant.
Resubmissions are always done manually.

For historical reasons, there has been no requirement to use positive acknowledgments, which is why Scenario # 1a can in practice be run as Scenario # 1b. The Sending System may therefore experience that there is no acknowledgment of acknowledgment of a message, and it is not recommended to make program logic that sends messages.
For a number of standards, however, there is an explicit requirement for a positive acknowledgment, see the documentation for the individual standards if this is the case.#### Reliable Messaging using VANSEnvelope

