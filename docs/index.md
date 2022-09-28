# Governance for MedCom FHIR®© Messaging

<hr>

## Table of contents

* [Terms](#terms)
* [1 Introduction to Governance for MedCom FHIR Messaging](#1-introduction-to-governance-for-medcom-fhir-messaging)
* [2 Governance for Reliable Messaging in general](#2-governance-for-reliable-messaging-in-general)
* [3 Governance for the Network Layer](#3-governance-for-network-layer)
* [4 Governance for MedComFHIR Messaging](#4-governance-for-medcom-fhir-messaging)
* [5 Governance for MedCom FHIR Messages](#5-governance-for-medcom-fhir-messages)
* [6 Governance for displaying MedCom FHIR Messages](#6-governance-for-displaying-medcom-fhir-messages)
* [7 Governance for MedCom Terminology](#7-governance-for-medcom-fhir-terminology)
* [8 Governance for MedCom Terminology Server](#8-governance-for-medcom-fhir-terminology-server)
* [9 Governance-for MedCom versioning](#9-governance-for-medcom-versioning)
* [10 Governance-for MedCom process of change requests](#10-governance-for-medcom-process-of-change-requests)

<hr>

## Terms

![/assets/images/Link-Icon.jpg](#terms "link to here")

### Terms used in Governance for MedCom FHIR Messaging

[Click here to go to an overview of the Governance Terms](/assets/documents/011_Governance_Terms.md)

### Special Terms used in Governance for MedCom FHIR Messaging

MedCom adopts the normative words defined in IETF Best Current Practice 14: Key words for use in RFCs to Indicate Requirement Levels (BCP-14) (currently RFC 2119 and RFC 8174), certain words indicate whether a specific content of the Technical Framework is normative: either required (e.g., “must”, “required”, “shall”) or optional (e.g., “may”, “recommended”). Informative content does not contain these key words.

<a href="https://www.rfc-editor.org/info/rfc2119" target="_blank">Click here to go to RFC 2119 (opens up in a new tab)</a>

RFC 2119 specifies common key words that may be used in protocol specifications.

RFC 8174 aims to reduce the ambiguity by clarifying that only UPPERCASE usage of the key words have the defined special meanings.

<a href="https://www.rfc-editor.org/info/rfc8174" target="_blank">Click here to go to RFC 8174 (opens up in a new tab)</a>

This specification uses the conformance verbs SHALL, SHOULD, and MAY as defined in RFC 2119. Unlike RFC 2119, however, this specification allows that different applications might not be able to interoperate because of how they use optional features. In particular:

* **SHALL**: (or “REQUIRED” or “MUST”) an absolute requirement for all implementations
* **SHALL NOT**: (or "MUST NOT") an absolute prohibition against inclusion for all implementations
* **SHOULD/SHOULD NOT**: (or “RECOMMENDED”/“NOT RECOMMENDED”) A best practice or recommendation to be considered by implementers within the context of their particular implementation; there may be valid reasons to ignore an item, but the full implications must be understood and carefully weighed before choosing a different course
* **MAY**: (or "OPTIONAL") This is truly optional language for an implementation; can be included or omitted as the implementer decides with no implications

<br>

This convention is in compliance with HL7 FHIR use of the terms.

<a href="http://www.hl7.org/fhir/conformance-rules.html#conflang" target="_blank">Click here to go to HL7 FHIR's conformance rules - conformance language (opens up in a new tab)</a>

## 1 Introduction to Governance for MedCom FHIR Messaging

On this page, you can find information about how MedCom has profiled the <a href="http://hl7.org/fhir/R4/messaging.html" target="_blank">HL7 FHIR Messaging Framework (opens up in a new tab)</a> to work in a Danish context.
Governance for MedCom HL7 FHIR Messaging describes the basic ruleset of how MedCom Messages must be exchanged in the Danish Healthcare Messaging Network.
The Danish ruleset is based on both:

* the ruleset for the Danish VANS Network, the Danish profiling of FHIR messaging
* the general <a href="http://hl7.org/fhir/R4/messaging.html" target="_blank">HL7 FHIR Communication Rules for FHIR Messaging (opens up in a new tab)</a>.

<br>

These “MedCom FHIR Messaging Governance rules” are intended to clarify the use of MedCom’s FHIR messages for the health and social area. Formerly these kinds of rules for other MedCom Messaging paradigms were known as ”Syntax & Communication Rules”.

It is the intention that the “MedCom FHIR Messaging Governance rules” together with MedCom’s standards for the individual messages form the full and sufficient basis for implementing MedCom’s healthcare messages. Thus, the governance rules must be able to function as “a chief judge”, where there is doubt about the practical application of MedCom’s FHIR messages.

In the following, we follow a top-down approach by initially addressing shipping over the Network Layer and its ruleset, followed by the logistics for MedCom FHIR Messaging and lastly the basic ruleset of how to compose a MedCom FHIR message.

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

### 1.1 What is a MedCom FHIR Message Standard?

An implementer of a MedCom FHIR Message Standard **MUST** be compliant with all parts of the documentation laid out for the MedCom FHIR Message Standard.

You can find a description here:<a href="https://medcomdk.github.io/dk-medcom-messaging/#12-medcommessagingmessage-bundle" target="_blank"> Documentation for the MedCom FHIR Message Standard (opens up in a new tab)</a>

### 1.2 Asynchronous Messaging

MedCom FHIR Messaging is based on Asynchronous Messaging.

In Asynchronous messaging, a Sending EcoSystem dispatches an unsolicited message to a Receiving EcoSystem possibly through several intermediate hubs. Besides sending a possibly requested acknowledgement immediately as a response, the Receiving EcoSystem responds to the Sending EcoSystem separately. The Receiving EcoSystem may respond more than once to any given message.

## 2 Governance for Reliable Messaging in general

Governance for Reliable Messaging in general lays the grounds for Governance for Reliable Messaging using VANSenvelope and Governance for Reliable Messaging using FHIR. The generic ruleset defines the other two rulesets.

[Click here to go to Reliable Messaging in general.](/assets/documents/020_Governance-for-Reliable-Messaging-in-general.md)

## 3 Governance for Network Layer

Governance for Network Layer covers rulesets for VANSEnvelope and Reliable Messaging using VANSenvelope.

[Click here to go to Governance for Network Layer.](/assets/documents/030_Governance-for-Network-Layer.md)

## 4 Governance for MedCom FHIR Messaging

Governance for MedCom FHIR Messaging covers Reliable Messaging using MedCom FHIR Messaging, sending and receiving scenarios, and rulesets for FHIR Messaging and FHIR Messaging Acnowledgement.

[Click here to go to Governance for MedCom FHIR Messaging.](/assets/documents/040_Governance4FHIR-Messaging.md)

## 5 Governance for MedCom FHIR Messages

Governance for MedCom FHIR Messages covers the basic ruleset for a MedCom FHIR Message, MedComMessagingMessage and its content, MedComMessagingMessageHeader, MedComMessagingOrganization and MedComMessagingProvenance

[Click here to go to Governance for MedCom FHIR Messages.](/assets/documents/050_Governance-for-MedCom-FHIR-Messages.md)

## 6 Governance for displaying MedCom FHIR Messages

Governance for displaying MedCom FHIR Messaging covers the basic demands for a sending system to be able to display before sending and the basic demands for a receiving system to be able to display after having received a MedComMessagingMessage.

[Click here to go to Governance for displaying MedCom FHIR Messages](/assets/documents/060_Governance-for-displaying-MedCom-FHIR-Messages.md)

## 7 Governance for MedCom FHIR Terminology

Governance for MedCom FHIR Terminology covers Codesystems, Valuesets and ConceptMaps, which are published through our MedCom FHIR Terminology IG and hosted on a MedCom FHIR Terminology Server.

[Click here to go to Governance for Terminology.](/assets/documents/070_Governance-for-Terminology.md)

## 8 Governance for MedCom FHIR Terminology Server

Governance for the MedCom FHIR Terminology Server will appear here when published.

## 9 Governance for MedCom Versioning

MedComFHIRMessages are versioned with Semver 2.0 [Link to Semver 2.0 (opens in a new tab)](https://www.semver.com)

[Click here to go to Governance for Terminology.](/assets/documents/090_MedCom-Versioning.md)

## 10 Governance for MedCom process of change requests

Change reuests regarding FHIR Messaging **SHALL** be reported through one of the following channels:

[Click here to go to Governance for MedCom process of change requests.](/assets/documents/10 Governance-for-MedCom-process-of-change-requests.md)
