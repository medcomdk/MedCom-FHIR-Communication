# Governance for MedCom FHIR Message Exchange

**Table of content**

* [1 Basic Danish Messaging Assumptions](#1-basic-danish-messaging-assumptions)
* [2 Message exchange patterns](#2-message-exchange-patterns)
* [3 Reliable Messaging using MedCom FHIR Messaging](#3-reliable-messaging-using-medcom-fhir-messaging)
* [4 Handling sending scenarios](#4-handling-sending-scenarios)
    * [4.1 Scenario #1 Sending to a primary receiver](#41-scenario-1-sending-to-a-primary-receiver)
    * [4.2 Scenario #2 Sending copies of a MedComMessagingMessage](#42-scenario-2-sending-copies-of-a-medcommessagingmessage)
    * [4.3 Scenario #3 Sending to a primary receiver with an already known copyreciver](#43-scenario-3-sending-to-a-primary-receiver-with-an-already-known-copyreciver)
    * [4.3.1 Scenario #3a Sending to a copyreceiver while also sending to a Primary receiver](#431-scenario-3a-sending-to-a-copyreceiver-while-also-sending-to-a-primary-receiver)
    * [4.4 Scenario #4 Forwarding a message](#44-scenario-4-forwarding-a-message)
* [5 Handling receiving scenarios](#5-handling-receiving-scenarios)
* [6 MedCom FHIR Messaging rules](#6-fhir-messaging-rules)
* [7 MedCom FHIR Messaging Acnowledgement rules](#7-fhir-messaging-acnowledgement-rules)

This Governance for MedCom FHIR Messaging includes the corresponding OIOXML version of certain MedCom FHIR Messages, that are developed with the FHIR Message as the definer of the content of the OIOXML version.

FHIR Resources can be used in a traditional messaging context, much like HL7 v2.
<!-- Applications asserting conformance to this framework claim to be conformant to "FHIR messaging". -->

In FHIR messaging, a "request message" or an "unsolicited message" is sent from a source application (Sending System) to a destination application (Receiving System) when an event happens. Events mostly correspond to things that happen in the real world.

The message consists of a Bundle identified by the type "message", with the first resource in the Bundle being a MessageHeader resource. The MessageHeader resource has a code - the message event - that identifies the nature of the message, and it also carries additional metadata. The other resources in the Bundle depend on the type of the message, eg. in which context a message is triggered.

The events supported in MedCom FHIR Messaging, along with the resources that are included in them, are defined in: [Click here to read tne MedCom FHIR Messaging events](MedCom-FHIR-Messaging-Events.md).

The destination application processes the message and returns an acknowledgement message and maybe one or more response messages, which too are a Bundle of resources identified by the type "message", with the first resource in each Bundle being a MessageHeader resource with a response section that reports the outcome of processing the message and any additional response resources required.

## 1 Basic Danish Messaging Assumptions

This specification assumes that content will be delivered from one application to another by some delivery mechanism, and then one or more responses will be returned to the source application.

In Denmark this specification rules the exchange of messages through the Danish Messaging Network, currently known as VANS, and using the central organization register, SOR, for delivering the virtual adressing information.

The agreements around the content of the messages and the behavior of the two applications form the "contract" that describes the exchange. These contracts are exactly what MedCom delivers in the Danish Healthcare Domain and therefore MedCom adds regional and local agreements to the rules defined in the HL7 FHIR®© specification.
toThis specification ignores the existence of interface engines and message transfer agents that exist between the source and destination. Either they are transparent to the message/transaction content and irrelevant to this specification, or they are actively involved in manipulating the message content (in particular, the source and destination headers are often changed). If these middleware agents are modifying the message content, then they become responsible for honoring the contract that applies (including applicable profiles) in both directions.

## 2 Message Exchange Patterns

Each MedCom FHIR message has one or more response messages. There **SHALL** be at least one response message, an acknowledgement message, so that the sender can know, that the message was properly received.

Multiple response messages **SHALL NOT** be returned for messages of consequence, and **SHOULD** not be returned for notifications.

In principle, source applications **SHOULD** not wait for a response to a transaction before issuing a new transaction. However, in many cases, the messages in a given stream are dependent on each other, and must be sent and processed in order. In addition, some transfer methods may require sequential delivery of messages.

## 3 Reliable Messaging using MedCom FHIR Messaging

FHIR Messaging is developed to support Reliable Messaging.
MedCom FHIR Messages **SHALL** make use of this Reliable Messaging functionality.

[Click here to see how to set up Reliable Messaging using MedCom FHIR Messaging](043_Reliable_Messaging-FHIR.md)

## 4 Handling sending scenarios

### 4.1 Scenario #1 Sending to a primary receiver

When sending to a primary receiver the Receiving Organization **SHALL** be pointed out/referenced by destination:primary/receiver in MedComMessagingMessageHeader.

Accordingly a MedComMessagingProvenance instance **SHALL** be populated with an activitycode in this enumeration: new-message, reply-message, retract-message, modified-message.

### 4.2 Scenario #2 Sending copies of a MedComMessagingMessage

A CarbonCopy-message is a MedComMessagingMessage sent to a copy receiver of the exact same MedComMessagingMessage transaction dispatched to a primary receiver.

A Forward-message is a MedComMessagingMessage sent to a copy receiver of a MedComMessagingMessage at a different time compared with the original MedComMessagingMessage transaction. A Forward-message is a MedComMessagingMessage that might differ in content with the original MedComMessagingMessage.

When sending a copy of an original MedComMessagingMessage, either exact copy (CC) or partially copy (fwd), the sending application **SHALL** make a copy of the original MedComMessagingMessage and it **SHALL** send the copy as a new MedComMessagingMessage.

That means that the requirements of a Bundle and MedComMessagingMessageHeader applies to the new MedComMessagingMessage and that a new MedComMessagingProvenance **SHALL** be made reflecting the kind of copy message that is sent and added to the MedComMessagingProvenance stack.

### 4.3 Scenario #3 Sending to a primary receiver with an already known copyreciver

When sending to a primary receiver the Receiving Organization **SHALL** be pointed out/referenced by destination:primary/receiver in MedComMessagingMessageHeader.

When also sending to a copyreciver the Receiving Organization representing this **SHALL** be pointed out/referenced by destination:cc/receiver in MedComMessagingMessageHeader.

Both elements **SHALL** be represented in both MedComMessagingMessages, so that the receivers of a MedComMessagingMessage will know who was the primary receiver and who was the copy receiver(s).

#### 4.3.1 Scenario #3a Sending to a copyreceiver while also sending to a Primary receiver

A MedComMessagingMessage to a copyreceiver is as the name says a carbon copy of the original MedComMessagingMessage.

The MedComMessagingMessage that is sent to a ccreceiver **SHALL** be an exact copy of the original MedComMessagingMessage sent to the primary receiver, except for the unique ids in Bundle and MedComMessagingMessageHeader and the addition of a MedComMessagingProvenance instance.

Sending to a copyreceiver is handled on different levels:

* MedComMessagingMessage: As the message is regarded as a new message, the Bundle.id **SHALL** be a new unique id different form the original MedComMessagingMessage and Bundle.Timestamp **SHALL** reflect the time of creation of this Bundle.
* MedComMessagingMessage: The MedComMessagingMessageHeader.id **SHALL** be changed.
* MedComMessagingMessage: Other MedComMessagingMessageHeader **SHALL NOT** be changed.
* MedComMessagingMessage: The MedComMessagingProvenance **SHALL** reflect the scenario by adding a MedComMessagingMessage to the stack of MedComMessagingProvenances with a copyreceiver activitycode.
* MedComMessagingMessage: The MedComMessagingProvenance's Provenance.occurredDateTime og Provenance.recorded **SHALL** reflect the sending time of the message.
* MedComMessagingMessage: Other entry.ressources **SHALL NOT** be changed.
* VANSenvelope: The VANSEnvelope **SHALL** be created with the copyreceiver's GLN as the receiving EAN.

#### 4.4 Scenario #4 Forwarding a message

A forwarded MedComMessagingMessage is a new MedComMessagingMessage to a new receiver, that was not present in the construction and dispatching of the original MedComMessagingMessage.

The MedComMessagingMessage that is sent to a forwardreceiver **MAY** be an exact copy of the original MedComMessagingMessage sent to the primary receiver, except for the unique ids in Bundle and MedComMessagingMessageHeader and the addition of a MedComMessagingProvenance instance.

The forwarded MedComMessagingMessage **SHALL** include most of the original content of the original MedComMessagingMessage.

The forwarded MedComMessagingMessage **MAY** add minor adjustments and minor new content.

Forwarding is handled on different levels

* MedComMessagingMessage: As the message is regarded as a new message, the Bundle.id **SHALL** be a new unique id different form the original MedComMessagingMessage and Bundle.Timestamp **SHALL** reflect the time of creation of this Bundle.
* MedComMessagingMessage: The MedComMessagingMessageHeader.id **SHALL** be changed.
* MedComMessagingMessage: Other MedComMessagingMessageHeader **SHALL NOT** be changed.
* MedComMessagingMessage: The MedComMessagingProvenance **SHALL** reflect the scenario by adding a MedComMessagingMessage to the stack of MedComMessagingProvenances with a forward activitycode.
* MedComMessagingMessage: The MedComMessagingProvenance's Provenance.occurredDateTime og Provenance.recorded **SHALL** reflect the sending time of the message.
* MedComMessagingMessage: Other entry.ressources **SHALL NOT** be changed.
* VANSenvelope: The VANSEnvelope **SHALL** be created with the forwardreceiver's GLN as the receiving EAN.


## 5 Handling receiving scenarios
There exists two types of receiver of the MedComMessagingMessage, respectively a Primary Receiver or a Copy Receiver. The information about what type of reciver the message is received by **SHALL** be defined in provenance. Both Primary and Copy receiver of the MedComMessage **SHALL** generate and send an MedCom Acknowledgement.

<!-- 
A Receiving Ecosystem **SHALL** be able to handle that it is either a Primary Receiver or a Copy Reciver.
As the information about what kind of MedComMessagingMessage that is received
That means that the Receiving Ecosystem **SHALL** be ????? -->

## 6 FHIR Messaging rules

| ID | Rule |
|:------| :-----|
| MR1.S | A MedCom FHIR Acknowledgement **SHALL** always be requested on a MedCom FHIR Message |
| MR2.S | A MedCom FHIR Message **SHALL** be marked as sent and received when an MedCom FHIR AA Acknowledgement has been received |
| MR3.S | A MedCom FHIR Message **SHALL** be marked as failed when a negative MedCom FHIR AR Acknowledgement has been received |
| MR4.S | A MedCom FHIR Message **SHALL** be marked as failed when a negative MedCom FHIR AE Acknowledgement has been received |
| MR5.R | A MedCom FHIR Message **SHALL** not be resent more than 3 times upon receipt of an MedCom FHIR AE Acknowledgement |
| MR6.R | A MedCom FHIR Message **SHALL NOT** be re-sent more than 3 times in the event of failure to receive an MedCom FHIR AE Acknowledgement |
| MR7.R | A MedCom FHIR Message that is resent **SHALL** always be updated with new timestamp=Provenance.timestamps and new envelopeid=Bundle.id |
| MR8.R | A MedCom FHIR Message is a duplicate if it contains the same MessageHeader.Id as a previously received MedCom FHIR Message |

<!-- [Danish: Meddelelsesregler](Rules_Messaging-DA.md) -->

<!-- [Messaging rules (English)](Rules_Messaging-EN.md) -->

## 7 FHIR Messaging Acnowledgement rules

| ID | Rules |
|:------| :-----|
| KR1.R | A FHIR message **SHALL** always be acknowledged |
| KR2.R | An Acknowledgement message **SHALL** never be acknowledged |
| KR3.R | If no errors are found while receiving a message, a positive Acknowledgement **SHALL** be made with AA |
| KR4.R | If a technical error occurs in the receiver's system while receiving a message, a negative Acknowledgement **SHALL** be made with AR |
| KR5.R | If a technical error from KR4.R is resolved and the message can be loaded Acknowledgement **SHALL**  be made with AA |
| KR6.R | If a message validates negatively against the standard's profiling, it **SHALL** be acknowledged negatively with AE |
| KR7.S | If an Acknowledgement of a message is not received within 30 minutes, the original message **MAY** be marked for resending |

<!-- [Danish: Kvitteringsregler](Rules_Acknowledgement-DA.md) -->

<!-- [Acnowledgement rules (English)](Rules_Acknowledgement-EN.md) -->
