# MessageHeader Identifiers

An incoming message contains two identifiers:

- the Bundle.id and
- the MessageHeader.id.

Each time a new message is created, it SHALL be assigned an identifier (MessageHeader.id) that is unique within that message stream. Note that since message streams are often merged with other streams, it is recommended that the identifier should be globally unique. This can be achieved by using a UUID or an OID. Each time a message is sent, the Bundle.id should be changed to a new value.

When a receiver receives and processes the message, it responds with a new message with a new identifier, wrapped in a bundle which also has a new id. The response message also quotes the request MessageHeader.id in MessageHeader.response.identifier so that the source system can relate the response to its request.