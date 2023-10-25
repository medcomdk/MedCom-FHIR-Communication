# Governance for MedCom HospitalNotification

* [1 Exchange of HospitalNotification message](#1-exchange-of-hospitalnotification-message)
  * [1.2 VANS-network and Municipality Message Publisher](#12-vans-network-and-municipality-message-publisher)
    * [1.2.1 Type A](#121-type-a)
    * [1.2.2 Type B](#122-type-b)
    * [1.2.3 Type C](#123-type-c)
  * [1.3 Acknowledgements](#13-acknowledgements)
  * [1.4 Envelopes](#14-envelopes)
* [2 HospitalNotification message](#2-hospitalnotification-message)
  * [2.1 MedComHospitalNotificationMessage profile](#21-medcomhospitalnotificationmessage-profile)
  * [2.2 MedComHospitalNotificationEncounter profile](#22-medcomhospitalnotificationencounter-profile)
  * [2.3 MedComMessagingProvenance profile](#23-medcommessagingprovenance)
<br><br>

## 1 Exchange of HospitalNotification message 

The flow of events of a HospitalNotification message differs from the regular message exchange over the VANS-network, as it is exchanged over both the VANS-network and the Municipalities Message Publisher (Danish: KOMBIT Beskedfordeler). Questions regarding the Municipalities Message Publisher, and its envelope, called Beskedfordeler-envelope, should be addressed to KOMBIT. 


### 1.2 VANS-network and Municipality Message Publisher
The following sections describe the flow of a HospitalNotification message. There are three types of receiving systems that can receive a HospitalNotification: Type A, B and C. Since there is different requirements to acknowledging a HospitalNotification, they are presented seperately. 

The flow of events and rules, when sending and receiving a HospitalNotification, are common for all the systems. However, a type C system shall not acknowledge a HospitalNotification.

|Rules describing the flow of events when sending, and acknowledging a HospitalNotification message|
|:---|
|A Sending EcoSystem **SHALL** wrap a HospitalNotification in a VANS-envelope|
|The Municipality Message Publisher **SHALL** unwrap a HospitalNotification in a VANS-envelope|
|The Municipality Message Publisher **SHALL** wrap a HospitalNotification in a Beskedfordeler-envelope|
|A Receiving EcoSystem **SHALL** unwrap a HospitalNotification in a Beskedfordeler-envelope|
|A Receiving EcoSystem **SHALL** wrap an Acknowledgement in a Beskedfordeler-envelope|
|The Municipality Message Publisher **SHALL** unwrap an Acknowledgement in a Beskedfordeler-envelope|
|The Municipality Message Publisher **SHALL** wrap an Acknowledgement in a VANS-envelope|
|A Sending EcoSystem **SHALL** unwrap a received Acknowledgement in a VANS-envelope|


#### 1.2.1 Type A
A Type A system is, according to KOMBIT, a receiving system that shall receive and acknowledge. The acknowledgement of a Type A system is the basis for the Municipality Message Publisher to sent an Acknowledgement to the sending system. 

#### 1.2.2 Type B
A Type B system is according to KOMBIT a receiving system that shall receive and acknowledge. The acknowledgement of a Type B system isn't the basis for the Municipality Message Publisher to sent an Acknowledgement to the sending system. It will, though, be the basis of an internal root cause investigation.

#### 1.2.3 Type C
A Type C system is according to KOMBIT a receiving system that is able to receive a HospitalNotification, but not to acknowledge it.

### 1.3 Acknowledgements

All MedCom FHIR messages **SHALL** be acknowledged, which is also valid for a HospitalNotification message. To acknowledge a HospitalNotification message the [MedCom FHIR Acknowledgement](https://medcomdk.github.io/dk-medcom-acknowledgement/) standard **SHALL** be used.

### 1.4 Envelopes

When the HospitalNotification message is sent over the VANS-network, it **SHALL** be wrapped in a VANS-envelope [This page describes the use of VANS-envelope](/docs/assets/documents/030_Governance-for-Network-Layer.md)

Values of fields used in a VANSenvelope **SHALL** obey to the [specifications described on the page for VANSenvelope](https://medcomdk.github.io/MedCom-FHIR-Communication/assets/documents/FHIRMessages_NetworkEnvelopes_EN.html#32-hospitalnotification) for a HospitalNotification message.

When the HospitalNotification message is sent over Municipality Message Publisher, it **SHALL** be in a beskedfordelerkuvert. [More information can be found on](kombit.dk)

## 2 HospitalNotification message

HospitalNotification follows [MedComs generic messaging model](https://medcomdk.github.io/dk-medcom-messaging/assets/documents/Intro-Technical-Spec-ENG.html#21-medcommessagingmessage-bundle), which is described on the GitHub pages for the messaging IG. To embrace the business requirements, the HospitalNotification standard expands the generic messaging model by including more profiles and rules. The structure and included profiles can be seen on <a href="#Fig2">Figure 2</a>. The rules can be found below the figure. 

<figure style="margin-left: 0px; margin-right: 0px; width: 100%;">
<a href="../images/HospitalNotification.svg" target="_blank"> <img src="../images/HospitalNotification.svg" alt="The structure and included profiles in HospitalNotification" style="width:auto; margin-left:0px; margin-right:0px;" id="Fig2"></a>
<figcaption text-align="left"><b>Figure 2: The structure and included profiles in HospitalNotification</b></figcaption>
</figure>
<br>

### 2.1 MedComHospitalNotificationMessage profile

|Rule name|Rules used to constrain the possibilities in a MedComHospitalNotificationMessage profile|
|:---|:---|
|medcom-hospitalNotification-1 | The MessageHeader **SHALL** conform to MedComHospitalNotificationMessageHeader |
|medcom-hospitalNotification-2 | Entry **SHALL** contain exactly one patient resource |
|medcom-hospitalNotification-3 | All Provenance resources **SHALL** contain activities from medcom-hospitalNotification-messageActivities ValueSet |
|medcom-hospitalNotification-4 | The system of Patient.identifier **SHALL** be 'urn:oid:1.2.208.176.1.2', which represents an official Danish CPR-number |
|medcom-hospitalNotification-5 | The receiver of a HospitalNotification **SHALL** be a primary receiver. |

<br>

### 2.2 MedComHospitalNotificationEncounter profile

One episodeOfCare-identifier **SHALL** be included. More information about the <a href="https://medcomfhir.dk/ig/hospitalnotification/StructureDefinition-medcom-hospitalNotification-encounter.html" target="_blank">use and expectations for the episodeOfCare-identifier can be found in the IG for HospitalNotification</a> 

|Rule name|Rules used to constrain the possibilities in a MedComHospitalNotificationEncounter profile|
|:---|:---|
|uuidv5 | The episodeOfCare-identifier **MAY** be an LPR3-identifier, which **SHALL** be an UUID version 5. |
|medcom-hospitalNotification-6 | When the Encounter.status = onleave, the timestamp Encounter.extension:leavePeriod.start **SHALL** be present|



### 2.3 MedComMessagingProvenance

When sending an initial HospitalNotification exactly one instance of the Provenance resource **SHALL** be included. An initial HospitalNotification can be of the type STIN or STAA, as described in the [Clinical guidelines for application](https://medcomdk.github.io/dk-medcom-hospitalnotification/#11-clinical-guidelines-for-application). 

When sending any following HospitalNotification, all the previous instances of the Provenance resource describing the previous HospitalNotifications and a new instance describing the current HospitalNotification **SHALL** be included.

> Note: The lateste Provenance can be identified be comparing Provenance.occurred in across all instances or by identify Provenance.target that is equal to MessageHeader.id in the current message.

When acknowledging a HospitalNotification with an Acknowledgement, only the latest instance of the Provenance the HospitalNotification and the current instance of the Provenance describing the Acknowledgement **SHALL** be included. Therefore, an Acknowledgement will always contain two instances of Provenance resources.

All instances of the Provenance resource **SHALL** comply to the [MedComMessagingProvenance profile](https://medcomfhir.dk/ig/messaging/StructureDefinition-medcom-messaging-provenance.html).

