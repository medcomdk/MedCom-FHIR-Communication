# Governance for MedCom FHIR®© Messaging

## Table of Content

* [1 Introduction to Governance for MedCom FHIR Messaging](#1-introduction-to-governance-for-medcom-fhir-messaging)
* [2 Governance for Reliable Messaging in general](#2-governance-for-reliable-messaging-in-general)
* [3 Governance for the Network Layer](#3-governance-for-network-layer)
* [4 Governance for MedComFHIR Messaging](#4-governance-for-medcom-fhir-messaging)
* [5 Governance for MedCom FHIR Messages](#5-governance-for-medcom-fhir-messages)
* [6 Governance for displaying MedCom FHIR Messaging](#6-governance-for-displaying-medcom-fhir-messaging)
* [7 Governance for MedCom Terminology](#7-governance-for-medcom-fhir-terminology)
* [8 Governance for MedCom Terminology Server](#8-governance-for-medcom-fhir-terminology-server)

### Terms used in Governance for MedCom FHIR Messaging

[Tab here to get an overview of the Governance Terms](/assets/documents/011_Governance_Terms.md)

## 1 Introduction to Governance for MedCom FHIR Messaging

On this page you can find information about how MedCom has profiled the [HL7 FHIR Messaging Framework](http://hl7.org/fhir/R4/messaging.html) to work in a Danish context.
Governance for MedCom HL7 FHIR Messaging describes the basic ruleset of how MedCom Messages shall be exchanged in the Danish Healthcare Messaging Network.
The Danish ruleset is based on both the ruleset for the Danish VANS Network, the Danish profiling of FHIR messaging and the general HL7 FHIR Communication Rules for FHIR Messaging.These “MedCom FHIR Messaging Governance rules” are intended to clarify the use of MedCom’s FHIR messages for the health and social area. Formerly these kind of rules for other MedCom Messaging paradigms were known as ”Syntax & Communication Rules”.

It is the intention that the “MedCom FHIR Messaging Governance rules” together with MedCom’s standards for the individual messages form the full and sufficient basis for implementing MedCom’s healthcare messages.The governance rules must thus be able to function as “chief judge”, where there is doubt about the practical application of MedCom’s FHIR messages.

The “Governance for MedCom FHIR Messaging” ensures a uniform use of MedCom’s FHIR messages to the health and social domains in Denmark.
In the following we follow a top-down approach by initially addressing shipping over the Network Layer and its ruleset, then the logistics for MedCom FHIR Messaging and lastly the basic ruleset of how to compose a MedCom FHIR message.

What you will find here is, how MedCom has profiled the HL7 FHIR Messaging Framework to work in a Danish context.

Governance for MedCom HL7 FHIR Messaging is the basic ruleset of how MedCom Messages must be exhanged in the Danish Healthcare Messaging Network.

The Danish ruleset is based on both the ruleset for the Danish VANS Network, the Danish profiling of FHIR messaging and the general HL7 FHIR Communication Rules for FHIR Messaging can be found on the <a href="http://hl7.org/fhir/R4/messaging.html" target="_blank">HL7 FHIR R4 Messaging Website</a>.

These "MedCom FHIR Messaging Governance rules" are intended to clarify the use of MedCom's FHIR messages for the health and social area. Formerly these kind of rules for other MedCom Messaging paradigms were known as 'Syntax & Communication Rules'

It is the intention that the governance rules together with MedCom's standards for the individual messages form the full and sufficient basis for implementing MedCom's healthcare messages.The governance rules must thus be able to function as “chief judge”, where there is doubt about the practical application of MedCom's FHIR messages.

The "Governance for MedCom FHIR Messaging" must ensure a uniform use of MedCom's FHIR messages to the health and social area domains in Denmark.

In the following we follow a top-down approach by addressing shipping over the Network Layer and its ruleset first, then the logistics for MedCom FHIR Messaging and last cover the basic ruleset of how to compose a MedCom FHIR message.

<!-- [Introduction details (Danish)](/assets/documents/1-Introduction.md)-->

<!-- [Generelle tekniske use cases](Generelle-tekniske-use-cases-v1.0.0-b2.md) -->

### 1.1 What is a MedCom FHIR Message Standard

An implementer of a MedCom FHIR Message Standard **SHALL** be compliant with all the parts of the documentation laid out for the MedCom FHIR Message Standard and described here: [Documentation for the MedCom FHIR Message Standard](https://medcomdk.github.io/dk-medcom-messaging/#12-medcommessagingmessage-bundle)

### 1.2 Asynchronous Messaging

MedCom FHIR Messaging is based on Asynchronous Messaging.

In Asynchronous messaging, a Sending EcoSystem dispatches an unsolicited message to a Receiving EcoSystem possibly through several intermediate hubs, and besides from sending an possibly requested acknowledgement immediately as a response, the Receiving EcoSystem responds to the Sending EcoSystem separately. The Receiving EcoSystem may respond more than once to any given message.

## 2 Governance for Reliable Messaging in general

Governance for Reliable Messaging in general lays the grounds for Governance for Reliable Messaging using VANSenvelope and Governance for Reliable Messaging using FHIR. It's the generic ruleset, which the 2 other rulesets are defined from.

[Reliable Messaging in general](/assets/documents/020_Governance-for-Reliable-Messaging-in-general.md)

## 3 Governance for Network Layer

Governance for Network Layer covers rulesets for VANSEnvelope and Reliable Messaging using VANSenvelope.

[Governance for Network Layer](/assets/documents/030_Governance-for-Network-Layer.md)

## 4 Governance for MedCom FHIR Messaging

Governance for MedCom FHIR Messaging covers Reliable Messaging using MedCom FHIR Messaging, sending and receiving scenarios, and rulesets for FHIR Messaging and FHIR Messaging Acnowledgement.

[Governance for MedCom FHIR Messaging](/assets/documents/040_Governance4FHIR-Messaging.md)

## 5 Governance for MedCom FHIR Messages

Governance for MedCom FHIR Messages covers the basic ruleset for a MedCom FHIR Message, MedComMessagingMessage and its content, MedComMessagingMessageHeader, MedComMessagingOrganization and MedComMessagingProvenance

[Governance for MedCom FHIR Messages](/assets/documents/050_Governance-for-MedCom-FHIR-Messages.md)

## 6 Governance for displaying MedCom FHIR Messaging

Governance for displaying MedCom FHIR Messaging covers the basic demands for a sending system to be able to display before sending and the basic demands for a receiving system to be able to display after having received a MedComMessagingMessage.

[Governance for displaying MedCom FHIR Messaging](/assets/documents/060_Governance-for-displaying-MedCom-FHIR-Messaging.md)

## 7 Governance for MedCom FHIR Terminology

Governance for MedCom FHIR Terminology covers Codesystems, Valuesets and ConceptMaps, which are published through our MedCom FHIR Terminology IG and hosted on a our MedCom FHIR Terminology Server. Governance for the MedCom FHIR Terminology Server will 

[Governance for Terminology](/assets//documents/070_Governance-for-Terminology.md)

## 8 Governance for MedCom FHIR Terminology Server

Governance for the MedCom FHIR Terminology Server will appear hear when published.
