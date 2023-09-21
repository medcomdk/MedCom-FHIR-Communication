# Acknowledgement rules 

| ID | Rules |
|:------| :-----|
| KR1.R | A FHIR message must always be acknowledged |
| KR2.R | An acknowledgement message must never be acknowledged |
| KR3.R | If no errors are found while receiving a message, a positive acknowledgement is made with AA |
| KR4.R | If a technical error occurs in the receiver's system while receiving a message, a negative acknowledgement is made with AE |
| KR5.R | If a message validates negatively against the standard's profiling, it is acknowledged negatively with AR |
| KR6.S | If an acknowledgement of a message is not received within xx minutes, the original message is marked for resending |
