# Governance for MedCom Acknowledgement 

**Table of content**






## 1. MedComAcknowledgement message 
MedComAcknowledgement message follows the MedCom generic messaging model, except that the carbon-copy destination is not allowed. [Click here to read about the MedCom generic messaging model.](https://medcomdk.github.io/dk-medcom-messaging/assets/documents/Intro-Technical-Spec-ENG.html#21-medcommessagingmessage-bundle)  

The structure and included profiles in MedCom Acknowledgement can be seen on <a href="#fig1">Figure 1: 

<figure style="margin-left: 0px; margin-right: 0px; width: 100%;">
<a href="../images/MedComAcknowledgementMessage.svg" target="_blank"> <img src="../images/MedComAcknowledgementMessage.svg.svg" alt="The structure and included profiles in MedCom Acknowledgement" style="width:auto; margin-left:0px; margin-right:0px;" id="fig1"></a>
<figcaption text-align="left"><b>Figure 1: The structure and included profiles in MedCom Acknowledgement.</b></figcaption>
</figure>
<br>


### 1.1 MedComAcknowledgement profile 


### 1.2 MedComAcknowledgementMessageHeader 

The message header SHALL conform to medcom-messaging-acknowledgementHeader profile.
Furthermore, when acknowledging a MedComMessage a response code indicating the type of Acknowledgement SHALL be included. 
[Click here to see the response codes](https://medcomfhir.dk/ig/acknowledgement/StructureDefinition-medcom-messaging-acknowledgementHeader.html#respons-code)

#### 1.2.1 MedComAcknowledgementOperationOutcome 

[MedComAcknowledgementOperationOutcome](https://medcomfhir.dk/ig/acknowledgement/StructureDefinition-medcom-acknowledgement-operationoutcome.html) SHALL be included in the bundle when the MessageHeader.response.code is different from ‘ok’. Further, an OperationOutcome resource may be included when the MessageHeader.response.code is ‘ok’, e.g. in cases where the received message is valid, but it is a dublet.When the MessageHeader.response.code is different form ‘ok’, OperationOutcome SHALL contain a description of the error and the severity of the error.
The ValueSet MedComAcknowledgementIssueDetailValues attached to the element OperationOutcome.response.detail.coding is used to describe the issue more detailed.
MedCom has developed a ValueSet with predefined issues descriptions that can help with troubleshooting. It is recommeded to use the ValueSet but it is also allowed to add self defined issue descriptions.  

[Click here to se MedCom defined issue descriptions](https://medcomfhir.dk/ig/terminology/ValueSet-medcom-acknowledgement-issue-details.html)


## 1.3 MedComAcknowledgementProvenance
When acknowledging a MedCom Message with an Acknowledgement, two Provenance instances SHALL be included; one describing the MedCom Message that is acknowledged and one describing the Acknowledgement. Therefore, an Acknowledgement Message will always contain two instances of Provenance resource.  

Furthermore, all instances of the Provenance resource SHALL comply to the [MedComMessagingProvenance profile](https://medcomfhir.dk/ig/messaging/StructureDefinition-medcom-messaging-provenance.html)  

## 1.4 Envelope
MedCom Acknowledgement message SHALL be wrapped in a VANSenvelope and sent over VANS-network. 
[To read more about the VANS-network click her.](https://medcomdk.github.io/MedCom-FHIR-Communication/assets/documents/030_Governance-for-Network-Layer.html)  

Values of fields used in a VANSenvelope SHALL obey to the specifications described on the page for VANSenvelope. [Click here to read the specifications for VANSenvelope.](https://medcomdk.github.io/MedCom-FHIR-Communication/assets/documents/FHIRMessages_NetworkEnvelopes_EN.html) 

