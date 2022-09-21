# 3. Governance for Network Layer

## Table of contents

* [3. Governance for Network Layer](#3-governance-for-network-layer)
* [3.1 VANSEnvelope](#31-vansenvelope)
* [3.2 Reliable Messaging using VANSenvelope](#32-reliable-messaging-using-vansenvelope)

The Danish Healthcare Messaging Network is currently the VANS Network on which the overall shipment of a message is handled through Asynchronous Messaging.

To be able to communicate over the VANS Network, both senders and receivers **SHALL** have a GLN number issued by the SOR. <a href="https://sundhedsdatastyrelsen.dk/da/rammer-og-retningslinjer/organisationsregistrering" target="_blank">Link for SOR (Danish)</a>

To be able to communicate a specific MedCom FHIR message type both senders and receivers **SHALL** be registered in SOR with that messagetype and version.

The Sending EcoSystem **SHALL** validate the message before dispatching it. Validating a message **SHALL** include validating the correct use of the ValueSets and Coding Systems used in the message.

The Sending EcoSystem **SHALL** validate the message before dispatching it. Validating a message **SHALL** include validating the correct use of the ValueSets and Coding Systems used in the message.

## 3.1 VANSEnvelope

The VANSenvelope is developed to contain XML-based or other non-edifact message types over the VANS Network

MedCom FHIR Messages **SHALL** be enveloped in a VANSenvelope whether they are shipped as "application/fhir+xml" or "application/fhir+json"

* The enveloping of MedCom FHIR Messages **SHALL** follow the VANS ENVELOPE specification outlined in
  * <a href="https://svn.medcom.dk/svn/releases/Standarder/Den%20gode%20VANSEnvelope/Dokumentation/Den%20gode%20VANSEnvelope.pdf" target="_blank">VANS ENVELOPE specification (Danish)</a>
* MedCom FHIR Messages **SHALL** follow the metadata specification outlined in
  * [Network Envelope (Danish)](FHIRMessages_NetworkEnvelopes_DA.md)
  * [Network Envelope (English)](FHIRMessages_NetworkEnvelopes_EN.md)

## 3.2 Reliable Messaging using VANSenvelope

VANSenvelope is developed to support Reliable Messaging.
VANSenvelope containing FHIR Messages **SHALL** make use of this Reliable Messaging functionality.

* The use of Reliable Messaging functionality when shipping MedCom FHIR Messages **SHALL** follow the VANS ENVELOPE specification outlined in
  * <a href="https://svn.medcom.dk/svn/releases/Standarder/Den%20gode%20VANSEnvelope/Dokumentation/Den%20gode%20VANSEnvelope.pdf" target="_blank">VANS ENVELOPE specification (Danish)</a>

[Tap here to see how to setup Reliable Messaging using VANSEnvelope](032_Reliable_Messaging-VANSEnvelope.md)
