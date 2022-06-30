# MedCom FHIR Messages And Network Envelopes

![alt text](https://medcomdk.github.io/MedCom-FHIR-Communication/fhir-logo.png "HL7 FHIR")

## Table of Content

[1. Introduction](#introduction) <br/>
[2. Shipping envelopes](#shipping-envelopes) <br/>
[2.1 VANSenvelope](#vansenvelope)) <br/>
[2.1.1 Format](#format) <br/>
[2.1.2 Name](#name) <br/>
[2.1.3 Version](#version) <br/>
[3. FHIR message types](#medcom-fhir-message-types) <br/>
[3.1 CareCommunication](#carecommunication) <br/>
[3.2 HospitalNotification](#hospitalnotification)) <br/>
[3.3 Acknowledgment](#acknowledgement)) <br/>

---

## Introduction

MedCom's FHIR messages will be wrapped and appear in various envelope formats during their shipping process.

Pt. shipping will take place in the existing VANS network and thus with the use of VANSenvelope unless otherwise specified under the individual standard. Reception can be both in VANSenvelope or in another reception envelope, e.g. KOMBITs BeskedFordeler envelope.

Obs. When modernized infrastructure is implemented, it will draw on a new shipping envelope that will replace VANSenvelope, so this document will by that time be updated with the new envelope format. For a transitional period, both VANSenvelope and the new envelope will be used, but there will be clear clarifications of how this will take place.

---

---

## Shipping envelopes

### VANSenvelope

In relation to MedCom's new FHIR messages, VANSenvelope contains 3 elements (fields) which are influenced by FHIR as a new message type. These are contained in the following parent element "VANSEnvelope/Message/MetaInformation/Document/".

The elements contained are:

- Format
- Name
- Version

MedCom's FHIR-messages **SHALL** be handled like all other messages in VANSenvelope by  base64-encoding the message in the element "VANSEnvelope/Message/Data/"

In the Transport element, "VANSEnvelope/Message/MetaInformation/Transport", the "TransformMessage" element is handled as usual, while "ServiceTag" with the attribute name = "MCM:MIME" **SHALL** be specified with one of the following values:

- application/fhir+xml
- application/fhir+json

depending on the format in which the FHIR-message is formatted.

---

#### Format

Format **SHALL** be the same as "Standard type" in MedCom's Standards Directory and **SHALL** be defined for all FHIR-standards as "HL7".

---

#### Name

Name **SHALL** be the same as "Type nr." in MedCom's Standards Directory and will thus vary from messagetype to messagetype. Name **SHALL** be prefixed with MCM: and will otherwise be able to be postfixed with statistical variants of a given messagetype. Known from GGOP, this outcome space can e.g. be GGOP1, GGOP2 and GGOP3. Similar constructions will occur as long as FHIR-messages are transported in the VANSenvelope.

---

#### Version

Version **MUST** be the same as "Version" in MedCom's standard directory and will thus vary from message version to message version.

---

## MedCom FHIR message types

Specifically, the above for MedCom's FHIR messages means this

---

### CareCommunication

|||
|:---|:---|
|Envelope           |VANSenvelope                           |
|Format             |"HL7"                                  |
|Name               |"MCM:FDIS91#`<postfix value>`"         |
|Version            |"2.0.0"                                |

Name **MUST** explicitly be taken from the following ValueSet: [CodeSystem-medcom-messaging-sorEdiSystem](https://build.fhir.org/ig/hl7dk/dk-medcom/CodeSystem-medcom-messaging-sorEdiSystem.html)

Postfix Values for Name **MUST** be within this ValueSet, which is taken from: [CareCommunications ValueSet for categories](https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-careCommunication-categories.html)

The combined Name+Postfix **MUST** explicitly conform with the following ValueSet: [https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html](https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html)

---

### HospitalNotification

|||
|:---|:---|
|Envelope Sender    |VANSenvelope (EPJ)                      |
|Envelope Receiver  |KOMBIT's BeskedFordeler envelope (EOJ)  |
|Format             |"HL7"                                   |
|Name               |"MCM:FDIS20#`<postfix value>`"          |
|Version            |"2.0.0"                                 |

Name **MUST** explicitly be taken from the following ValueSet: [CodeSystem-medcom-messaging-sorEdiSystem](https://build.fhir.org/ig/hl7dk/dk-medcom/CodeSystem-medcom-messaging-sorEdiSystem.html)

Postfix Values for Name **MUST** be within this ValueSet, which is taken from the HospitalNotification ValueSet: MedCom Hospital Notification Message Activity Codes:  [https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-hospitalNotification-messageActivities.html](https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-hospitalNotification-messageActivities.html)

The combined Name+Postfix **MUST** explicitly conform with the following ValueSet: [https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html](https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html)

---

### Acknowledgement

|||
|:---|:---|
|Envelope           |VANSenvelope                           |
|Format             |"HL7"                                  |
|Name               |"MCM:FCTL1#`<postfix value>`"          |
|Version            |"2.0.0"                                |

Name **MUST** explicitly be taken from the following ValueSet: [https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html](https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html)

Postfix Values for Name **MUST** be within this ValueSet, which is taken from the Response Code ValueSet: Codes:  [http://hl7.org/fhir/R4/valueset-response-code.html](http://hl7.org/fhir/R4/valueset-response-code.html)

The combined Name+Postfix **MUST** explicitly conform with the following ValueSet: [https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html](https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html)

---