# MessageHeader

From FHIR R4:

The header for a message exchange that is either requesting or responding to an action. The reference(s) that are the subject of the action as well as other information related to the action are typically transmitted in a bundle in which the MessageHeader resource instance is the first resource in the bundle.

## Scope and Usage
The MessageHeader resource is defined in order to support Messaging using FHIR resources. The principal usage of the MessageHeader resource is when messages are exchanged. However, as a resource that can be used with the RESTful framework, the MessageHeader resource has the normal resource end-point ([base-url]/MessageHeader), which is used to manage a set of static messages resources. This could be used to make an archive of past messages available. Creating or updating Message resources in this fashion does not represent the actual occurrence of any event, nor can it trigger any logic associated with the actual event. It is just for managing a set of message resources.