# Messaging using FHIR Resources

FHIR Resources can be used in a traditional messaging context, much like HL7 v2  (see detailed comparison). Applications asserting conformance to this framework claim to be conformant to "FHIR messaging" (see Conformance).

In FHIR messaging, a "request message" is sent from a source application to a destination application when an event happens. Events mostly correspond to things that happen in the real world. The request message consists of a Bundle identified by the type "message", with the first resource in the bundle being a MessageHeader resource. The MessageHeader resource has a code - the message event - that identifies the nature of the request message, and it also carries additional request metadata. The other resources in the bundle depend on the type of the request.

The events supported in FHIR, along with the resources that are included in them, are defined below.

The destination application processes the request and returns one or more response messages which are also a bundle of resources identified by the type "message", with the first resource in each bundle being a MessageHeader resource with a response section that reports the outcome of processing the message and any additional response resources required.

## MessageHeader Identifiers & Timestamps

An incoming message contains two identifiers: the Bundle.id and the MessageHeader.id. Each time a new message is created, it SHALL be assigned an identifier (MessageHeader.id) that is unique within that message stream. Note that since message streams are often merged with other streams, it is recommended that the identifier should be globally unique. This can be achieved by using a UUID or an OID. Each time a message is sent, the Bundle.id should be changed to a new value.

When a receiver receives and processes the message, it responds with a new message with a new identifier, wrapped in a bundle which also has a new id. The response message also quotes the request MessageHeader.id in MessageHeader.response.identifier so that the source system can relate the response to its request.

A message has 2 important timestamps:

Bundle.timestamp: the time the message was sent
Bundle.meta.lastUpdated: the last time the message was updated (either by storing, or by modification)
In addition, the message may have additional timestamps in additional resources in the message, either .meta.lastUpdated or others throughout the resources. The meaning of these will depend on the message event.
