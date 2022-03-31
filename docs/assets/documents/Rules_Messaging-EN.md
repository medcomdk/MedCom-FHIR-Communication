# Messaging rules

| ID    | Regel |
|:------| :-----|
| MR1.S | Der skal altid anmodes om kvittering på en FHIR-meddelelse |
| MR2.S | En meddelelse markeres som sendt og modtaget, når der er modtaget en AA kvittering |
| MR3.S | En meddelelse markeres som fejlet, når der er modtaget en negativ AR kvittering |
| MR4.S | En meddelelse markeres som fejlet, når der er modtaget en negativ AE kvittering |
| MR5.R | En meddelelse må forsøges gensendt x gange ved modtagelse af en AE Kvittering |
| MR6.R | En meddelelse må forsøges gensendt x gange ved manglende modtagelse af en Kvittering |
| MR7.R | En meddelelse, der gensendes, skal altid opdateres med ny timestamp=Bundle.timestamp og ny kuvertid=Bundle.id |
| MR8.R | En meddelelse er en dublet, hvis den indeholder samme MessageHeader.Id som en tidligere modta-get meddelelse |
