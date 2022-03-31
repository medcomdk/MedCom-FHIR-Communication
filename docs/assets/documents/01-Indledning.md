# Indledning

![alt text](https://medcomdk.github.io/MedCom-FHIR-Communication/fhir-logo.png "HL7 FHIR")

Disse ”FHIR syntaks- og kommunikationsregler” har til formål at præcisere benyttelsen af MedComs FHIR-meddelelser til sundheds- og socialområdet.

Det er hensigten, at reglerne sammen med MedComs standarder for de enkelte meddelelser kan udgøre det fulde og tilstrækkelige grundlag for at implementere MedComs sygehusmeddelelser – på samme måde som dette var tilfældet for ”De gode EDI-breve” på primærområdet.

Syntaks- og kommunikationsreglerne skal således kunne fungere som ”overdommer”, hvor der er tvivl om den praktiske anvendelse af MedComs FHIR-meddelelser til sundheds- og socialområdet.

Syntaks- og kommunikationsreglerne bygger i vid udstrækning på erfaringerne fra anvendelse af EDIFACT-kommunikation i primærsektoren – med den væsentlige forskel at der anvendes XML syntaks på sygehusområdet i stedet for EDIFACT.

Derudover er MedComs XML-breve blevet tilpasset Forskningsministeriets regelsæt for dokumentation af data i den offentlige sektor (”OIO – Offentlig Information Online”).
Endelig er det gjort muligt

- at medsende en eller flere binære filer (f.eks. et billede)
- at angive en Internet URL reference
- at angive en reference til en SUP database
- at tilføje lokale (to-sidigt aftalte) xml-koder, der ikke fremgår af MedCom standarden.

MedComs meddelelser er beregnet til kommunikation mellem forskellige leverandørers IT-systemer.

I primærsektoren er dette oftest intuitivt klart, f.eks. mellem de forskellige lægers EPJ-systemer indbyrdes og med de forskellige apotekssystemer.
På sygehusene kan denne skelnen af og til være mindre klar. F.eks. anvender alle amter centrale PAS IT-systemer, der dækker samtlige sygehuse og samtlige sygehusafdelinger i amtet. I sådanne tilfælde "kommunikeres" internt i selve IT-systemet ("databasekommunikation") eller ved benyttelse af "in-house" formater og forskellige former for integrationsplatforme. I disse tilfælde benyttes "Syntaks- og kommunikationsreglerne" i sagens natur ikke internt – kun eksternt til andre leverandørers IT-systemer.

I det følgende gennemgås først ”syntaksreglerne” for anvendelse af MedComs sygehusmeddelelser, og dernæst de mere overordnede kommunikationsregler.
"FHIR syntaks- og kommunikationsreglerne" skal sikre en ensartet brug af MedComs FHIR-meddelelser til sundheds- og socialområdet.
