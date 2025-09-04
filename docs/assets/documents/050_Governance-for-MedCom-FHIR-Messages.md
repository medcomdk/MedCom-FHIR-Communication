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

The MedComMessageHeader profile is a resource that **SHALL** be used in all MedCom FHIR Messages. A MedComMessagingMessageHeader **SHALL** include a sender and receiver and it **MAY** include a carbon-copy receiver, however this is depended on type of standard. Each MedComMessagingMessageHeader **SHALL** include a globally unique id, which **SHALL** be used to reference the message in the message history from the MedComMessagingProvenance profile.

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

A MedComMessagingOrganization **MAY** include more identifiers. These Identifiers ****SHOULD** NOT** be expected to introduce application logic for the receiver(s) of the FHIRMessage.

#### 3.2 MedComMessagingOrganization Links

| Links for MedComMessagingOrganization|
|:---|
| <a href="https://medcomdk.github.io/dk-medcom-messaging/#14-medcommessagingorganization" target="_blank">MedComMessagingOrganization in MedCom Message</a> |
| <a href="https://medcomfhir.dk/ig/messaging/StructureDefinition-medcom-messaging-organization.html" target="_blank"> Detailed specification for MedComMessagingOrganization in MedComMessagingMessage IG</a> |
| <a href="http://hl7.org/fhir/R4/Organization.html" target="_blank">Detailed specification for Organization in FHIR R4</a> |

<br>

### 4 MedComMessagingProvenance
The Provenance resource tracks information about the activity what was created, revised, or deleted, while referencing the current message and previous messages if such exist. To identify the actual content of the message and time of activity, it is important to look in the resources carrying the clinical content, such as the Encounter for the HosptialNotification standard, and the Communication for the CareCommunication standard.

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

Labeling an element MustSupport means that implementations that produce or consume resources **SHALL** provide "support" for the element in some meaningful way, and is therefore a part of a standard. Because the base FHIR specification is intended to be independent of any particular implementation context, no elements are flagged as mustSupport=true as part of the base specification. This flag is intended for use in profiles that have a defined implementation context.

<br>

#### 5.1 MustSupport Rules

In MedCom FHIR Messaging MustSupport requires that a system provides "support" for the element in some meaningful way. A meaningful way depends on the type of information, which will be expressed for each standard.

**For technical profiles**

Systems receiving or consuming a resource instance:

**MUST** be able to process the field’s content when it is present
**MUST** process the content according to the rules defined for the profile
**MUST NOT** fail when the value is not present.

Systems sending or creating a resource instance

**SHOULD** populate the element when the information is available
**MUST** populate the element according to the rules defined for the profile

For Logical Models
Functional Analysis **MUST** consider the data element as defined

“Must Support” elements that are used in an implementation **MUST** inherit the behaviour and constraints defined for the data element
“Must Support” elements not needed in a particular implementation MAY be excluded from implementation but such exclusion **MUST** be described
Derived implementations **SHOULD** inherit the field’s “Must Support” flag

#### 5.2 MustSupport Links

| Links for MustSupport|
|:---|
| <a href="https://www.hl7.org/FHIR/conformance-rules.html#mustSupport" target="_blank">Detailed specification for MustSupport in FHIR R4</a> |

<br>

### 6 Narrative Texts

#### 6.1 The Importance of Narrative Text in MedCom’s FHIR Standards
In MedCom’s FHIR standards, it is required that all FHIR resources include a narrative text. The narrative serves an essential purpose: It ensures that the clinical or administrative content of the resource can be understood by healthcare professionals without the need for specialized technical tools. While the structured elements of a FHIR resource are designed for system-to-system communication, the narrative provides a human-readable summary that makes the information accessible to human interpreation in a simple XHTML view.

The narrative text plays a critical role in supporting robustness and patient safety across the healthcare system. First, it allows the content of a message to be read even if the recipient system fails to process the structured data. For example. Second, when narrative text is displayed across multiple versions of a standard, it increases patient safety by ensuring that as much information as possible remains visible, and it enables healthcare professionals to review historical messages in the future. Third, it makes it additional elements beyond those defined in the MedCom standard transparent, since FHIR allows resources to include more data than the standard strictly requires. Fourth, including a narrative is considered best practice in FHIR and aligns MedCom’s work with international recommendations. Finally, the presence of a narrative ensures that even if a system receives a FHIR Bundle it is not fully equipped to handle, the content can still be displayed and understood when necessary.

#### 6.2 Requirements for the Narratives

The narrative text **SHALL** include a human-readable representation of every data element marked with the Obligation code **SHALL:in-narrative**.

