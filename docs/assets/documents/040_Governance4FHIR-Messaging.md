# &nbsp; &nbsp;

## 4. Governance for MedCom FHIR Messaging

This Governance for MedCom FHIR Messaging includes the corresponding OIOXML version of certain MedCom FHIR Messages, that are developed with the FHIR Message as the definer of the content of the OIOXML version.

FHIR Resources can be used in a traditional messaging context, much like HL7 v2.
<!-- Applications asserting conformance to this framework claim to be conformant to "FHIR messaging". -->

In FHIR messaging, a "request message" or an "unsolicited message" is sent from a source application (Sending System) to a destination application (Receiving System) when an event happens. Events mostly correspond to things that happen in the real world.

The message consists of a Bundle identified by the type "message", with the first resource in the Bundle being a MessageHeader resource. The MessageHeader resource has a code - the message event - that identifies the nature of the message, and it also carries additional metadata. The other resources in the Bundle depend on the type of the message, eg. in which context a message is triggered.

The events supported in MedCom FHIR Messaging, along with the resources that are included in them, are defined in: [MedCom FHIR Messaging events](/assets/documents/MedCom-FHIR-Messaging-Events.md).

The destination application processes the message and returns an acknowledgement message and maybe one or more response messages, which too are a Bundle of resources identified by the type "message", with the first resource in each Bundle being a MessageHeader resource with a response section that reports the outcome of processing the message and any additional response resources required.

### 4.1 Basic Danish Messaging Assumptions [TBD]

This specification assumes that content will be delivered from one application to another by some delivery mechanism, and then one or more responses will be returned to the source application.

In Denmark this specification rules the exchange of messages through the Danish Messaging Network, currently known as VANS, and using the central organization register, SOR, for delivering the virtual adressing information.

The agreements around the content of the messages and the behavior of the two applications form the "contract" that describes the exchange. These contracts are exactly what MedCom delivers in the Danish Healthcare Domain and therefore MedCom adds regional and local agreements to the rules defined in the HL7 FHIR®© specification.
toThis specification ignores the existence of interface engines and message transfer agents that exist between the source and destination. Either they are transparent to the message/transaction content and irrelevant to this specification, or they are actively involved in manipulating the message content (in particular, the source and destination headers are often changed). If these middleware agents are modifying the message content, then they become responsible for honoring the contract that applies (including applicable profiles) in both directions.

### 4.2 Message Exchange Patterns

Each MedCom FHIR message has one or more response messages. There **SHALL** be at least one response message, an acknowledgement message, so that the sender can know, that the message was properly received.

Multiple response messages **SHALL NOT** be returned for messages of consequence, and **SHOULD** not be returned for notifications.

In principle, source applications **SHOULD** not wait for a response to a transaction before issuing a new transaction. However, in many cases, the messages in a given stream are dependent on each other, and must be sent and processed in order. In addition, some transfer methods may require sequential delivery of messages.

### 4.3 Reliable Messaging using MedCom FHIR Messaging

FHIR Messaging is developed to support Reliable Messaging.
MedCom FHIR Messages **SHALL** make use of this Reliable Messaging functionality.

[Tap here to see how to set up Reliable Messaging using MedCom FHIR Messaging](/assets/documents/Reliable_Messaging-FHIR.md)

### 4.4 Handling sending scenarios

#### 4.4.1 Sending to a primary receiver

When sending to a primary receiver the Receiving Organization **SHALL** be pointed out/referenced by destination:primary/receiver in MedComMessagingMessageHeader.

#### 4.4.2 Sending to a primary receiver with an already known copyreciver

When sending to a primary receiver the Receiving Organization **SHALL** be pointed out/referenced by destination:primary/receiver in MedComMessagingMessageHeader.

When also sending to a copyreciver the Receiving Organization representing this **SHALL** be pointed out/referenced by destination:cc/receiver in MedComMessagingMessageHeader.

Both elements **SHALL** be represented.

#### 4.4.3 Sending a copy of a message

A CopyReceiver is a ccreceiver of the same message dispatched transaction to a primary receiver.

A Forwardreceiver is a fwdreceiver of a message dispatched transaction unlinked to the original message transaction

##### 4.4.3.1 Sending to a copyreceiver while also sending to a Primary receiver

A message to a copyreceiver is as the name says a copy of the original message.

Sending to a copyreceiver is handled on different levels:

- VANSenvelope: The VANSEnvelope **SHALL** be made with the copyreceiver's GLN as the receiving EAN.
- MedComFHIRMessage: The MedComMessagingProvenance **SHALL** reflect the scenario by adding a copyreceiver element to the stack of MedComMessagingProvenances.
- MedComFHIRMessage: The Messageheader **SHALL NOT** be changed
- MedComFHIRMessage: The Bundle.id and Timestamp **SHALL** be changed

##### 4.4.3.2 Forwarding a message

A forwarded message to a new receiver not present in the construction and dispatching of the original message.

Forwarding is handled on different levels

- VANSenvelope: The VANSEnvelope **SHALL** be made with the copyreceiver's GLN as the receiving EAN.
- MedComFHIRMessage: The MedComMessagingProvenance **SHALL** reflect the scenario by adding a forwarding element to the stack of MedComMessagingProvenances.
- MedComFHIRMessage: The Messageheader **SHALL NOT** be changed
- MedComFHIRMessage: The Bundle.id and Timestamp **SHALL** be changed

### 4.5 Handling receiving scenarios

Lorem ipsum
