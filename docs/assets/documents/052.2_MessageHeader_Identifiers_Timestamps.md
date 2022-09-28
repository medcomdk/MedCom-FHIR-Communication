# MessageHeader Identifiers and Timestamps

## MessageHeader Identifiers

A message contains two identifiers:

- the Bundle.id and
- the MessageHeader.id.

Each time a new message is created, it **SHALL** be assigned an identifier (MessageHeader.id) that is unique. This **SHALL** be achieved by using a UUID. Each time a message is sent, the Bundle.id **SHALL** be changed to a new value.

When a receiver receives and processes the message, it **SHALL** respond with a new message with a new identifier, wrapped in a bundle which also has a new id. The response message **SHALL** also quote the request MessageHeader.id in MessageHeader.response.identifier so that the source system can relate the response to its request.

## MessageHeader Timestamps

A message has 2 important timestamps:

- Bundle.timestamp: the time the message was sent
- Bundle.meta.lastUpdated: the last time the message was updated (either by storing, or by modification)

In addition, the message **MAY** have additional timestamps in additional resources in the message, either .meta.lastUpdated or others throughout the resources. The meaning of these will depend on the message event.
