# Reliable Messaging in general

A Application Source (AS) wishes to reliably send messages to an Application Destination (AD) over an unreliable infrastructure. To accomplish this, they make use of a Reliable Messaging Source (RMS) and a Reliable Messaging Destination (RMD). The AS sends a message to the RMS. The RMS uses the a Reliable Messaging protocol to transmit the message to the RMD. The RMD delivers the message to the AD. If the RMS cannot transmit the message to the RMD for some reason, it must raise an exception or otherwise indicate to the AS that the message was not transmitted. The AS and RMS may be implemented within the same process space or they may be separate components. Similarly, the AD and RMD may exist within the same process space or they may be separate components.

The protocol defines and supports a number of Delivery Assurances. These are:

**AtLeastOnce**
- Each message will be delivered to the AD at least once. If a message cannot be delivered, an error must be raised by the RMS and/or the RMD. Messages may be delivered to the AD more than once (i.e. the AD may get duplicate messages).

**AtMostOnce**
- Each message will be delivered to the AD at most once. Messages might not be delivered to the AD, but the AD will never get duplicate messages.

**ExactlyOnce**
Each message will be delivered to the AD exactly once. If a message cannot be delivered, an error must be raised by the RMS and/or the RMD. The AD will never get duplicate messages.
InOrder
Messages will be delivered from the RMD to the AD in the order that they are sent from the AS to the RMS. This assurance can be combined with any of the above assurances.

Reliable Messaging is defined as:

"Reliable Messaging refers to the ability of a sender to deliver a message once and only once to its intended receiver. However the key requirements of Reliable Messaging can be captured more formally as follows:

- Support carrying message traffic reliably in support of business processes whose lifetimes commonly exceed the up times of the components on which these processes are realized
- Support quality-of-service assertions such as:
  - Each message sent be received exactly once (once and only once), at most once, at least once, and so on
  - Messages be received in the same order in which they were sent
  - Failure to deliver a message be made known to both the sender and receiver
- Accommodate mobility of a reliable business process to different channels or physical machines
- Support message transfer via intermediaries
- Leverage the SOAP extensibility mechanism to achieve Reliable Messaging
- Enable Reliable Messaging bindings to a variety of underlying reliable and unreliable transport protocols together with the Message Routing Protocol
- Compose with other protocols to support security and other message delivery services
-->