Obligations in FHIR define actor-specific requirements in an Implementation Guide to express conformance expectations. The code “SHALL:in-narrative” indicates that the referenced data element must be represented in the human-readable narrative of the resource. An Actor represents a defined role in an exchange, and obligations are applied to actors to indicate their specific responsibilities. The narrative **SHALL** provide a human-readable summary of the essential elements and **SHALL NOT** replicate the full structured content.

All MedCom FHIR ressources **SHALL** include a narrative in the `[resource].text`-element (even though it is not marked with 1..1 cardinality in the Implementation Guide), except the Bundle resources. Since the Bundle itself does not carry clinical meaning, its content must be understood by reviewing the individual resources inside the Bundle.

Narratives contain two sub elements, text.status and text.div.

##### 6.2.1 The status element

In MedCom FHIR ressources the text.status elemen **SHALL** always use the code "generated" or "extension". The status "generated" **SHALL** be used when the resource contains only standard, generated content. The status "extension" **SHALL** be used when the resource includes additional elements provided through extensions.

A narrative in MedCom FHIR resources **SHALL NEVER** be of code: empty.

##### 6.2.2 The div element

The contents of the text.div element are XHTML fragments that **SHALL** contain only the basic HTML formatting elements described in chapters 7-11 (except section 4 of chapter 9) and 15 of the HTML 4.0 standard, '<a>' elements (either name or href), images and internally contained style attributes.

The XHTML content **SHALL NOT** contain a head, a body element, external stylesheet references, deprecated elements, scripts, forms, base/link/xlink, frames, iframes, objects or event related attributes (e.g. onClick). 

If a resource includes a base-64-encoded attachment, this **SHALL NOT** be included in the narrative text, as it will cause the size of the message to increase rapidly.

##### 6.2.3 General Narrative Text Rules

* All resources **SHALL** contain a narrative text defined by the `[resource].text` element (Except Bundles).
* The Narrative Text **SHALL** have a status with value "generated" or "extensions". 
* The Narrative Text **SHALL** include elements marked with the Obligation code **SHALL:in-narrative**. 
* The Narrative Text **SHALL NOT** include base-64-encoded attachments.
* If a resource contains extra information beyond the MedCom standard, this **SHALL** be included in the narrative.
* The narrative **SHALL** use Danish clinical terminology or recognized Danish display texts where such exist, and it **SHALL** also include the corresponding English text to ensure international readability.

#### 6.3 Governance for narrative content in MedCom FHIR standards

This governance is applied by MedCom to define which elements **SHALL** be included in the narrative and assigned the Obligation code **SHALL:in-narrative** found in the MedCom FHIR standard profiles. The purpose of this governance is to ensure a consistent use of narrative texts across MedCom’s FHIR profiles. The governance defines which types of elements that **SHALL** be included in the human-readable narrative and which should be excluded, based on best practice and patient safety considerations. The same type of element **SHOULD** always be treated consistently across MedCom profiles to support predictable implementation.

##### 6.3.1 Elements that must be included in the narrative text

Clinically and administratively relevant information (CARI), including diagnoses, observations, procedures, and other content directly relevant to patient care or administration **SHALL** be included in the narrative text.

Clinically and administratively relevant information includes:

* Elements representing relevant person and organization information (e.g., Patient, Practitioner, Organization), including e.g. name, role, CPR-number, birthdate, and contact information.
* Codes and corresponding systems with human meaning. When coded values are used (e.g., LOINC, SNOMED CT, MedCom codes), their display text (the human-readable term) must appear in the narrative.
* Relevant values (e.g., observation results, medication names and dosages, diagnostic conclusions).
* Relevant elements from extension.
* Identifiers (e.g., SOR-ID, municipality codes, episode-of-care identifiers) when they have human relevance.
* Relevant dates and times.

##### 6.3.2 Elements that shall not be included in the narrative text

* Technical identifiers.
* System-generated IDs (UUIDs, database keys, OIDs).
* References and resource links.
* FHIR references (e.g., Patient/123) should not be rendered in the narrative; instead, their human-readable display (e.g., patient name) must be shown.
* Metadata.
* Elements such as meta, versionId, lastUpdated, or technical extensions not meaningful for end users.
* Extensions without direct clinical relevance.

#### 6.4 Links for Narrative Text

|Additional information can be found in the following links for narrative texts in FHIR|
|:---|
|<a href="http://hl7.org/fhir/R4/narrative.html#Narrative" target ="_blank">Narrative Text description in FHIR R4</a>|
|<a href="http://hl7.org/fhir/R4/codesystem-narrative-status.html#4.3.14.424.2" target="_blank">NarrativeStatus in FHIR R4</a>|
|<a href ="http://hl7.org/fhir/R4/narrative.html#css" target="_blank">Styling the XHTML in FHIR R4</a>|
