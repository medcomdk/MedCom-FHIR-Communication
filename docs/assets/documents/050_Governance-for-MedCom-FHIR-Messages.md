# Governance for MedCom FHIR Messages

**Table of content**
* [1. MedComMessagingMessage-bundle](#1-medcommessagingmessage-bundle)
    * [1.1 MedComMessagingMessage Rules](#11-medcommessagingmessage-rules)
    * [1.2 MedComMessagingMessage Links](#12-medcommessagingmessage-links)
* [2 MedComMessagingMessageHeader](#2-medcommessagingmessageheader)
    * [ 2.1 MedComMessagingMessageHeader Rules](#21-medcommessagingmessageheader-rules)
    * [2.2 Identifiers and Timestamps](#22-identifiers-and-timestamps)
* [3 MedComMessagingOrganization](#3-medcommessagingorganization)
    * [3.1 MedComMessagingOrganization Rules](#31-medcommessagingorganization-rules)
    * [3.2 MedComMessagingOrganization Links](#32-medcommessagingorganization-links)
* [4 MedComMessagingProvenance](#4-medcommessagingprovenance)
    * [4.1 MedComMessagingProvenance Rules](#41-medcommessagingprovenance-rules)
    * [4.2 MedComMessagingProvenance Links](#42-medcommessagingprovenance-links)
* [5 MustSupport](#5-mustsupport)
    * [5.1 MustSupport rules](#51-mustsupport-rules)
    * [5.2 MustSupport links](#52-mustsupport-links)
* [6 Narrative texts](#6-narrative-texts)
    * [6.1 The status element](#61-the-status-element)
    * [6.2 The div element](#62-the-div-element)
    * [6.3 General narrative text rules](#63-general-narrative-text-rules)
    * [6.4 Links for narrative text](#64-links-for-narrative-text)


## 1 MedComMessagingMessage (Bundle)

An inherited instance profile of MedComMessagingMessage **SHALL** follow the generic concept of the MedComMessagingMessage as outlined here:
[Click here to read more about the MedComMessagingMessage (Bundle) in IG for MedCom Message](https://medcomdk.github.io/dk-medcom-messaging/assets/documents/Intro-Technical-Spec-ENG.html#21-medcommessagingmessage-bundle)

### 1.1 MedComMessagingMessage Rules

| MedComMessagingMessage Rules|
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

### 1.2 MedComMessagingMessage Links

| Links for MedComMessagingMessage|
|:---|
| <a href="https://medcomfhir.dk/ig/messaging//StructureDefinition-medcom-messaging-message.html" target="_blank"> Click here to read a detailed specification for MedComMessagingMessage in MedComMessagingMessage IG</a> |
| <a href="https://medcomdk.github.io/dk-medcom-messaging/" target="_blank">Click here to read a detailed page for MedCom Messaging</a> |
| <a href="http://hl7.org/fhir/R4/Bundle.html" target="_blank">Click here to read a detailed specification for Bundle in FHIR R4</a> |

### 2 MedComMessagingMessageHeader

An inherited instance profile of MedComMessagingMessageHeader **SHALL** follow the generic concept of the MedComMessagingMessageHeader as outlined here:
[Click here to read more about MedComMessagingMessageHeader in IG for MedCom Message](https://medcomdk.github.io/dk-medcom-messaging/#13-medcommessagingmessageheader)

| Links for MedComMessagingMessageHeader|
|:---|
| <a href="https://medcomdk.github.io/dk-medcom-messaging/assets/documents/Intro-Technical-Spec-ENG.html#22-medcommessagingmessageheader" target="_blank">MedComMessagingMessageHeader in MedCom Message</a> |
| <a href="https://medcomfhir.dk/ig/messaging//StructureDefinition-medcom-messaging-messageHeader.html" target="_blank"> Detailed specification for MedComMessageHeader in MedComMessagingMessage IG</a> |
| <a href="http://hl7.org/fhir/R4/MessageHeader.html" target="_blank">Detailed specification for MessageHeader in FHIR R4</a> |

<br>

#### 2.1 MedComMessagingMessageHeader Rules

The MedComMessageHeader profile is a resource that **SHALL** be used in all MedCom FHIR Messages. A MedComMessagingMessageHeader **SHALL** include a sender and receiver and it **may** include a carbon-copy receiver, however this is depended on type of standard. Each MedComMessagingMessageHeader **SHALL** include a globally unique id, which **SHALL** be used to reference the message in the message history from the MedComMessagingProvenance profile.

The element event **SHALL** be defined in accordance with the type of standard the message concerns e.g., HospitalNotification and CareCommunication. Due to the different requirements for each standard, it **SHALL** be expected that the MedComMessagingMessageHeader is inherited in each standard.

| MedComMessageHeader Rules|
|:---|
| The MedComMessagingHeader resource **SHALL** be the first resource in a MedCom Message Bundle |
| The MedComMessagingHeader resource **SHALL** contain an event of the MedCom Message (eg. the type of the message) |
| The MedComMessagingHeader resource **SHALL** contain an MedComMessagingHeader.id of the MedCom Message (eg. the letter.id of the message) |
| One of the two bundled MedComMessagingOrganization resources **SHALL** represent the Sender Organization pointed to by the MedComMessagingHeader.sender element |
| One of the two bundled MedComMessagingOrganization resources **SHALL** represent the Receiver Organization pointed to by the MedComMessagingHeader.destination:primary sliced element |
| The MedComMessagingHeader resource **MAY** include a list of carbon-copy receiver organizations pointed to by the MedComMessagingHeader.destination:cc sliced element(s) |
| MedCom FHIR Messages **SHALL** contain one bundled focused resource pointed to by the MedComMessagingHeader pointed to by the MedComMessagingHeader.focus element |

#### 2.2 Identifiers and Timestamps

[Click here to go to Governance for Identifiers](052.2_MessageHeader_Identifiers_Timestamps.md)

### 3 MedComMessagingOrganization

An inherited instance profile of MedComMessagingOrganization **SHALL** follow the generic concept of the MedComMessagingOrganization as outlined here:
[MedComMessagingOrganization in MedCom Message](https://medcomdk.github.io/dk-medcom-messaging/assets/documents/Intro-Technical-Spec-ENG.html#23-medcommessagingorganization)

This profile describes the Organization resource that **SHALL** be used in all MedCom FHIR Messages. MedComMessagingOrganization inherits from MedComCoreOrganization as it **SHALL** include both a SOR and an EAN/GLN identifier. MedComMessagingOrganization **SHALL** be used to describe the sender and receiver organizations of all MedCom FHIR Messages.

<br>

#### 3.1 MedComMessagingOrganization Rules

A MedComMessagingOrganization that is referenced as a "primary" receiver **SHALL** never be used also to reference a "cc-receiver" in the same FHIRMessage.

A MedComMessagingOrganization that is referenced as either a "primary" receiver or a "cc-receiver" **MAY** be used to reference organization entities used otherwhere in a FHIRMessage.

A MedComMessagingOrganization **SHALL** include both a SOR and an EAN/GLN identifier.

A MedComMessagingOrganization **MAY** include more identifiers. These Identifiers **SHOULD NOT** be expected to introduce application logic for the receiver(s) of the FHIRMessage.

#### 3.2 MedComMessagingOrganization Links

| Links for MedComMessagingOrganization|
|:---|
| <a href="https://medcomdk.github.io/dk-medcom-messaging/#14-medcommessagingorganization" target="_blank">MedComMessagingOrganization in MedCom Message</a> |
| <a href="https://medcomfhir.dk/ig/messaging/StructureDefinition-medcom-messaging-organization.html" target="_blank"> Detailed specification for MedComMessagingOrganization in MedComMessagingMessage IG</a> |
| <a href="http://hl7.org/fhir/R4/Organization.html" target="_blank">Detailed specification for Organization in FHIR R4</a> |

<br>

### 4 MedComMessagingProvenance

#### 4.1 MedComMessagingProvenance Rules

* MedCom FHIR Messages **SHALL** contain at least one bundled MedComMessagingProvenance resource
* MedCom FHIR Messages **SHALL** contain one bundled MedComMessagingProvenance resource for each message exchange the message has been involved in
* MedCom FHIR Messages **SHALL** contain no more than two bundled MedComMessagingProvenance resource when acknowledging a message

#### 4.2 MedComMessagingProvenance Links

| Links for MedComMessagingProvenance|
|:---|
| <a href="https://medcomdk.github.io/dk-medcom-messaging/#15-medcommessagingprovenance" target="_blank">MedComMessagingProvenance in MedCom Messaging</a> |
| <a href="https://medcomfhir.dk/ig/messaging/StructureDefinition-medcom-messaging-provenance.html" target="_blank"> Detailed specification for MedComMessagingProvenance in MedComMessagingMessage IG</a> |
| <a href="http://hl7.org/fhir/R4/Provenance.html" target="_blank">Detailed specification for Provenance in FHIR R4</a> |

<br>

### 5 MustSupport

Unless otherwise stated, the following criteria apply to elements marked as “Must Support” in MedCom's Implementation Guides:

Labeling an element MustSupport means that implementations that produce or consume resources **SHALL** provide "support" for the element in some meaningful way. Because the base FHIR specification is intended to be independent of any particular implementation context, no elements are flagged as mustSupport=true as part of the base specification. This flag is intended for use in profiles that have a defined implementation context.

<br>

#### 5.1 MustSupport Rules

In MedCom FHIR Messaging MustSupport requires that a system

Systems supporting the profile **MUST NOT** ignore the field.

**For technical profiles**

Systems receiving or consuming a resource instance:

**MUST** be able to process the field’s content when it is present
**MUST** process the content according to the rules defined for the profile
**MUST NOT** fail when the value is not present.

Systems sending or creating a resource instance

**SHOULD** populate the element when the information is available
**MUST** populate the element according to the rules defined for the profile

For Logical Models
Functional Analysis MUST consider the data element as defined

“Must Support” elements that are used in an implementation MUST inherit the behaviour and constraints defined for the data element
“Must Support” elements not needed in a particular implementation MAY be excluded from implementation but such exclusion MUST be described
Derived implementations SHOULD inherit the field’s “Must Support” flag

#### 5.2 MustSupport Links

| Links for MustSupport|
|:---|
| <a href="https://www.hl7.org/FHIR/conformance-rules.html#mustSupport" target="_blank">Detailed specification for MustSupport in FHIR R4</a> |

<br>

### 6 Narrative Texts

The narrative text **SHALL** encode all the structured data pointed out by the ∑-symbol and it **SHALL** contain sufficient detail to make it "clinically safe" for a human to just read the narrative.
Contained resources do not have narrative, but their content **SHALL** be represented in the ressource container.

Narratives contains two sub elements, status and div.

#### 6.1 The status element

In MedCom FHIR Messages The code **SHALL** always be: "additional" meaning that the it is covering the code: extension and allowing for more human readable text in the div element than is produced by: generated and extension.

A narrative in MedCom FHIR Messages **SHALL NEVER** be of code: empty.

#### 6.2 The div element

The contents of the div element are XHTML fragments that **SHALL** contain only the basic HTML formatting elements described in chapters 7-11 (except section 4 of chapter 9) and 15 of the HTML 4.0 standard, '<a>' elements (either name or href), images and internally contained style attributes.

The XHTML content **SHALL NOT** contain a head, a body element, external stylesheet references, deprecated elements, scripts, forms, base/link/xlink, frames, iframes, objects or event related attributes (e.g. onClick). 

The div element **SHALL** have some non-whitespace content (text or an image).

#### 6.3 General Narrative Text Rules

* All resources in a MedComMessagingMessage **SHALL** contain a Narrative Text defined by the [resource].Text element
* The Narrative Text **SHALL** have a status with value "extensions". Extensions means that the contents of the narrative are entirely generated from the core elements in the content and some of the content is generated from extensions.
* The narrative **SHALL** reflect the impact of all modifier extensions.

#### 6.4 Links for Narrative Text

| Links for Narrative Text|
|:---|
|<a href="http://hl7.org/fhir/R4/narrative.html#Narrative" target ="_blank">Narrative Text description in FHIR R4</a>|
|<a href="http://hl7.org/fhir/R4/codesystem-narrative-status.html#4.3.14.424.2" target="_blank">NarrativeStatus in FHIR R4</a>|
|<a href ="http://hl7.org/fhir/R4/narrative.html#css" target="_blank">Styling the XHTML in FHIR R4</a>|
