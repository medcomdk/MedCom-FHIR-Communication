# Communication Rules for MedCom HL7 FHIR®© Messaging

Here you will find the information you need to get started with MedCom's FHIR®© standards.

![alt text](https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/fhir-logo.png "HL7 FHIR")

## Indledning

[here](/assets/documents/01-Indledning.md)

<table border=2>
    <tr border=2>
        <td><b>Name in English</b></td>
        <td><b>Name in Danish</b></td>
    </tr>
    <tr border=2>
        <td>Core Profiles</td>
        <td>Kerneprofiler</td>
    </tr>
    <tr border=2>
        <td>Messaging</td>
        <td>Medddelser</td>
    </tr>
    <tr border=2>
        <td>Acknowledgement</td>
        <td>Kvittering</td>
    </tr>
</table>

## Content
[FHIR Messaging](FHIR Messaging)
- [Basic Messaging Assumptions](Basic Messaging Assumptions)

## FHIR Messaging

FHIR Resources can be used in a traditional messaging context, much like HL7 v2  (see detailed comparison). Applications asserting conformance to this framework claim to be conformant to "FHIR messaging".

In FHIR messaging, a "request message" or an "unsolicidated message" is sent from a source application to a destination application when an event happens. Events mostly correspond to things that happen in the real world. The message consists of a Bundle identified by the type "message", with the first resource in the bundle being a MessageHeader resource. The MessageHeader resource has a code - the message event - that identifies the nature of the request message, and it also carries additional metadata. The other resources in the bundle depend on the type of the message.

The events supported in FHIR, along with the resources that are included in them, are defined below.

The destination application processes the message and returns an acknowledgment message and one or more response messages, which are also a bundle of resources identified by the type "message", with the first resource in each bundle being a MessageHeader resource with a response section that reports the outcome of processing the message and any additional response resources required.

### Basic Messaging Assumptions

This specification assumes that content will be delivered from one application to another by some delivery mechanism, and then one or more responses will be returned to the source application. The exact mechanism of transfer is irrelevant to this specification, but may include file transfer, HTTP based transfer, MLLP (HL7 minimal lower layer protocol), MQ series messaging or anything else. The only requirement for the transfer layer is that requests are sent to a known location and responses are returned to the source of the request. This specification considers the source and destination applications as logical entities, and the mapping from logical source and destination to implementation specific addresses is outside the scope of this specification, though this specification does provide a direct delivery mechanism below.

The agreements around the content of the messages and the behavior of the two applications form the "contract" that describes the exchange. The contract will add regional and local agreements to the rules defined in this specification.

This specification ignores the existence of interface engines and message transfer agents that exist between the source and destination. Either they are transparent to the message/transaction content and irrelevant to this specification, or they are actively involved in manipulating the message content (in particular, the source and destination headers are often changed). If these middleware agents are modifying the message content, then they become responsible for honoring the contract that applies (including applicable profiles) in both directions.

## Basic elements of FHIR Messages

### MessageHeader

[here](/assets/documents/MessageHeader_Identifiers.md)

### Timestamps

[here](/assets/documents/MessageHeader_Timestamps.md)

### Messaging rules

[Danish here](/assets/documents/Rules_Messaging-DA.md)
[English here](/assets/documents/Rules_Messaging-EN.md)

### Acnowledgment rules

[Danish here](/assets/documents/Rules_Acknowledgment-DA.md)
[English here](/assets/documents/Rules_Acknowledgment-EN.md)

## Reliable Messaging

[here](/assets/documents/Reliable_Messaging.md)

## MustSupport

[here](/assets/documents/MustSupport.md)

## Information about Network Envelopes and the Transportation Layer

Danish [here](/assets/documents/MedComs_FHIR-meddelelser_og_forsendelseskuvert.md)

English [here](/assets/documents/MedComFHIRMessagesAndNetworkEnvelopes.md)

## Test and Certification

All profiles MUST be validated with the FHIR validator

All profiles MUST be validated with TouchStone

## Release Notes

Updates in the latest release.

## Support or Contact

[MedCom](https://www.medcom.dk/) is responsible for this page.  
For any question regaring the standard, please contact <fhir@medcom.dk>
