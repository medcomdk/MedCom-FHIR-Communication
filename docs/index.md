# Governance for MedCom FHIR®© Messaging (Work-in-progress)

<hr/>

## Table of Content

* [1. Introduction to Governance for MedCom FHIR®© Messaging](#1-introduction-to-governance-for-medcom-fhir-messaging)
* [2. Governance for Reliable Messaging in general](#2-governance-for-reliable-messaging-in-general)
* [3. Governance for the Network Layer](#3-governance-for-network-layer)
  * [3.1 Vansenvelope](#31-vansenvelope)
  * [3.2 Vansenvelope](#32-reliable-messaging-using-vansenvelope)
* [4. Governance for MedComFHIR Messaging](#4-governance-for-medcom-fhir-messaging)
  * [4.1 Basic Danish Messaging Assumptions](#41-basic-danish-messaging-assumptions-tbd)
  * [4.2 Message exchange patterns](#42-message-exchange-patterns)
  * [4.3 Reliable Messaging using MedCom FHIR Messaging](#43-reliable-messaging-using-medcom-fhir-messaging)
  * [4.7 Messaging Rules](#44-fhir-messaging-rules-google-translated)
  * [4.8 Acnowledgement Rules](#45-fhir-messaging-acnowledgement-rules-google-translated)
* [5. Governance for MedCom FHIR Messages](#5-governance-for-medcom-fhir-messages)

<!-- 
  * [1.2 Asynchronous messaging](#12-asynchronous-messaging)
  * [4.1 MedComMessagingMessage (Bundle)](#51-medcommessagingmessage-bundle)
  * [4.2 MedComMessagingMessageHeader](#52-medcommessagingmessageheader)
  * [4.3 MedComMessagingOrganization](#53-medcommessagingorganization)
  * [4.4 MedComMessagingProvenance](#54-medcommessagingprovenance)
  * [4.5 MustSupport](#55-mustsupport)
  * [4.6 Narrative Texts](#56-narrative-texts)
-->

---

[Governance Terms](/assets/documents/01-1-Governance_Terms.md)

---

## 1. Introduction to Governance for MedCom FHIR Messaging

On this page you can find information about how MedCom has profiled the [HL7 FHIR®© Messaging Framework](http://hl7.org/fhir/R4/messaging.html) to work in a Danish context.
Governance for MedCom HL7 FHIR®© Messaging describes the basic ruleset of how MedCom Messages shall be exchanged in the Danish Healthcare Messaging Network.
The Danish ruleset is based on both the ruleset for the Danish VANS Network, the Danish profiling of FHIR messaging and the general HL7 FHIR®© Communication Rules for FHIR Messaging.These “MedCom FHIR®© Messaging Governance rules” are intended to clarify the use of MedCom’s FHIR messages for the health and social area. Formerly these kind of rules for other MedCom Messaging paradigms were known as ”Syntax & Communication Rules”.

It is the intention that the “MedCom FHIR®© Messaging Governance rules” together with MedCom’s standards for the individual messages form the full and sufficient basis for implementing MedCom’s healthcare messages.The governance rules must thus be able to function as “chief judge”, where there is doubt about the practical application of MedCom’s FHIR messages.

The “Governance for MedCom FHIR®© Messaging” ensures a uniform use of MedCom’s FHIR messages to the health and social domains in Denmark.
In the following we follow a top-down approach by initially addressing shipping over the Network Layer and its ruleset, then the logistics for MedCom FHIR Messaging and lastly the basic ruleset of how to compose a MedCom FHIR message.

What you will find here is, how MedCom has profiled the HL7 FHIR®© Messaging Framework to work in a Danish context.

Governance for MedCom HL7 FHIR®© Messaging is the basic ruleset of how MedCom Messages must be exhanged in the Danish Healthcare Messaging Network.

The Danish ruleset is based on both the ruleset for the Danish VANS Network, the Danish profiling of FHIR messaging and the general HL7 FHIR®© Communication Rules for FHIR Messaging can be found on the <a href="http://hl7.org/fhir/R4/messaging.html" target="_blank">HL7 FHIR®© R4 Messaging Website</a>.

These "MedCom FHIR®© Messaging Governance rules" are intended to clarify the use of MedCom's FHIR messages for the health and social area. Formerly these kind of rules for other MedCom Messaging paradigms were known as 'Syntax & Communication Rules'

It is the intention that the governance rules together with MedCom's standards for the individual messages form the full and sufficient basis for implementing MedCom's healthcare messages.The governance rules must thus be able to function as “chief judge”, where there is doubt about the practical application of MedCom's FHIR messages.

The "Governance for MedCom FHIR®© Messaging" must ensure a uniform use of MedCom's FHIR messages to the health and social area domains in Denmark.

In the following we follow a top-down approach by addressing shipping over the Network Layer and its ruleset first, then the logistics for MedCom FHIR Messaging and last cover the basic ruleset of how to compose a MedCom FHIR message.

<!-- [Introduction details (Danish)](/assets/documents/01-Introduction.md)-->

<!-- [Generelle tekniske use cases](/assets/documents/Generelle-tekniske-use-cases-v1.0.0-b2.md) -->

### 1.1 What is a MedCom FHIR Message Standard

An implementer of a MedCom FHIR Message Standard **SHALL** be compliant with all the parts of the documentation laid out for the MedCom FHIR Message Standard and described here: [Dcumentation for the MedCom FHIR Message Standard](https://medcomdk.github.io/dk-medcom-messaging/#12-medcommessagingmessage-bundle)

### 1.2 Asynchronous Messaging

MedCom FHIR Messaging is based on Asynchronous Messaging.

In Asynchronous messaging, a Sending EcoSystem dispatches an unsolicited message to a Receiving EcoSystem possibly through several intermediate hubs, and besides from sending an possibly requested acknowledgement immediately as a response, the Receiving EcoSystem responds to the Sending EcoSystem separately. The Receiving EcoSystem may respond more than once to any given message.

## 2 Governance for Reliable Messaging in general

MedCom FHIR Messaging uses Reliable Messaging.

A key part of the Messaging Network is to provide funcionality for Reliable Messaging.

Sending and Receiving EcoSystems when acting in FHIR MEssaging scenarios **SHALL** support the Reliable Messaging scenarios outlined in the following section.

These scenarios are laid out as generic scenarios and later specified as how they will work out in a VANSEnvelope context and as how they will work out in a MedCom FHIR Messaging context.

| Links for Reliable Messaging|
|:---|
| [Reliable Messaging in general](/assets/documents/Reliable_Messaging-In-General.md) |

## 2.1 Generic ruleset governing the principles of Reliable Messaging

|Generic ruleset governing the principles of Reliable Messaging|
|:---|
| A Sending EcoSystem **SHALL** send a Message with a flag indicating that it expects an Acknowledgement on the Message|
| A Sending EcoSystem **SHALL** be able to handle an unacknowledged Message|
| A Sending EcoSystem **SHALL** resend the Message, when the expected Acknowledgement is not received within a timelimit of 15 minutes|
| A Sending EcoSystem **SHALL** change the MessageEnvelopeId and the MessageSentTime of a resend Message|
| A Sending EcoSystem **SHALL NOT** resend the Message more than 2 times, when the expected Acknowledgement is not received|
| A Receiving EcoSystem **SHALL** return an Acknowledgement on a received Message with a flag indicating that it expects an Acknowledgement on the Message|
| A Receiving EcoSystem **SHALL** be able to receive a Message as a duplicate|
| A Receiving EcoSystem **SHALL NOT** present the end-user for a duplicate of a Message|
| A Receiving EcoSystem **SHALL** change the MessageEnvelopeId and the MessageSentTime of a resend Acknowledgement|
| A Receiving EcoSystem **SHALL** return the same Acknowledgement content on a received Message as it returned on the first received copy of the Message|

<br>

A specific ruleset for respectively the MedCom FHIR Message and the VANSEnvelope will be explained later in this Governance.

| Links for specific ruleset of Reliable Messaging|
|:---|
|[2.3.1 Reliable Messaging using VANSEnvelope](#32-reliable-messaging-using-vansenvelope)|
|[3.3 Reliable Messaging using MedCom FHIR Messaging](#43-reliable-messaging-using-medcom-fhir-messaging)|

## 3. Governance for Network Layer

The Danish Healthcare Messaging Network is currently the VANS Network on which the overall shipment of a message is handled through Asynchronous Messaging.

To be able to communicate over the VANS Network, both senders and receivers **SHALL** have an GLN number issued by the SOR. [Link for SOR](https://sundhedsdatastyrelsen.dk/da/rammer-og-retningslinjer/organisationsregistrering)

To be able to communicate a specific MedCom FHIR messagetype both senders and receivers **SHALL** be registered in SOR with that messagetype and version.

The Sending EcoSystem **SHALL** validate the message before dispatching it. Validating a message **SHALL** include validating the correct use of the ValueSets and Coding Systems used in the message.

The Sending EcoSystem **SHALL** validate the message before dispatching it. Validating a message **SHALL** include validating the correct use of the ValueSets and Coding Systems used in the message.

### 3.1 VANSEnvelope

The VANSenvelope is developed to contain xml-based or other non-edifact messagetypes over the VANS Network

MedCom FHIR Messages **SHALL** be enveloped in a VANSenvelope whether they are shipped as "application/fhir+xml" or "application/fhir+json"

* The enveloping of MedCom FHIR Messages **SHALL** follow the VANS ENVELOPE specification outlined in
  * <a href="https://svn.medcom.dk/svn/releases/Standarder/Den%20gode%20VANSEnvelope/Dokumentation/Den%20gode%20VANSEnvelope.pdf" target="_blank">VANS ENVELOPE specification (Danish)</a>
* MedCom FHIR Messages **SHALL** follow the metadata specification outlined in
  * [Network Envelope (Danish)](/assets/documents/FHIRMessages_NetworkEnvelopes_DA.md)
  * [Network Envelope (English)](/assets/documents/FHIRMessages_NetworkEnvelopes_EN.md)

### 3.2 Reliable Messaging using VANSenvelope

VANSenvelope is developed to support Reliable Messaging.
VANSenvelope containing FHIR Messages **SHALL** make use of this Reliable Messaging functionality.

* The use of Reliable Messaging functionality when shipping MedCom FHIR Messages **SHALL** follow the VANS ENVELOPE specification outlined in
  * <a href="https://svn.medcom.dk/svn/releases/Standarder/Den%20gode%20VANSEnvelope/Dokumentation/Den%20gode%20VANSEnvelope.pdf" target="_blank">VANS ENVELOPE specification (Danish)</a>

[Tap here to see how to setup Reliable Messaging using VANSEnvelope](/assets/documents/Reliable_Messaging-VANSEnvelope.md)

## 4. Governance for MedCom FHIR Messaging

[Governance for MedCom FHIR Messaging](/assets/documents/04Governance4FHIR-Messaging.md)

<!-- 
This Governance for MedCom FHIR Messaging includes the corresponding OIOXML version of certain MedCom FHIR Messages, that are developed with the FHIR Message as the definer of the content of the OIOXML version.

FHIR Resources can be used in a traditional messaging context, much like HL7 v2.
Applications asserting conformance to this framework claim to be conformant to "FHIR messaging". 

In FHIR messaging, a "request message" or an "unsolicited message" is sent from a source application (Sending Application) to a destination application (Receiving Application) when an event happens. Events mostly correspond to things that happen in the real world.

The message consists of a Bundle identified by the type "message", with the first resource in the Bundle being a MessageHeader resource. The MessageHeader resource has a code - the message event - that identifies the nature of the message, and it also carries additional metadata. The other resources in the Bundle depend on the type of the message, eg. in which context a message is triggered.

The events supported in MedCom FHIR Messaging, along with the resources that are included in them, are defined in: [MedCom FHIR Messaging events](/assets/documents/MedCom-FHIR-Messaging-Events.md).

The destination application processes the message and returns an acknowledgement message and maybe one or more response messages, which too are a Bundle of resources identified by the type "message", with the first resource in each Bundle being a MessageHeader resource with a response section that reports the outcome of processing the message and any additional response resources required.

### 4.1 Basic Danish Messaging Assumptions [TBD]

This specification assumes that content will be delivered from one application to another by some delivery mechanism, and then one or more responses will be returned to the source application.

In Denmark this specification rules the exchange of messages through the Danish Messaging Network, currently known as VANS, and using the central organization register, SOR, for delivering the virtual adressing information.

The agreements around the content of the messages and the behavior of the two applications form the "contract" that describes the exchange. These contracts are exactly what MedCom delivers in the Danish Healthcare Domain and therefore MedCom adds regional and local agreements to the rules defined in the HL7 FHIR®© specification.

This specification ignores the existence of interface engines and message transfer agents that exist between the source and destination. Either they are transparent to the message/transaction content and irrelevant to this specification, or they are actively involved in manipulating the message content (in particular, the source and destination headers are often changed). If these middleware agents are modifying the message content, then they become responsible for honoring the contract that applies (including applicable profiles) in both directions.

### 4.2 Message Exchange Patterns

Each MedCom FHIR message has one or more response messages. There **SHALL** be at least one response message, an acknowledgement message, so that the sender can know, that the message was properly received.

Multiple response messages **SHALL NOT** be returned for messages of consequence, and **SHOULD** not be returned for notifications.

In principle, source applications **SHOULD** not wait for a response to a transaction before issuing a new transaction. However, in many cases, the messages in a given stream are dependent on each other, and must be sent and processed in order. In addition, some transfer methods may require sequential delivery of messages.

-->

### 4.3 Reliable Messaging using MedCom FHIR Messaging

FHIR Messaging is developed to support Reliable Messaging.
MedCom FHIR Messages **SHALL** make use of this Reliable Messaging functionality.

[Tap here to see how to set up Reliable Messaging using MedCom FHIR Messaging](/assets/documents/Reliable_Messaging-FHIR.md)

### 4.4 FHIR Messaging rules (Google translated)

[TBD]

| ID | Rule |
|:------| :-----|
| MR1.S | An acknowledgment **SHALL** always be requested on a FHIR message |
| MR2.S | A message **SHALL** be marked as sent and received when an AA acknowledgment has been received |
| MR3.S | A message **SHALL** be marked as failed when a negative AR acknowledgment has been received |
| MR4.S | A message **SHALL** be marked as failed when a negative AE acknowledgment has been received |
| MR5.R | A message **SHALL** not be resent more than 3 times upon receipt of an AE Acknowledgment |
| MR6.R | A message **SHALL** be re-sent more than 3 times in the event of failure to receive an Acknowledgment |
| MR7.R | A message that is resent **SHALL** always be updated with new timestamp=Bundle.timestamp and new envelope time=Bundle.id |
| MR8.R | A message is a duplicate if it contains the same MessageHeader.Id as a previously received message |

<!--
[Messaging rules (Danish)](/assets/documents/Rules_Messaging-DA.md)

[Messaging rules (English)](/assets/documents/Rules_Messaging-EN.md)
-->

### 4.5 FHIR Messaging Acnowledgement rules (Google translated)

[TBD]

| ID | Rules |
|:------| :-----|
| KR1.R | A FHIR message **SHALL** always be acknowledged |
| KR2.R | An acknowledgment message **SHALL** never be acknowledged |
| KR3.R | If no errors are found while receiving a message, a positive acknowledgment **SHALL** be made with AA |
| KR4.R | If a technical error occurs in the receiver's system while receiving a message, a negative acknowledgment **SHALL** be made with AE |
| KR5.R | If a message validates negatively against the standard's profiling, it **SHALL** be acknowledged negatively with AR |
| KR6.S | If an acknowledgment of a message is not received within 30 minutes, the original message **MAY** be marked for resending |

<!--
[Acnowledgement rules (Danish)](/assets/documents/Rules_Acknowledgement-DA.md)

[Acnowledgement rules (English)](/assets/documents/Rules_Acknowledgement-EN.md)
-->

## 5. Governance for MedCom FHIR Messages

<!-- 
Below you see the basic MedCom FHIR Messaging Model.

As shown in the diagram below there are 4 MedCom profiled FHIR resources involved in a MedCom FHIR Message:

- A MedComMessagingMessage is a Bundle resource of type "message"
- The MedComMessagingMessage's first resource is a MedComMessagingMesssageHeader, which is a MesssageHeader resource
- The MedComMessagingMesssageHeader points to at least two organizations for the MedComMessagingMessage:
  - a source organization called a MedComMessagingOrganization, which is an Organization resource
  - a destination organization also a MedComMessagingOrganization, which too is an Organization resource
- The MedComMessagingMessage's MedComMessagingProvennance, which is a Provennance resource

<br>

<figure style="margin-left: 0px; margin-right: 0px; width: 100%;">
<a href="https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/MessagingModel.png" target="blank"> <img src="https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/MessagingModel.png" alt="The basic MedCom Messaging Model"  style="width:100%" id="Fig2" style="align-left"></a>
<figcaption text-align="left"><b>Figure 2: The basic MedCom Messaging Model</b></figcaption>
</figure>
<br>

-->

### 5.1 MedComMessagingMessage (Bundle)

An inherited instance profile of MedComMessagingMessage **SHALL** follow the generic concept of the MedComMessagingMessage as outlined here:
[MedComMessagingMessage (Bundle) in MedCom Message](https://medcomdk.github.io/dk-medcom-messaging/#13-medcommessagingmessage-bundle)

<!-- 
MedComMessagingMessage is a Bundle resource of type "message", which is a container for a collection of other resources.

<br>

| Links for MedComMessingMessage|
|:---|
| <a href="https://build.fhir.org/ig/medcomdk/dk-medcom-messaging//StructureDefinition-medcom-messaging-message.html" target="_blank"> Detailed specification for MedComMessingMessage in MedComMessingMessage IG</a> |
| <a href="https://medcomdk.github.io/dk-medcom-messaging/" target="_blank">Detailed page for MedCom Messaging</a> |
| <a href="http://hl7.org/fhir/R4/Bundle.html" target="_blank">Detailed specification for Bundle in FHIR R4</a> |

<br>

## 4.1.1 Scope and Usage

One common operation performed with resources is to gather a collection of resources into a single instance with containing context. In FHIR this is referred to as "bundling" the resources together. These resource bundles are useful for a variety of different reasons, including sending a set of resources as part of a message exchange (see Messaging)
-->

### 5.1.2 MedComMessingMessage Rules

| MedComMessingMessage Rules|
|:---|
| A MedCom FHIR Message **SHALL** be a Bundle resource of type "message" |
| A MedCom FHIR Message **SHALL** contain at least one bundled MedComMessagingHeader resource |
| The MedComMessagingHeader resource **SHALL** be the first resource in a MedCom Message Bundle |
| A MedCom FHIR Message **SHALL** contain at least two bundled MedComMessagingOrganization resources |
| One of the two bundled MedComMessagingOrganization resources **SHALL** represent the Sender Organization pointed to by the MedComMessagingHeader.sender element |
| One of the two bundled MedComMessagingOrganization resources **SHALL** represent the Receiver Organization pointed to by the MedComMessagingHeader.destination:primary sliced element |
| A MedCom FHIR Message **MAY** contain more bundled MedComMessagingOrganization resources |
| The MedComMessagingHeader resource **MAY** include a list of carbon-copy receiver organizations pointed to by the MedComMessagingHeader.destination:cc sliced element(s) |
| If there exists one or more destination:cc elements, these **SHALL** be represented as bundled MedComMessagingOrganization resource(s) each one of the carbon-copy receiver Organizations pointed to by the MedComMessagingHeader.destination:cc sliced element |
| A MedCom FHIR Message **SHALL** contain at least one bundled MedComCorePatient resource |
| A MedCom FHIR Message **SHALL** contain at least one bundled MedComMessagingProvenance resource |
| A MedCom FHIR Message **SHALL** contain one bundled focused resource pointed to by the MedComMessagingHeader |
| The MedComMessagingHeader resource **SHALL** contain a Narrative text |
| A MedCom FHIR Message **SHALL** be validated before disptching of the message |
| A MedCom FHIR Message **SHALL** be validated on reception of the message in the Receiving Apllication|

### 5.2 MedComMessagingMessageHeader

[TBD]

An inherited instance profile of MedComMessagingMessage **SHALL** follow the generic concept of the MedComMessagingMessage as outlined here:
[MedComMessagingMessage (Bundle) in MedCom Message](https://medcomdk.github.io/dk-medcom-messaging/#13-medcommessagingmessage-bundle)

<!-- 
<figure style="margin-left: 0px; margin-right: 0px; width: 100%;">
<a href="https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/MedComMessageHeader.png" target="_blank"> <img src="https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/MedComMessageHeader.png" alt="MedComMessageHeader"  style="width:100%" id="Fig1" style="align-left"></a>
<figcaption text-align="left"><b>Figure 3: MedComMessageHeader</b></figcaption>
</figure>

<br>

| Links for MedComMessagingMessageHeader|
|:---|
| <a href="https://build.fhir.org/ig/medcomdk/dk-medcom-messaging//StructureDefinition-medcom-messaging-messageHeader.html" target="_blank"> Detailed specification for MedComMessageHeader in MedComMessingMessage IG</a> |
| [MedComMessageHeader](/assets/documents/MedComMessagingMessageHeader.md) |
| <a href="http://hl7.org/fhir/R4/MessageHeader.html" target="_blank">Detailed specification for MessageHeader in FHIR R4</a> |

<br>

### 4.2.1 Scope and Usage
-->

#### 5.2.1 MedComMessagingMessageHeader Rules

The MedComMessageHeader profile is a resource that **shall** be used in all MedCom FHIR Messages. A MedComMessagingMessageHeader **shall** include a sender and receiver and it **may** include a carbon-copy receiver, however this is depended on type of standard. Each MedComMessagingMessageHeader **shall** include a globally unique id, which **shall** be used to reference the message in the message history from the MedComMessagingProvenance profile.

The element event **shall** be defined in accordance with the type of standard the message concerns e.g., HospitalNotification and CareCommunication. Due to the different requirements for each standard, it **shall** be expected that the MedComMessagingMessageHeader is inherited in each standard.

| MedComMessageHeader Rules|
|:---|
| The MedComMessagingHeader resource **SHALL** be the first resource in a MedCom Message Bundle |
| The MedComMessagingHeader resource **SHALL** contain an event of the MedCom Message (eg. the type of the message) |
| The MedComMessagingHeader resource **SHALL** contain an MedComMessagingHeader.id of the MedCom Message (eg. the letter.id of the message) |
| One of the two bundled MedComMessagingOrganization resources **SHALL** represent the Sender Organization pointed to by the MedComMessagingHeader.sender element |
| One of the two bundled MedComMessagingOrganization resources **SHALL** represent the Receiver Organization pointed to by the MedComMessagingHeader.destination:primary sliced element |
| The MedComMessagingHeader resource **MAY** include a list of carbon-copy receiver organizations pointed to by the MedComMessagingHeader.destination:cc sliced element(s) |
| MedCom FHIR Messages **SHALL** contain one bundled focused resource pointed to by the MedComMessagingHeader pointed to by the MedComMessagingHeader.focus element |

#### 5.2.2 Identifiers and Timestamps

[TBD]

[Identifiers](/assets/documents/MessageHeader_Identifiers_Timestamps.md)

### 5.3 MedComMessagingOrganization

[TBD]

<br>

| Links for MedComMessagingOrganization|
|:---|
| <a href="https://build.fhir.org/ig/medcomdk/dk-medcom-messaging/StructureDefinition-medcom-messaging-organization.html" target="_blank"> Detailed specification for MedComMessagingOrganization in MedComMessingMessage IG</a> |
| <a href="http://hl7.org/fhir/R4/Organization.html" target="_blank">Detailed specification for Organization in FHIR R4</a> |

<br>

#### 5.3.1 Scope and Usage

This profile describes the Organization resource that **shall** be used in all MedCom FHIR Messages. MedComMessagingOrganization inherits from MedComCoreOrganization as it **shall** include both a SOR and EAN/GLN identifier. MedComMessagingOrganization **shall** be used to describe the sender and receiver organizations of all MedCom FHIR Messages.

<br>

#### 5.3.2 MedComMessagingOrganization Rules

[TBD]

### 5.4 MedComMessagingProvenance

Provenance of a resource is a record that describes entities and processes involved in producing and delivering or otherwise influencing that resource. Provenance provides a critical foundation for assessing authenticity, enabling trust, and allowing reproducibility. Provenance assertions are a form of contextual metadata and can themselves become important records with their own provenance. Provenance statement indicates clinical significance in terms of confidence in authenticity, reliability, and trustworthiness, integrity, and stage in lifecycle (e.g. Document Completion - has the artifact been legally authenticated), all of which may impact security, privacy, and trust policies.

<br>

| Links for MedComMessagingProvenance|
|:---|
| <a href="https://build.fhir.org/ig/medcomdk/dk-medcom-messaging/StructureDefinition-medcom-messaging-provenance.html" target="_blank"> Detailed specification for MedComMessagingProvenance in MedComMessingMessage IG</a> |
| [MedComs use of Provenance](/assets/documents/MedComMessagingProvenance.md) |
| <a href="http://hl7.org/fhir/R4/Provenance.html" target="_blank">Detailed specification for Provenance in FHIR R4</a> |

<br>

#### 5.4.1 Scope and Usage

The MedComMessagingProvenance resource tracks information about the activity that created, revised, deleted, or signed a version of a resource, describing the entities and agents involved. This information can be used to form assessments about its quality, reliability, trustworthiness, or to provide pointers for where to go to further investigate the origins of the resource and the information in it.

Provenance resources are a record-keeping assertion that gathers information about the context in which the information in a resource was obtained. Provenance resources are prepared by the application that initiates the create/update etc. of the resource. An AuditEvent resource contains overlapping information, but is created as events occur, to track and audit the events. AuditEvent resources are often (though not exclusively) created by the application responding to the read/query/create/update/etc. event.

<br>
<figure style="margin-left: 0px; margin-right: 0px; width: 100%;">
<a href="https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/MedComMessagingProvenance.png" target="_blank"> <img src="https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/MedComMessagingProvenance.png" alt="MedComMessageHeader"  style="width:100%" id="Fig1" style="align-left"></a>
<figcaption text-align="left"><b>Figure 4: MedComMessagingProvenance</b></figcaption>
</figure>
<br>

#### 5.4.2 Rules

[TBD]

* MedCom FHIR Messages **SHALL** contain at least one bundled MedComMessagingProvenance resource
* MedCom FHIR Messages **SHALL** contain one bundled MedComMessagingProvenance resource for each message exchange the message has been involved in
* MedCom FHIR Messages **SHALL** contain no more than two bundled MedComMessagingProvenance resource when acknowledging a message

### 5.5 MustSupport

Labeling an element MustSupport means that implementations that produce or consume resources SHALL provide "support" for the element in some meaningful way. Because the base FHIR specification is intended to be independent of any particular implementation context, no elements are flagged as mustSupport=true as part of the base specification. This flag is intended for use in profiles that have a defined implementation context.

For this reason, the specification itself never labels any elements as MustSupport. This is done in StructureDefinitions, where the profile labels an element as mustSupport=true. When a profile does this, it SHALL also make clear exactly what kind of "support" is required, as this could involve expectations around what a system must store, display, allow data capture of, include in decision logic, pass on to other data consumers, etc.

Note that an element that has the property IsModifier is not necessarily a "key" element (e.g. one of the important elements to make use of the resource), nor is it automatically mustSupport - however both of these things are more likely to be true for IsModifier elements than for other elements.

<br>

| Links for MustSupport|
|:---|
| <a href="http://hl7.org/fhir/R4/MustSupport.html" target="_blank">Detailed specification for MustSupport in FHIR R4</a> |

<br>

#### 5.5.1 Scope and Usage

In MedCom FHIR Messaging MustSupport denotes the MedCom FHIR Message. While FHIR resources can contain a lot of different elements, a MedCom FHIR Message is defined to be exactly what is outlined by the MustSupport flag in the IG

#### 5.5.2 Rules

In MedCom FHIR Messaging MustSupport requires that a system

* **SHALL** store,
* **SHALL** display
* **SHOULD** include in decision logic
* **MAY** pass on to other data consumers

### 5.6 Narrative Texts

A Narrative Text is a human-readable narrative that contains a summary of the resource and can be used to represent the content of the resource to a human. The narrative **SHALL** encode all the structured data pointed out by the ∑-symbol and it is required to contain sufficient detail to make it "clinically safe" for a human to just read the narrative.
Contained resources do not have narrative, but their content **SHALL** be represented in the ressource container.

Narratives contains two sub elements, status and div.

#### 5.6.1 The status element

[TBD]
The code system [narrative status](http://hl7.org/fhir/narrative-status) defines the codes for the status element.

In MedCom FHIR Messages The code **SHALL** always be: "additional" meaning that the it is covering the code: extension and allowing for more human readable text in the div element than is produced by: generated and extension.

A narrative in MedCom FHIR Messages **SHALL NEVER** be of code: empty.

#### 5.6.2 The div element

The contents of the div element are XHTML fragments that **SHALL** contain only the basic HTML formatting elements described in chapters 7-11 (except section 4 of chapter 9) and 15 of the HTML 4.0 standard, '<a>' elements (either name or href), images and internally contained style attributes.

The XHTML content **SHALL NOT** contain a head, a body element, external stylesheet references, deprecated elements, scripts, forms, base/link/xlink, frames, iframes, objects or event related attributes (e.g. onClick). This is to ensure that the content of the narrative is contained within the resource and that there is no active content. Such content would introduce security issues and potentially safety issues with regard to extracting text from the XHTML. Note that even with these restrictions, there are still several important security risks associated with displaying the narrative.

The div element **SHALL** have some non-whitespace content (text or an image).

#### 5.6.3 Scope and Usage

[TBD]
The narrative element is a human-readable summary of the resource (essential clinical and business information)

#### 5.6.4 General Narrative Text Rules

* All resources in a MedComMessingMessage **SHALL** contain a Narrative Text defined by the [resource].Text element
* The Narrative Text **SHALL** have a status with value "extensions". Extensions means that the contents of the narrative are entirely generated from the core elements in the content and some of the content is generated from extensions.
* The narrative **SHALL** reflect the impact of all modifier extensions.

[Narrative Text description in FHIR R4](http://hl7.org/fhir/R4/narrative.html#Narrative)

[NarrativeStatus in FHIR R4](http://hl7.org/fhir/R4/codesystem-narrative-status.html#4.3.14.424.2)

[Styling the XHTML in FHIR R4](http://hl7.org/fhir/R4/narrative.html#css)

### 5.9 Governance for displaying MedCom FHIR Messaging

All elements marked as MustSupport **SHALL** be presented or easily accessed on the display of the reader of a received message.

The message as a whole coherent object **SHALL** be present for easy access for the reader.

The receiving application **SHALL** be able to show only relevant information for the different receiver roles in the receiving organization, eg. only persons in clinical roles **SHALL** be able to read clinical content

### 6.0 Governance for Terminiology

The term Terminology is in this governance a term covering all kins of terminology, classifications, enumerations and qualifiers.

All elements of a MedCom FHIR Message **SHALL** be compliant with the terminologies that are pointed out by these elements.

All Terminologies that are not implicitly present in the specification of an element are present in the Terminology IG and this Terminology IG **SHALL** be

## x. Governance for Test and Certification (To be moved)

All message solutions developed on the basis of MedCom FHIR Messing profiles **SHALL** be validated with the FHIR validator

All message solutions developed on the basis of MedCom FHIR Messing profiles **SHALL** be validated with MedComs TouchStone Certification Suites

_**Insert requirements from the test and certification process here**_

## y. Governance for Release Notes (To be moved)

All changes in the MedCom FHIR Specifications **SHALL** be described in a release note following that specific version of the specification.

_**Insert requirements from Release Notes**_
