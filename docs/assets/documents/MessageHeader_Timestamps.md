# MessageHeader Timestamps

A message has 2 important timestamps:

- Bundle.timestamp: the time the message was sent
- Bundle.meta.lastUpdated: the last time the message was updated (either by storing, or by modification)

In addition, the message may have additional timestamps in additional resources in the message, either .meta.lastUpdated or others throughout the resources. The meaning of these will depend on the message event.
