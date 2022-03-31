# Acknowledgment rules

| ID    | Regel |
|:------| :-----|
| KR1.R | Der skal altid kvitteres på en FHIR-meddelelse |
| KR2.R | Der må aldrig kvitteres på en kvitteringsmeddelelse |
| KR3.R | Hvis der ikke findes fejl under modtagelse af en meddelelse, kvitteres der positivt med AA |
| KR4.R | Hvis der sker en teknisk fejl i modtagersystemet under modtagelse af en meddelelse, kvitteres der negativt med AE |
| KR5.R | Hvis en meddelelse validerer negativt mod standardens profilering, kvitteres der negativt med AR |
| KR6.S | Hvis en kvittering på en meddelelse ikke er modtaget inden xx minutter, markeres den originale med-delelse til genafsendelse |
