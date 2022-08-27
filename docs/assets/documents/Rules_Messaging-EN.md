# Messaging rules (Google translated)

| ID | Rule |
|:------| :-----|
| MR1.S | An acknowledgment must always be requested on a FHIR message |
| MR2.S | A message is marked as sent and received when an AA acknowledgment has been received |
| MR3.S | A message is marked as failed when a negative AR acknowledgment has been received |
| MR4.S | A message is marked as failed when a negative AE acknowledgment has been received |
| MR5.R | A message must be resent x times upon receipt of an AE Acknowledgment |
| MR6.R | A message must be re-sent x times in the event of failure to receive an Acknowledgment |
| MR7.R | A message that is resent must always be updated with new timestamp=Bundle.timestamp and new envelope time=Bundle.id |
| MR8.R | A message is a duplicate if it contains the same MessageHeader.Id as a previously received message |
