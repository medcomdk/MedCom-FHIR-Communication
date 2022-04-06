# Communication Rules

||||
|:---|---|:---|
|[FHIR Messaging](#fhir-messaging)            ||[Network Envelope](#network-envelope)|
|[MedCom FHIR messages](#medcom-fhir-messages)||[Network Layer](#network-layer)|
|[Reliable Messaging](#reliable-messaging)    ||[Test and Certification](#test-and-certification)|

# Introduction

Some general HL7 FHIR Communication Rules can be found on the [HL7 FHIR R4 Website](http://hl7.org/fhir/R4/messaging.html). What you will find here is, how MedCom has profiled the HL7 FHIR Messaging Framework to work in a Danish context.
[Introduction details](/assets/documents/01-Introduction.md)

[Generelle tekniske use cases](/assets/documents/Generelle-tekniske-use-cases-v1.0.0-b1.md)

## FHIR Messaging

FHIR Resources can be used in a traditional messaging context, much like HL7 v2. Applications asserting conformance to this framework claim to be conformant to "FHIR messaging".

In FHIR messaging, a "request message" or an "unsolicidated message" is sent from a source application to a destination application when an event happens. Events mostly correspond to things that happen in the real world.
The message consists of a Bundle identified by the type "message", with the first resource in the bundle being a MessageHeader resource. The MessageHeader resource has a code - the message event - that identifies the nature of the message, and it also carries additional metadata. The other resources in the bundle depend on the type of the message.

The events supported in MedCom FHIR Messaging, along with the resources that are included in them, are defined in [here](/assets/documents/MedCom-FHIR-Messaging-Events.md).

The destination application processes the message and returns an acknowledgment message and one or more response messages, which are also a bundle of resources identified by the type "message", with the first resource in each bundle being a MessageHeader resource with a response section that reports the outcome of processing the message and any additional response resources required.

### Basic Messaging Assumptions [TBD]

This specification assumes that content will be delivered from one application to another by some delivery mechanism, and then one or more responses will be returned to the source application.

In Denmark this specification rules the exchange of messages through the Danish Messaging Network, currently known as VANS, and using the central organization register, SOR, for delivering the virtual adressing information.

The agreements around the content of the messages and the behavior of the two applications form the "contract" that describes the exchange. These contract is exactly what MedCom delivers in a the Danish Healthcare Domain and therefore adds  regional and local agreements to the rules defined in the HL7 FHIR specification.

This specification ignores the existence of interface engines and message transfer agents that exist between the source and destination. Either they are transparent to the message/transaction content and irrelevant to this specification, or they are actively involved in manipulating the message content (in particular, the source and destination headers are often changed). If these middleware agents are modifying the message content, then they become responsible for honoring the contract that applies (including applicable profiles) in both directions.

### Message Exchange Patterns

Each MedCom FHIR message has one or more response messages. There must be at least one response message so that the sender can know that the message was properly received. Multiple response messages SHALL NOT be returned for messages of consequence, and SHOULD not be returned for notifications.

In principle, source applications are not required to wait for a response to a transaction before issuing a new transaction. However, in many cases, the messages in a given stream are dependent on each other, and must be sent and processed in order. In addition, some transfer methods may require sequential delivery of messages.

#### Asynchronous

In Asynchronous messaging, the server acknowledges receipt of the message immediately, and responds to the sender separately. The server may respond more than once to any given message.
When a message is received, a receiver can determine from the content of the message header whether it's a new message to process, or a response to a message that has already been sent.

## MedCom FHIR Messages

![alt text](https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/MessagingModel.png "MedCom Messaging Model")

- MedCom FHIR Messages SHALL contain at least one bundled MedComMessagingHeader resource
-- The MedComMessagingHeader resource SHALL be the first resource in a MedCom Message Bundle
- MedCom FHIR Messages SHALL contain at least two bundled MedComMessagingOrganization resources
-- One of the two bundled MedComMessagingOrganization resources SHALL repsresent the Sender Organization
-- One of the two bundled MedComMessagingOrganization resources SHALL repsresent the Receiver Organization
- MedCom FHIR Messages SHALL contain at least one bundled MedComMessagingProvenance resource

[here](https://github.com/hl7dk/dk-medcom-messaging/blob/master/input/pagecontent/index.md)

[Permalink here](https://github.com/hl7dk/dk-medcom-messaging/blob/b23dfe00cba8aba273ca08ab7eead8228952f6c4/input/pagecontent/index.md)

### MessageHeader

![alt text](https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/MedComMessageHeader.png "MedCom Messaging Model")

[here](/assets/documents/MessageHeader.md)

### Identifiers

[here](/assets/documents/MessageHeader_Identifiers.md)

### Timestamps

[here](/assets/documents/MessageHeader_Timestamps.md)

### Messaging rules

[Danish here](/assets/documents/Rules_Messaging-DA.md)
[English here](/assets/documents/Rules_Messaging-EN.md)

### Acnowledgment rules

[Danish here](/assets/documents/Rules_Acknowledgment-DA.md)
[English here](/assets/documents/Rules_Acknowledgment-EN.md)

## MustSupport

[here](/assets/documents/MustSupport.md)

## Provenance

- MedCom FHIR Messages SHALL contain at least one bundled MedComMessagingProvenance resource
- MedCom FHIR Messages SHALL contain one bundled MedComMessagingProvenance resource for each message exchange the message ha been involved in
- MedCom FHIR Messages SHALL contain no more than two bundled MedComMessagingProvenance resource when acknowledging a message

![alt text](https://build.fhir.org/ig/hl7dk/dk-medcom-messaging/MedComMessagingProvenance.png "MedCom Messaging Provenance key concepts(Remote)")

[here](/assets/documents/Provenance.md)

## Reliable Messaging

[here](/assets/documents/Reliable_Messaging.md)

## Network Envelope

- MedCom FHIR Messages SHALL be enveloped in a VANS ENVELOPE
- MedCom FHIR Messages SHALL follow the metadataspecification outlined in
  - [Danish](/assets/documents/FHIRMessages_NetworkEnvelopes_DA.md)
  - [English](/assets/documents/FHIRMessages_NetworkEnvelopes_EN.md)

## Network Layer

## Test and Certification

All profiles MUST be validated with the FHIR validator

All profiles MUST be validated with TouchStone

## Release Notes

Updates in the latest release.

## Support or Contact

[MedCom](https://www.medcom.dk/) is responsible for this page.  
For any question regaring the standard, please contact <fhir@medcom.dk>

![alt text](https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/fhir-logo.png "HL7 FHIR")
