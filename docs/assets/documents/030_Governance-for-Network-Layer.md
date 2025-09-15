# Governance for Network Layer

**Table of contents**

* [1 VANSEnvelope](#1-vansenvelope)
* [2 Reliable Messaging using VANSEnvelope](#2-reliable-messaging-using-vansenvelope)
* [3 Sending MedCom FHIR messages in VANSEnvelope](#3-sending-medcom-fhir-messages)
* [4 Receiving MedCom FHIR messages in VANSEnvelope](#4-receiving-medcom-fhir-messages)

<br>

The Danish Healthcare Messaging Network is currently the VANS Network on which the overall shipment of a message is handled through Asynchronous Messaging.

To be able to communicate over the VANS Network, both senders and receivers **SHALL** have a GLN number issued by the SOR. <a href="https://sundhedsdatastyrelsen.dk/da/rammer-og-retningslinjer/organisationsregistrering" target="_blank">Click here to open SOR </a>. The SOR is developed by The Danish Health Data Authority and therefore the information in SOR are in Danish.

To be able to communicate a specific MedCom FHIR message type both senders and receivers **SHALL** be registered in SOR with that message type and version.

The Sending Ecosystem **SHALL** validate the message before dispatching it. Validating a message **SHALL** include validating the correct use of the ValueSets and CodeSystems used in the message.

## 1 VANSEnvelope

The VANSEnvelope is developed to contain XML-based or other non-edifact message types over the VANS Network

MedCom FHIR Messages **SHALL** be enveloped in a VANSEnvelope whether they are shipped as "application/fhir+xml" or "application/fhir+json"

* The envelopment of MedCom FHIR Messages **SHALL** follow the VANSEnvelope specification outlined in
  * <a href="https://svn.medcom.dk/svn/releases/Standarder/Den%20gode%20VANSEnvelope/Dokumentation" target="_blank"> Click here to read VANSEnvelope specification</a>. Please be aware that the VANSEnvelope specification is in Danish.
* MedCom FHIR Messages **SHALL** follow the metadata specification outlined in both Danish and English:
  * [English:Network Envelope](FHIRMessages_NetworkEnvelopes_EN.md)
* VANSEnvelopes **SHALL** only contain one MedCom FHIR Message.

## 2 Reliable Messaging using VANSEnvelope

VANSEnvelope is developed to support Reliable Messaging.

VANSEnvelope containing FHIR Messages **SHALL** make use of this Reliable Messaging functionality.

* The use of Reliable Messaging functionality when shipping MedCom FHIR Messages **SHALL** follow the VANSEnvelope specification outlined in
  * <a href="https://svn.medcom.dk/svn/releases/Standarder/Den%20gode%20VANSEnvelope/Dokumentation" target="_blank"> Click here to read VANSEnvelope specification</a>. Please be aware that the VANSEnvelope specification is in Danish.

[Click here to see how to set up Reliable Messaging using VANSEnvelope](032_Reliable_Messaging-VANSEnvelope.md)

## 3 Sending MedCom FHIR messages

Sending MedCom FHIR messages over the VANS Network requires the sending system to handle the following:

When sending to both primary and cc destinations.

1. A Sending Ecosystem **MUST** secure that the MedCom FHIR messages for primary and cc receivers differ on ID's as described in [Governance for MedCom FHIR Messaging](040_Governance4FHIR-Messaging.md)
2. A Sending Ecosystem MUST ensure that the total size of a MedCom FHIR message, once embedded in a VANSEnvelope, does not exceed 100 MB when sent on the VANS Network. If the size is validated before the message is embedded in a VANSEnvelope, the Sending Ecosystem MAY apply a slightly lower limit to reserve space for the VANSEnvelope overhead and thereby ensure compliance with the 100 MB maximum.

## 4 Receiving MedCom FHIR messages

A Receiving Ecosystem **SHALL** be able to receive MedCom FHIR messages both as "application/fhir+xml" and "application/fhir+json"

A Receiving Ecosystem **SHALL** be able to handle both primary and cc destinations and route them to the right application.
