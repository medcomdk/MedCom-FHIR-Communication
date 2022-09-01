# Reliable Messaging in general

Realiable Messaging is the way to secure that important information sent through messaging is handled thoroughly and either is sent from the Sending EcoSystem, the Sending Application and its MSH, to a Receiving EcoSystem, the Receiving Application and its MSH, or is handled safely manually. In every part of a message chain something go wrong and Reliable Messaging is developed to handle that.

A message sent from the Sending EcoSystem to the intended Receiving EcoSystem can be well received but the returned acknowledgement can be lost. 

When discovering that the Sending EcoSystem after a well-agreed mutual time hasn't received the acknowledgement, it therefore has to resend the message. 

That message can be lost and again the Sending EcoSystem will not know whether that the message has been received or not. 

It will then have to resend the message again. This time it will be received and acknowledged as before and the acknowledgement will eventually reach the original Sending EcoSystem and the message transaction will be fulfilled. 

The Receiving EcoSystem will in the last event recognize the message as a duplicat and will return exactly the same acknowledgement content as the first time it received the message.

Any of these events can happen over time and therefore Reliable Messaging defines the ruleset used to govern these events.

<figure style="margin-left: 0px; margin-right: 0px; width: 100%;">
<a href="../images/reliable-messaging-principle_1160x763.png" target="_blank"> <img src="../images/reliable-messaging-principle_1160x763.png" alt="reliable messaging principle" style="width:auto; margin-left:0px; margin-right:0px;" id="Fig1"></a>
<figcaption text-align="left"><b>Figure 1: Generic Reliable Messaging Model (Click on the figure to open it in full screen)</b></figcaption>
</figure>
<br>

## 1.0 Different Reliable Messaging scenarios

This section provides a description of the different types of Reliable Messaging scenarios in generic terms. For specific handling of these scenarios for VANSEnvelope and FHIR Messages see the description in the detailed sections of the respective chapters for these subjects.

The different types of Reliable Messaging scenarios are:

* Scenario #1 - Normally successful unsolicited message or request message flow with acknowledgement request
* Scenario #2 - Duplicate an unchanged message with a positive acknowledgement request
* Scenario #3 - (Re-)Sending Unchanged Message
* Scenario #4 - Message is sent normally, acknowledgement is lost along the way
* Scenario #5 - (Re-)Sending Modified Message

### 1.1 Scenario #1 - Normally successful unsolicited message or request message flow with acknowledgement request (Google translated)

An unsolicited message or request message is sent with a new request for a positive acknowledgement from the Sending EcoSystem to a Receiving EcoSystem.

The Receiving EcoSystem **SHALL** always send a positive acknowledgement to the Sending EcoSystem.

### 1.2 Scenario #2 - Duplicate an unchanged message with a positive acknowledgement request (Google translated)

Duplication of an unchanged message can be done in one of the following ways:

* An error may have occurred in the flow from the Sending EcoSystem to the Receiving EcoSystem with subsequent duplication of a message in scenario 1a.
* The Sending EcoSystem may inadvertently send a duplicate of message

The messages are completely identical and as a consequence the message with request for positive acknowledgement arrives at the Receiving EcoSystem more than once.

The Receiving EcoSystem **SHALL** ignore the contents of the duplicate instances of the message, but **SHALL** acknowledge a duplicate message in the same way as the original message. 

A positive acknowledgement may not be sent first and then a negative acknowledgement or vice versa. 

The Receiving EcoSystem **SHALL** never display several instances of a message in a message overview, but **SHALL** log in a system log that reception of a duplicate message has taken place. 

If the Sending EcoSystem of the message has received acknowledgement already after the Receiving EcoSystem's acknowledgement of a message's first instance, the Sending EcoSystem **SHALL** similarly ignore the duplicate instances of the acknowledgement. 

The Sending EcoSystem **SHALL** never display multiple instances of the same acknowledgement in a message summary, but **SHALL** log in a system log that acknowledgement of a duplicate has taken place.

### 1.3 Scenario #3 - (Re) Sending Unchanged Message (Google translated)

Correct retransmission of a message.

The Sending EcoSystem **SHALL** form a new envelope with a new ID and time of dispatch. 

Since there has been no change in the letter section, the rest of the message **SHALL** remain identical.

The message **SHALL** sent and acknowledged as a completely new message according to Scenario #1 or Scenario #2.

Re-dispatches are always done manually and **SHALL** be in accordance with the normal response time for the specific message flow.

### 1.4 Scenario #4 - Message is sent normally, acknowledgement is lost along the way (Google translated)

As Scenario #1, but where acknowledgement is lost along the way from the Sending EcoSystem to the Receiving EcoSystem.

The shipping pattern is like Scenario #3.

### 1.5 Scenario #5 - (Re-) Sending Modified Message (Google translated)

If the content of the letter part is changed, the message **SHALL** be considered a completely new message with the consequent change of both EnvelopeId, LetterId and timestamp, where relevant.

Resubmissions **SHALL** then always be done manually.

For historical reasons, there has been no requirement to use positive acknowledgements for some of MedComs old Messaging Standards, which is why Scenario #1 can in practice be run as Scenario #2.

The Sending EcoSystem may therefore experience that there is no acknowledgement of a message, and it is not recommended to make program logic that sends messages.

For a number of the old MedComs Messaging Standards, however, there is an explicit requirement for a positive acknowledgement, see the documentation for the individual standards if this is the case. 

<a href="https://svn.medcom.dk/svn/releases/MedComs%20Standardkatalog.xlsx" target="_blank">Link to MedComs Messaging Standards Standard Catalogue (in Danish) </a>

| Links for specific ruleset of Reliable Messaging|
|:---|
|[Reliable Messaging in VANSEnvelope](Reliable_Messaging-VANSEnvelope.md)|
|[Reliable Messaging in MedCom FHIR Messaging](Reliable_Messaging-FHIR.md)|
