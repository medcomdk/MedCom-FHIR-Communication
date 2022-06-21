<!-- # Governance for MedCom FHIR®© Messaging -->

- [Network Layer](#network-layer)
  - [VANSEnvelope](#vansenvelope)
  - [Reliable Messaging](#reliable-messaging)
    - [Reliable Messaging using VANSEnvelope](#reliable-messaging-using-vansenvelope)
- [MedComFHIR Messaging](#medcom-fhir-messaging)
- [MedCom FHIR Messages](#medcom-fhir-messages)
- [Test and Certification](#test-and-certification)

<!--
|                                                 ||                                              ||                                                                                |
|:---|:---|:---|:---|:---|
|[Network Layer](#network-layer)                  ||[VANSEnvelope](#vansenvelope)                 ||[Reliable Messaging using VANSEnvelope](#reliable-messaging-using-vansenvelope) |
|[MedComFHIR Messaging](#medcom-fhir-messaging)   ||[MedCom FHIR Messages](#medcom-fhir-messages) ||                                                                                |
|[Test and Certification](#test-and-certification)||                                              ||                                                                                |
-->

---

## Introduction to Governance for MedCom FHIR®© Messaging

What you will find here is, how MedCom has profiled the HL7 FHIR Messaging Framework to work in a Danish context.

Governance for MedCom HL7 FHIR®© Messaging is the basic ruleset of how MedCom Messages must be exhanged in the Danish Healthcare Messaging Network.

The Danish ruleset is based on both the ruleset for the Danish VANS Network, the Danish profiling of FHIR messaging and the general HL7 FHIR Communication Rules for FHIR Messaging can be found on the [HL7 FHIR R4 Messaging Website](http://hl7.org/fhir/R4/messaging.html).

These "FHIR Governance rules" are intended to clarify the use of MedCom's FHIR messages for the health and social area. Formerly these kind of rules for other MedCom Messaging paradigms were known as 'Syntax & Communication Rules'

It is the intention that the governance rules together with MedCom's standards for the individual messages form the full and sufficient basis for implementing MedCom's healthcare messages.

The governance rules must thus be able to function as “chief judge”, where there is doubt about the practical application of MedCom's FHIR messages.

The "Governance for MedCom FHIR®© Messaging" must ensure a uniform use of MedCom's FHIR messages to the health and social area domains in Denmark.

In the following we follow a top-down approach by addressing shipping over the Network Layer and its ruleset first, then the logistics for MedCom FHIR Messaging and last cover the basic ruleset of how to compose a MedCom FHIR message.

<!-- [Introduction details (Danish)](/assets/documents/01-Introduction.md)-->

<!-- [Generelle tekniske use cases](/assets/documents/Generelle-tekniske-use-cases-v1.0.0-b2.md) -->

---

| Terms |||
|:------||:-----|
| EAN   | Location Number issued by th GS1 organization through its partners all over the world - in Denmark SDS ( also known as GLN, Location number) |
| SDS  || Sundhedsdatastyrelsen (The Danish Health Data Authority) |
| SOR   | Sundhedsvæsenets Organisations Register (Healthcare Organization Register in Denmark ) |
| VANS  || VANS is an abbreviation of Value Added Network Services, in Denmark an Asynchronous Network run by 3 private suppliers |

---

## Network Layer

The Danish Healthcare Messaging Network is currently the VANS Network.

To be able to communicate over the VANS Network, both senders and receivers **MUST** have an EAN number issued by the SOR.

To be able to communicate a specific MedCom FHIR messagetype both senders and receivers **MUST** be registered in SOR with that messagetype and version.

### VANSEnvelope

The VANSenvelope is developed to contain xml-based or other non-edifact messagetypes over the VANS Network

MedCom FHIR Messages **SHALL** be enveloped in a VANSenvelope wether they are shipped as "application/fhir+xml" or "application/fhir+json"

- The enveloping of MedCom FHIR Messages **SHALL** follow the VANS ENVELOPE specification outlined in
  - [VANS ENVELOPE specification (Danish)](https://svn.medcom.dk/svn/releases/Standarder/Den%20gode%20VANSEnvelope/Dokumentation/Den%20gode%20VANSEnvelope.pdf)
- MedCom FHIR Messages **SHALL** follow the metadata specification outlined in
  - [Network Envelope (Danish)](/assets/documents/FHIRMessages_NetworkEnvelopes_DA.md)
  - [Network Envelope (English)](/assets/documents/FHIRMessages_NetworkEnvelopes_EN.md)

### Reliable Messaging

Reliable Messaging Model

![reliable-messaging-principle](https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/Ws-reliablemessaging.png "Ws-reliablemessaging")

A Application Source (AS) wishes to reliably send messages to an Application Destination (AD) over an unreliable infrastructure. To accomplish this, they make use of a Reliable Messaging Source (RMS) and a Reliable Messaging Destination (RMD). The AS sends a message to the RMS. The RMS uses the a Reliable Messaging protocol to transmit the message to the RMD. The RMD delivers the message to the AD. If the RMS cannot transmit the message to the RMD for some reason, it must raise an exception or otherwise indicate to the AS that the message was not transmitted. The AS and RMS may be implemented within the same process space or they may be separate components. Similarly, the AD and RMD may exist within the same process space or they may be separate components.

The protocol defines and supports a number of Delivery Assurances. These are:

**AtLeastOnce**
- Each message will be delivered to the AD at least once. If a message cannot be delivered, an error must be raised by the RMS and/or the RMD. Messages may be delivered to the AD more than once (i.e. the AD may get duplicate messages).

**AtMostOnce**
- Each message will be delivered to the AD at most once. Messages might not be delivered to the AD, but the AD will never get duplicate messages.

**ExactlyOnce**
Each message will be delivered to the AD exactly once. If a message cannot be delivered, an error must be raised by the RMS and/or the RMD. The AD will never get duplicate messages.
InOrder
Messages will be delivered from the RMD to the AD in the order that they are sent from the AS to the RMS. This assurance can be combined with any of the above assurances.
<!-->
Reliable messaging is defined as:

"Reliable messaging refers to the ability of a sender to deliver a message once and only once to its intended receiver. However the key requirements of reliable messaging can be captured more formally as follows:

- Support carrying message traffic reliably in support of business processes whose lifetimes commonly exceed the up times of the components on which these processes are realized
- Support quality-of-service assertions such as:
  - Each message sent be received exactly once (once and only once), at most once, at least once, and so on
  - Messages be received in the same order in which they were sent
  - Failure to deliver a message be made known to both the sender and receiver
- Accommodate mobility of a reliable business process to different channels or physical machines
- Support message transfer via intermediaries
- Leverage the SOAP extensibility mechanism to achieve reliable messaging
- Enable reliable messaging bindings to a variety of underlying reliable and unreliable transport protocols together with the Message Routing Protocol
- Compose with other protocols to support security and other message delivery services
-->

#### Reliable Messaging using VANSEnvelope

[Reliable Messaging using VANSEnvelope](/assets/documents/Reliable_Messaging-VANSEnvelope.md)

![vansenvelope-reliable-messaging-principle](https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/vansenvelope-reliable-messaging-principle.png "vansenvelope-reliable-messaging-principle")

---

## MedCom FHIR Messaging

FHIR Resources can be used in a traditional messaging context, much like HL7 v2. Applications asserting conformance to this framework claim to be conformant to "FHIR messaging".

In FHIR messaging, a "request message" or an "unsolicidated message" is sent from a source application to a destination application when an event happens. Events mostly correspond to things that happen in the real world.

The events supported in MedCom FHIR Messaging, along with the resources that are included in them, are defined in: [MedCom FHIR Messaging events](/assets/documents/MedCom-FHIR-Messaging-Events.md).

The message consists of a Bundle identified by the type "message", with the first resource in the bundle being a MessageHeader resource. The MessageHeader resource has a code - the message event - that identifies the nature of the message, and it also carries additional metadata. The other resources in the bundle depend on the type of the message, eg. in which context a message is triggered.

The destination application processes the message and returns an acknowledgment message and maybe one or more response messages, which too are a bundle of resources identified by the type "message", with the first resource in each bundle being a MessageHeader resource with a response section that reports the outcome of processing the message and any additional response resources required.

### Basic Danish Messaging Assumptions [TBD]

This specification assumes that content will be delivered from one application to another by some delivery mechanism, and then one or more responses will be returned to the source application.

In Denmark this specification rules the exchange of messages through the Danish Messaging Network, currently known as VANS, and using the central organization register, SOR, for delivering the virtual adressing information.

The agreements around the content of the messages and the behavior of the two applications form the "contract" that describes the exchange. These contracts are exactly what MedCom delivers in the Danish Healthcare Domain and therefore MedCom adds regional and local agreements to the rules defined in the HL7 FHIR specification.

This specification ignores the existence of interface engines and message transfer agents that exist between the source and destination. Either they are transparent to the message/transaction content and irrelevant to this specification, or they are actively involved in manipulating the message content (in particular, the source and destination headers are often changed). If these middleware agents are modifying the message content, then they become responsible for honoring the contract that applies (including applicable profiles) in both directions.

### Message Exchange Patterns

Each MedCom FHIR message has one or more response messages. There **SHALL** be at least one response message, an Acknowledgment message, so that the sender can know, that the message was properly received. 

Multiple response messages **SHALL NOT** be returned for messages of consequence, and **SHOULD** not be returned for notifications.

In principle, source applications **SHOULD** not wait for a response to a transaction before issuing a new transaction. However, in many cases, the messages in a given stream are dependent on each other, and must be sent and processed in order. In addition, some transfer methods may require sequential delivery of messages.

#### Asynchronous

In Asynchronous messaging, the server acknowledges receipt of the message immediately, and responds to the sender separately. The server may respond more than once to any given message.
When a message is received, a receiver can determine from the content of the message header whether it's a new message to process, or a response to a message that has already been sent.

### Reliable Messaging using MedCom FHIR Messaging

[Reliable Messaging using MedCom FHIR MessagingMedCom FHIR Messaging](/assets/documents/Reliable_Messaging-FHIR.md)

---

## MedCom FHIR Messages

How is a MedCom FHIR Messages constructed, what parts does it consist of? Below you see the basic MedCom Messaging Model:

![The basic MedCom Messaging Model](https://build.fhir.org/ig/hl7dk/dk-medcom-messaging/MessagingModel.png)

As shown in the diagram above there are 4 MedCom profiled FHIR resources involved in a message:

- A MedComMessagingMessage is a Bundle resource of type "message"

- The MedComMessagingMessage's first resource is a MedComMessagingMesssageHeader, which is a MesssageHeader resource

- The MedComMessagingMesssageHeader points to at least two organizations for the MedComMessagingMessage:
  - a source organization called a MedComMessagingOrganization, which is an Organization resource
  - a destination organization also a MedComMessagingOrganization, which too is an Organization resource

- The MedComMessagingMessage's MedComMessagingProvennance, which is a Provennance resource

### MedComMessagingMessage (Bundle)

A Bundle resource of type "message", which is a container for a collection of other resources.

### Scope and Usage

One common operation performed with resources is to gather a collection of resources into a single instance with containing context. In FHIR this is referred to as "bundling" the resources together. These resource bundles are useful for a variety of different reasons, including sending a set of resources as part of a message exchange (see Messaging)

[Bundle in FHIR R4](http://hl7.org/fhir/R4/bundle.html)

| **MedComMessingMessage Rules**|
|:---|
| A MedCom FHIR Message **SHALL** be a bundle resource of type "message" |
| A MedCom FHIR Message **SHALL** contain at least one bundled MedComMessagingHeader resource |
| The MedComMessagingHeader resource **SHALL** be the first resource in a MedCom Message Bundle |
| A MedCom FHIR Message **SHALL** contain at least two bundled MedComMessagingOrganization resources |
| One of the two bundled MedComMessagingOrganization resources **SHALL** represent the Sender Organization pointed to by the MedComMessagingHeader.sender element |
| One of the two bundled MedComMessagingOrganization resources **SHALL** represent the Receiver Organization pointed to by the MedComMessagingHeader.destination:primary sliced element |
| A MedCom FHIR Message **MAY** contain more bundled MedComMessagingOrganization resources |
| The MedComMessagingHeader resource **MAY** include a list of carbon-copy receiver organizations pointed to by the MedComMessagingHeader.destination:cc sliced element(s) |
| The bundled MedComMessagingOrganization resource **MAY** represent one of the carbon-copy receiver Organizations pointed to by the MedComMessagingHeader.destination:cc sliced element |
| A MedCom FHIR Message **SHALL** contain at least one bundled MedComCorePatient resource |
| A MedCom FHIR Message **SHALL** contain at least one bundled MedComMessagingProvenance resource |
| A MedCom FHIR Message **SHALL** contain one bundled focused resource pointed to by the MedComMessagingHeader |
| The MedComMessagingHeader resource **SHALL** contain a Narrative text |

[here](https://github.com/hl7dk/dk-medcom-messaging/blob/master/input/pagecontent/index.md)

[Permalink here](https://github.com/hl7dk/dk-medcom-messaging/blob/b23dfe00cba8aba273ca08ab7eead8228952f6c4/input/pagecontent/index.md)

### Narrative Texts

A Narrative Text is a human-readable narrative that contains a summary of the resource and can be used to represent the content of the resource to a human. The narrative need to encode all the structured data pointed oout by the ∑-symbol and it is required to contain sufficient detail to make it "clinically safe" for a human to just read the narrative.
Contained resources do not have narrative, but their content SHALL be represented in the ressource container.

Narratives contains two sub elements, status and div.

**The div element**

The contents of the div element are an XHTML fragment that **SHALL** contain only the basic HTML formatting elements described in chapters 7-11 (except section 4 of chapter 9) and 15 of the HTML 4.0 standard, <a> elements (either name or href), images and internally contained style attributes. 

The XHTML content **SHALL NOT** contain a head, a body element, external stylesheet references, deprecated elements, scripts, forms, base/link/xlink, frames, iframes, objects or event related attributes (e.g. onClick). This is to ensure that the content of the narrative is contained within the resource and that there is no active content. Such content would introduce security issues and potentially safety issues with regard to extracting text from the XHTML. Note that even with these restrictions, there are still several important security risks associated with displaying the narrative.

The div element **SHALL** have some non-whitespace content (text or an image).

| **General Narrative Text Rules**|
|:---|
| All resources in a MedComMessingMessage **SHALL** contain a Narrative Text defined by the [resource].Text element |
| The Narrative Text **SHALL** have a status with value "extensions". Extensions means that the contents of the narrative are entirely generated from the core elements in the content and some of the content is generated from extensions. |
 The narrative **SHALL** reflect the impact of all modifier extensions. |

[Narrative Text description in FHIR R4](http://hl7.org/fhir/R4/narrative.html#Narrative)

[NarrativeStatus in FHIR R4](http://hl7.org/fhir/R4/codesystem-narrative-status.html#4.3.14.424.2)

[Styling the XHTML in FHIR R4](http://hl7.org/fhir/R4/narrative.html#css)

### MessageHeader

<p align="left">
  <img src="https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/MedComMessageHeader.png">
</p>

<!--
![alt text](https://medcomdk.github.io/MedCom-FHIR-Communication/assets/images/MedComMessageHeader.png "MedComMessageHeader")
-->

| **MedComMessageHeader Rules**|
|:---|
| The MedComMessagingHeader resource **SHALL** be the first resource in a MedCom Message Bundle |
| The MedComMessagingHeader resource **SHALL** contain an event of the MedCom Message (eg. the type of the message) |
| The MedComMessagingHeader resource **SHALL** contain an MedComMessagingHeader.id of the MedCom Message (eg. the letter.id of the message) |
| One of the two bundled MedComMessagingOrganization resources **SHALL** represent the Sender Organization pointed to by the MedComMessagingHeader.sender element |
| One of the two bundled MedComMessagingOrganization resources **SHALL** represent the Receiver Organization pointed to by the MedComMessagingHeader.destination:primary sliced element |
| The MedComMessagingHeader resource **MAY** include a list of carbon-copy receiver organizations pointed to by the MedComMessagingHeader.destination:cc sliced element(s) |
| MedCom FHIR Messages **SHALL** contain one bundled focused resource pointed to by the MedComMessagingHeader pointed to by the MedComMessagingHeader.focus element |

[MedComMessageHeader](/assets/documents/MessageHeader.md)

[MessageHeader in FHIR R4](http://hl7.org/fhir/R4/messageheader.html)

### Identifiers

[Identifiers](/assets/documents/MessageHeader_Identifiers.md)

### Timestamps

[Timestamps](/assets/documents/MessageHeader_Timestamps.md)

### Messaging rules

[Messaging rules (Danish)](/assets/documents/Rules_Messaging-DA.md)
[Messaging rules (English)](/assets/documents/Rules_Messaging-EN.md)

### Acnowledgment rules

[Acnowledgment rules (Danish)](/assets/documents/Rules_Acknowledgment-DA.md)
[Acnowledgment rules (English)](/assets/documents/Rules_Acknowledgment-EN.md)

## MustSupport

[MustSupport](/assets/documents/MustSupport.md)

## Provenance

Provenance of a resource is a record that describes entities and processes involved in producing and delivering or otherwise influencing that resource. Provenance provides a critical foundation for assessing authenticity, enabling trust, and allowing reproducibility. Provenance assertions are a form of contextual metadata and can themselves become important records with their own provenance. Provenance statement indicates clinical significance in terms of confidence in authenticity, reliability, and trustworthiness, integrity, and stage in lifecycle (e.g. Document Completion - has the artifact been legally authenticated), all of which may impact security, privacy, and trust policies.

### Scope and Usage

The Provenance resource tracks information about the activity that created, revised, deleted, or signed a version of a resource, describing the entities and agents involved. This information can be used to form assessments about its quality, reliability, trustworthiness, or to provide pointers for where to go to further investigate the origins of the resource and the information in it.

Provenance resources are a record-keeping assertion that gathers information about the context in which the information in a resource was obtained. Provenance resources are prepared by the application that initiates the create/update etc. of the resource. An AuditEvent resource contains overlapping information, but is created as events occur, to track and audit the events. AuditEvent resources are often (though not exclusively) created by the application responding to the read/query/create/update/etc. event.

- MedCom FHIR Messages **SHALL** contain at least one bundled MedComMessagingProvenance resource
- MedCom FHIR Messages **SHALL** contain one bundled MedComMessagingProvenance resource for each message exchange the message has been involved in
- MedCom FHIR Messages **SHALL** contain no more than two bundled MedComMessagingProvenance resource when acknowledging a message

<p align="left">
  <img src="https://build.fhir.org/ig/hl7dk/dk-medcom-messaging/MedComMessagingProvenance.png">
</p>

<!--
![alt text](https://build.fhir.org/ig/hl7dk/dk-medcom-messaging/MedComMessagingProvenance.png "MedCom Messaging Provenance key concepts(Remote)")
-->

[MedComs use of Provenance](/assets/documents/Provenance.md)

[HL7 FHIR description of Provenance](http://hl7.org/fhir/R4/provenance.html)

## Test and Certification

All profiles **MUST** be validated with the FHIR validator

All profiles **MUST** be validated with TouchStone

## Release Notes

Updates in the latest release.