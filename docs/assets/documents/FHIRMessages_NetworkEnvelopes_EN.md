# MedCom FHIR Messages And Network Envelopes

## Table of contents

* [1. Introduction](#introduction)
* [2. Shipping envelopes](#shipping-envelopes)
* [2.1 VANSEnvelope](#vansenvelope))
* [3. FHIR message types](#medcom-fhir-message-types)
* [3.1 CareCommunication](#carecommunication)
* [3.2 HospitalNotification](#hospitalnotification)
* [3.3 Acknowledgment](#acknowledgement)

---

## Introduction

MedCom's FHIR messages will be wrapped and appear in various envelope formats during their shipping process.

At present, shipping will take place in the existing VANS network and thus with the use of VANSEnvelope unless otherwise specified under the individual standard. Reception can be both in VANSEnvelope or in another reception envelope, e.g. KOMBIT's BeskedFordeler envelope.

>Note: When modernized infrastructure is implemented, it will draw on a new shipping envelope that will replace VANSEnvelope, so this document will by that time be updated with the new envelope format. For a transitional period, both VANSEnvelope and the new envelope will be used, but there will be clear clarifications of how this will take place.

---

## Shipping envelopes

### VANSEnvelope

In relation to MedCom's new FHIR messages, VANSEnvelope contains 3 elements (fields) which are influenced by FHIR as a new message type. These are contained in the following parent element "VANSEnvelope/Message/MetaInformation/Document/".

The elements contained are:

* Format
* Name
* Version

MedCom's FHIR messages **SHALL** be handled like all other messages in VANSEnvelope by  base64-encoding the message in the element "VANSEnvelope/Message/Data/"

In the Transport element, "VANSEnvelope/Message/MetaInformation/Transport", the "TransformMessage" element is handled as usual, while "ServiceTag" with the attribute name = "MCM:MIME" **SHALL** be specified with one of the following values:

* application/fhir+xml
* application/fhir+json

depending on the format the FHIR message is formatted.

---

#### Format

Format **SHALL** be the same as "Standard type" in MedCom's Standards Directory and **SHALL** be defined for all FHIR standards as "HL7".

---

#### Name

Name **SHALL** be the same as "Type nr." in MedCom's Standards Directory and will thus vary from message type to message type. Name **SHALL** be prefixed with MCM: and will otherwise be able to be postfixed with statistical variants of a given message type. Known from GGOP, this outcome space can e.g. be GGOP1, GGOP2 and GGOP3. Similar constructions will occur as long as FHIR messages are transported in the VANSEnvelope.

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
|**Envelope Sender**    |VANSEnvelope                           |
|**Envelope Receiver**  |VANSEnvelope                           |
|**Format**             |"HL7"                                  |
|**Name**               |"MCM:FDIS91#`<postfix value>`"         |
|**Version**            |"2.0.0"                                |

Name **MUST** explicitly be taken from the following ValueSet: [CodeSystem-medcom-messaging-sorEdiSystem](https://build.fhir.org/ig/hl7dk/dk-medcom/CodeSystem-medcom-messaging-sorEdiSystem.html)

Postfix Values for Name **MUST** be within this ValueSet, which is taken from: [CareCommunications ValueSet for categories](https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-careCommunication-categories.html)

The combined Name+Postfix **MUST** explicitly conform with the following ValueSet: [https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html](https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html)

---

### HospitalNotification

|||
|:---|:---|
|**Envelope Sender**    |VANSEnvelope (EPJ)                      |
|**Envelope Receiver**  |KOMBIT's BeskedFordeler Envelope (EOJ og andre kommunale systemer)  |
|**Format**             |"HL7"                                   |
|**Name**               |"MCM:FDIS20#`<postfix value>`"          |
|**Version**            |"2.0.0"                                 |

Name **MUST** explicitly be taken from the following ValueSet: [CodeSystem-medcom-messaging-sorEdiSystem](https://build.fhir.org/ig/hl7dk/dk-medcom/CodeSystem-medcom-messaging-sorEdiSystem.html)

Postfix Values for Name **MUST** be within this ValueSet, which is taken from the HospitalNotification ValueSet: MedCom Hospital Notification Message Activity Codes:  [https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-hospitalNotification-messageActivities.html](https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-hospitalNotification-messageActivities.html)

The combined Name+Postfix **MUST** explicitly conform with the following ValueSet: [https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html](https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html)

---

### Acknowledgement

|||
|:---|:---|
|**Envelope Sender**    |VANSEnvelope                           |
|**Envelope Receiver**  |VANSEnvelope                           |
|**Format**             |"HL7"                                  |
|**Name**               |"MCM:FCTL1#`<postfix value>`"          |
|**Version**            |"2.0.0"                                |

Name **MUST** explicitly be taken from the following ValueSet: [https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html](https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html)

Postfix Values for Name **MUST** be within this ValueSet, which is taken from the Response Code ValueSet: Codes:  [http://hl7.org/fhir/R4/valueset-response-code.html](http://hl7.org/fhir/R4/valueset-response-code.html)

The combined Name+Postfix **MUST** explicitly conform with the following ValueSet: [https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html](https://build.fhir.org/ig/hl7dk/dk-medcom/ValueSet-medcom-messaging-vansStatisticalCodeCombinations.html)
