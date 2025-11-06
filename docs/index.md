# Governance for MedCom FHIR®© Messaging

**Table of contents**
* [1 Introduction to Governance for MedCom FHIR Messaging](#1-introduction-to-governance-for-medcom-fhir-messaging)
* [2 Terms and abbreviations](#2-terms-and-abbreviations)
* [3 Message exchange](#3-message-exchange)
  + [3.1 Governance for Reliable Messaging in general](#31-governance-for-reliable-messaging-in-general)
  + [3.2 Governance for Network Layer](#32-governance-for-network-layer)
    * [3.2.1 VANSenvelope specifications](#321-vansenvelope-specifications)
  + [3.3 Governance for MedCom FHIR Message Exchange](#33-governance-for-medcom-fhir-message-exchange)
* [4 MedCom FHIR Messages](#4-medcom-fhir-messages)
  + [4.1 Governance for MedCom FHIR Messages](#41-governance-for-medcom-fhir-messages)
  + [4.2 Governance for displaying MedCom FHIR Messages](#42-governance-for-displaying-medcom-fhir-messages)
  + [4.3 Governance for EpisodeOfCare-identifier](#43-governance-for-episode-of-care-identifiers)
* [5 Versions of MedCom FHIR Standards](#5-versions-of-medcom-fhir-standards)
* [6 FHIR Validation in Messaging](#6-fhir-validation-in-messaging)
<br>

## 1 Introduction to Governance for MedCom FHIR Messaging

On this page, you can find information about how MedCom has profiled the <a href="http://hl7.org/fhir/R4/messaging.html" target="_blank">HL7 FHIR Messaging Framework</a> to work in a Danish context.
Governance for MedCom HL7 FHIR Messaging describes the basic ruleset of how MedCom Messages must be exchanged in the Danish Healthcare Messaging Network.
The Danish ruleset is based on:

* the ruleset for the Danish VANS Network
* the general <a href="http://hl7.org/fhir/R4/messaging.html" target="_blank">HL7 FHIR Communication Rules for FHIR Messaging</a>
* the Danish profiling of FHIR messaging.

<br>

These MedCom FHIR Messaging Governance rules are intended to clarify the use of MedCom’s FHIR messages for the health and social area. Formerly, these kinds of rules for other MedCom Messaging paradigms were known as ”Syntax & Communication Rules”.

It is the intention that the MedCom FHIR Messaging Governance rules together with MedCom’s FHIR standards for the individual messages form the full and sufficient basis for implementing MedCom’s healthcare messages. Thus, the governance rules must be able to function as “a chief judge”, where there is doubt about the practical application of MedCom’s FHIR messages.

In the following, we follow a top-down approach by initially addressing shipping over the Network Layer and its ruleset, followed by the logistics for MedCom FHIR Messaging and lastly the basic ruleset of how to compose a MedCom FHIR message. Initially, is a brief introduction to the use of terms presented. 

<!-- The “Governance for MedCom FHIR Messaging” ensures uniform use of MedCom’s FHIR messages to the health and social domains in Denmark. -->

<!-- 
Here, you will find how MedCom has profiled the HL7 FHIR Messaging Framework to work in a Danish context. -->

<!-- Governance for MedCom HL7 FHIR Messaging is the basic ruleset of how MedCom Messages must be exchanged in the Danish Healthcare Messaging Network.

The Danish ruleset is based on:

* the ruleset for the Danish VANS Network, the Danish profiling of FHIR messaging 
*

In the following we follow a top-down approach by addressing shipping over the Network Layer and its ruleset first, then the logistics for MedCom FHIR Messaging and last cover the basic ruleset of how to compose a MedCom FHIR message. -->

<!-- [Introduction details (Danish)](/assets/documents/1-Introduction.md)-->

<!-- [Generelle tekniske use cases](Generelle-tekniske-use-cases-v1.0.0-b2.md) -->


## 2 Terms and abbreviations

[Click here to get an overview of the terms and abbreviations used in to describe the Governance.](/assets/documents/011_Governance_Terms.md)

## 3 Message exchange

MedCom FHIR Messaging is based on Asynchronous Messaging. In Asynchronous messaging, a Sending EcoSystem dispatches an unsolicited message to a Receiving EcoSystem possibly through several intermediate hubs. Besides sending a possibly requested acknowledgement immediately as a response, the Receiving EcoSystem responds to the Sending EcoSystem separately. The Receiving EcoSystem may respond more than once to any given message.

When implementing a MedCom FHIR standard, it is fundamental to understand in which context the standard should be used to ensure that the implementation fulfils the business requirements. Therefore, it is important to understand the standard documentation for the given standard. 
Furthermore, it is essential to understand the messaging framework and the possibilities of the VANS Network, as the FHIR standards define the process for how information is packaged and sent from one part to another through the VANS Network.
The messaging framework and the VANS Network are described as governance, previously known as the “Syntax and Communication Rules". <br>
<a href="https://medcomdk.github.io/MedCom-FHIR-Communication/#network-layer" target="_blank"> Click here to get more information about governance.</a>  

When exchanging a MedCom FHIR message, it is allowed to send in a FHIR+JSON og FHIR+XML format, which is in alignment with HL7 FHIR. 

### 3.1 Governance for Reliable Messaging in general

Governance for Reliable Messaging in general lays the grounds for Governance for Reliable Messaging using VANSenvelope and Governance for Reliable Messaging using FHIR. The generic ruleset defines the other two rulesets.

[Click here to go to Reliable Messaging in general.](/assets/documents/020_Governance-for-Reliable-Messaging-in-general.md)

### 3.2 Governance for Network Layer

Governance for Network Layer covers rulesets for VANSEnvelope and Reliable Messaging using VANSenvelope.

[Click here to go to Governance for Network Layer.](/assets/documents/030_Governance-for-Network-Layer.md)

Reliable Messaging using VANSEnvelope describes different scenarios when using the VANSEnvelope. This is a profiling of the scenarios described in [Reliable Messaging in general.](/assets/documents/020_Governance-for-Reliable-Messaging-in-general.md) mentioned in [section 3.1](#31-governance-for-reliable-messaging-in-general). 

[Click here to see how to setup Reliable Messaging using VANSEnvelope](/assets/documents/032_Reliable_Messaging-VANSEnvelope.md)

#### 3.2.1 VANSenvelope specifications

[Click here to go to the specifications for VANSenvelope](/assets/documents/FHIRMessages_NetworkEnvelopes_EN.md).

### 3.3 Governance for MedCom FHIR Message Exchange

Governance for MedCom FHIR Messaging covers Reliable Messaging using MedCom FHIR Messaging, sending and receiving scenarios, and rulesets for FHIR Messaging and FHIR Messaging Acnowledgement.

[Click here to go to Governance for MedCom FHIR Messaging.](/assets/documents/040_Governance4FHIR-Messaging.md)

Reliable Messaging using MedCom FHIR Messaging describes different scenarios when using FHIR messages. This is a profiling of the scenarios described in [Reliable Messaging in general.](/assets/documents/020_Governance-for-Reliable-Messaging-in-general.md) mentioned in [section 3.1](#31-governance-for-reliable-messaging-in-general).

[Click here to see how to apply Reliable Messaging using MedCom FHIR Messaging](/assets/documents/043_Reliable_Messaging-VANSEnvelope.md)

## 4 MedCom FHIR Messages

An implementer of a MedCom FHIR Message Standard **SHALL** be compliant with all parts of the documentation laid out for the MedCom FHIR Messaging framework.

You can find a description here:<a href="https://medcomdk.github.io/dk-medcom-messaging/assets/documents/Intro-Technical-Spec-ENG.html#21-medcommessagingmessage-bundle" target="_blank"> Click here to read the documentation for the MedCom FHIR Messaging framework</a>


### 4.1 Governance for MedCom FHIR Messages

Governance for MedCom FHIR Messages covers the basic ruleset for a MedCom FHIR Message, MedComMessagingMessage and its content, including MedComMessagingMessageHeader, MedComMessagingOrganization and MedComMessagingProvenance.

[Click here to go to Governance for MedCom FHIR Messages.](/assets/documents/050_Governance-for-MedCom-FHIR-Messages.md)

### 4.2 Governance for displaying MedCom FHIR Messages

Governance for displaying MedCom FHIR Messaging covers the basic demands for a sending system to be able to display before sending and the basic demands for a receiving system to be able to display after having received a MedComMessagingMessage.

[Click here to go to Governance for displaying MedCom FHIR Messages](/assets/documents/060_Governance-for-displaying-MedCom-FHIR-Messages.md)

### 4.3 Governance for episode of care identifiers 

An episode of care identifier (Danish: forløbsid) is used for linking messages exchanged during a message flow. When the episode of care identifier is received e.g. in a ReportOfAdmission (Danish: Indlæggelsesrapport), ProgressOfCarePlan (Danish: Plejeforløbsplan), HospitalNotification (Danish: Advis om sygehusophold) or a previous CareCommunication (Danish: Korrespondancemeddelelse), it must be returned.

[Click here to reade more about episode of care identifiers](/assets/documents/080_Governance-for-episode-of-care-identifiers.md)

## 5 Versions of MedCom FHIR Standards
Vendors should be prepared to handle multiple versions of a MedCom FHIR standard.
The version of the standard is not explicitly stated in a message. However, the version of a received message can be found in the [VANSEnvelope, which is described in the section of Governance for Network Layer](/assets/documents/030_Governance-for-Network-Layer.md).

MedCom is, as of 2025, starting to introduce references in the MessageHeader to MessageDefinitions via the `definition` element. This means that future releases containing MessageHeaders will have an associated MessageDefinition linked. You can find the Implementation Guide for MessageDefinitions [here](https://medcomfhir.dk/ig/messagedefinitions/). MessageDefinitions contains the the standard's version.

When receiving a MedCom FHIR message, it should be validated against the rules and contraints defined in the associtated Implementation guide of the same version. If it is not possible for you to use the versionnumber from the envelopes, it is recommended that systems always validate a message against the latest version of the standard when recieving a such one. As long as there are no breaking changes in the standard (i.e. a non-backwards compatible change) this will be a viable way to go.

## 6 FHIR Validation in Messaging

Vendors using a MedCom FHIR Messaging standard **MUST** follow specific rules for how validation must be performed. See the [governance for validation here](https://medcomdk.github.io/MedComLandingPage/assets/documents/FHIRValidationGovernance.html).