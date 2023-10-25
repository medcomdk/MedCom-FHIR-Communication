# MedCom FHIR Messages And Network Envelopes

**Table of contents**
* [1. Introduction](#1-introduction)
* [2. Shipping envelopes](#2-shipping-envelopes)
    * [2.1 VANSEnvelope](#21-vansenvelope)
        * [2.1.1 Format](#211-format)
        * [2.1.2 Name](#212-name)
        * [2.1.3 Version](#213-version)
* [3. MedCom FHIR message types](#3-medcom-fhir-message-types)
    * [3.1 CareCommunication](#31-carecommunication)
    * [3.2 HospitalNotification](#32-hospitalnotification)
    * [3.3 Acknowledgment](#33-acknowledgement)


## 1 Introduction

MedCom's FHIR messages will be wrapped and appear in various envelope formats during their shipping process.

At present, shipping will take place in the existing VANS network and thus with the use of VANSEnvelope unless otherwise specified under the individual standard. Reception can be both in VANSEnvelope or in another reception envelope, e.g. KOMBIT's BeskedFordeler envelope.

>Note: When modernized infrastructure is implemented, it will draw on a new shipping envelope that will replace VANSEnvelope, so this document will by that time be updated with the new envelope format. For a transitional period, both VANSEnvelope and the new envelope will be used, but there will be clear clarifications of how this will take place.


## 2 Shipping envelopes

### 2.1 VANSEnvelope

In relation to MedCom's new FHIR messages, VANSEnvelope contains 3 elements (fields) which are influenced by FHIR as a new message type. These are contained in the following parent element "VANSEnvelope/Message/MetaInformation/Document/".

The elements contained are:

* Format
* Name
* Version

MedCom's FHIR messages **SHALL** be handled like all other messages in VANSEnvelope by  base64-encoding the message in the element "VANSEnvelope/Message/Data/"

In the Transport element, "VANSEnvelope/Message/MetaInformation/Transport", the "TransformMessage" element is handled as usual, while "ServiceTag" with the attribute name = "MCM:MIME" **SHALL** be specified with one of the following values:

* application/fhir+xml
* application/fhir+json

Depending on the format the FHIR message is formatted.



#### 2.1.1 Format

Format **SHALL** be the same as "Standard type" in MedCom's Standards Directory and **SHALL** be defined for all FHIR standards as "HL7".


#### 2.1.2 Name

Name **SHALL** be the same as "Type nr." in MedCom's Standards Directory and will thus vary from message type to message type. Name **SHALL** be prefixed with MCM: and will otherwise be able to be postfixed with statistical variants of a given message type. Known from GGOP, this outcome space can e.g. be GGOP1, GGOP2 and GGOP3. Similar constructions will occur as long as FHIR messages are transported in the VANSEnvelope.



#### 2.1.3 Version

Version **MUST** be the same as "Version" in MedCom's standard directory and will thus vary from message version to message version.



## 3 MedCom FHIR message types

Specifically, the above for MedCom's FHIR messages means this



### 3.1 CareCommunication

|||
|:---|:---|
|**Envelope Sender**    |VANSEnvelope                           |
|**Envelope Receiver**  |VANSEnvelope                           |
|**Format**             |"HL7"                                  |
|**Name**               |"MCM:FDIS91#`<postfix value>`"         |
|**Version**            |"3.0.0"                                |

Name **MUST** explicitly be taken from the following ValueSet:<a href="https://medcomfhir.dk/ig/terminology/CodeSystem-medcom-messaging-sorEdiSystem.html" target="_blank">CodeSystem-medcom-messaging-sorEdiSystem</a>

Postfix Values for Name **MUST** be within this ValueSet, which is taken from:<a href=""></a> <a href ="https://medcomfhir.dk/ig/terminology/ValueSet-medcom-careCommunication-categories.html" target="_blank">CareCommunications ValueSet for categories</a>

The combined Name+Postfix **MUST** explicitly conform with the following ValueSet: <a href="https://medcomfhir.dk/ig/terminology/CodeSystem-medcom-messaging-sorEdiSystem.html" target="_blank">VansStatisticalCodeCombination</a>


### 3.2 HospitalNotification

|||
|:---|:---|
|**Envelope Sender**    |VANSEnvelope (EPJ)                      |
|**Envelope Receiver**  |KOMBIT's BeskedFordeler Envelope (EOJ og andre kommunale systemer)  |
|**Format**             |"HL7"                                   |
|**Name**               |"MCM:FDIS20#`<postfix value>`"          |
|**Version**            |"3.0.0"                                 |

Name **MUST** explicitly be taken from the following ValueSet: <a href="https://medcomfhir.dk/ig/terminology/CodeSystem-medcom-messaging-sorEdiSystem.html" target="_blank">CodeSystem-medcom-messaging-sorEdiSystem</a>

Postfix Values for Name **MUST** be within this ValueSet, which is taken from the HospitalNotification ValueSet:<a href="https://medcomfhir.dk/ig/terminology/ValueSet-medcom-hospitalNotification-messageActivities.html" target="_blank">MedComHospitalNotificationMessageActivityCodes</a> 

The combined Name+Postfix **MUST** explicitly conform with the following ValueSet:<a href="https://medcomfhir.dk/ig/terminology/CodeSystem-medcom-messaging-sorEdiSystem.html" target="_blank">VansStatisticalCodeCombination</a>


### 3.3 Acknowledgement

|||
|:---|:---|
|**Envelope Sender**    |VANSEnvelope                           |
|**Envelope Receiver**  |VANSEnvelope                           |
|**Format**             |"HL7"                                  |
|**Name**               |"MCM:FCTL1#`<postfix value>`"          |
|**Version**            |"2.0.0"                                |

Name **MUST** explicitly be taken from the following ValueSet: <a href="https://medcomfhir.dk/ig/terminology/CodeSystem-medcom-messaging-sorEdiSystem.html" target="_blank">VansStatisticalCodeCombination</a>

Postfix Values for Name **MUST** be within this ValueSet, which is taken from the Response Code ValueSet: Codes:  [http://hl7.org/fhir/R4/valueset-response-code.html](http://hl7.org/fhir/R4/valueset-response-code.html)

The combined Name+Postfix **MUST** explicitly conform with the following ValueSet: <a href="https://medcomfhir.dk/ig/terminology/CodeSystem-medcom-messaging-sorEdiSystem.html" target="_blank">VansStatisticalCodeCombination</a>