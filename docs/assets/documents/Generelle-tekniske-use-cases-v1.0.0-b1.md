# GENERELLE TEKNISKE USE CASES FOR AFSENDELSE OG MODTAGELSE AF MEDDELELSER, KVITTERINGER OG KUVERTER

![](Aspose.Words.a77aa0f5-ad23-4c34-839d-9463f19dc431.003.png)

|**Id og proces**|**Id og titel**|**Init**|**Version**|**Dato**|
| :- | :-: | :-: | -: | -: |
|SOP 4.1 |SKA-4.X.X-Forretningsmæssige use cases|OVI/MBK/KML|1.0.0-rc.1|06-04-2022|

## Indholdsfortegnelse

[1 Indledning 3](#_Toc97758631)

[1.1 Baggrund og formål 3](#_Toc97758632)

[1.2 Målgruppe 3](#_Toc97758633)

[1.3 Afgrænsning 3](#_Toc97758634)

[1.4 Referencer 3](#_Toc97758635)

[1.5 Læsevejledning for use cases 3](#_Toc97758636)

[1.6 Termer 5](#_Toc97758637)

[1.7 Illustration af et fagsystem og dets forretningsmæssige og tekniske dele 7](#_Toc97758638)

[2 Oversigt over use cases 7](#_Toc97758639)

[3 Use cases for afsendelse af meddelelser 9](#_Toc97758640)

[3.1 S.TC1 Afsend meddelelse 9](#_Toc97758641)

[3.2 S.TC2 Gensend automatisk meddelelse 10](#_Toc97758642)

[4 Use cases for modtagelse af meddelelser 11](#_Toc97758643)

[4.1 R.TC1 Modtag meddelelse 12](#_Toc97758644)

[4.1.1 R.TC1.A1 Afvis meddelelse pga. invalidt teknisk indhold 12](#_Toc97758645)

[4.1.2 R.TC1.A2 Afvis meddelelse pga. teknisk fejl i modtagersystemet 13](#_Toc97758646)

[4.1.3 R.TC3 Håndtér dubleret meddelelse 13](#_Toc97758647)

[5 Use cases for afsendelse af kvittering 14](#_Toc97758648)

[5.1 R.TC2 Dan kvittering 14](#_Toc97758649)

[5.2 R.TC3 Afsend kvittering 15](#_Toc97758650)

[6 Use cases for modtagelse af kvittering 16](#_Toc97758651)

[6.1 S.TC3 Modtag kvittering (ACK AA) 17](#_Toc97758652)

[6.1.1 S.TC3.A1 Modtag negativ kvittering (ACK AE) 17](#_Toc97758653)

[6.1.2 S.TC3.A2 Modtag negativ kvittering (ACK AR) 18](#_Toc97758654)

[6.2 S.TC4 Forventet kvittering ikke modtaget 18](#_Toc97758655)

[7 Regler i systemerne, som use casene beror på 19](#_Toc97758656)

[7.1 Meddelelsesregler 19](#_Toc97758657)

[7.2 Kvitteringsregler 19](#_Toc97758658)

[7.3 Fejltilstande 20](#_Toc97758659)

[7.4 Meddelelsestilstand 20](#_Toc97758660)

## Indledning

Dette dokument indeholder en række tekniske use case til brug for implementering af alle MedComs meddelelsesstandarder. 

Use case-beskrivelserne supplerer det øvrige dokumentationsmateriale og bør derfor læses i sammenhæng til dette (se afsnit 1.4).

## Baggrund og formål
Formålet med de tekniske use cases er at beskrive de generelle tekniske krav, der er forbundet med afsendelse og modtagelse af MedCom-standarder, herunder systemets funktionaliteter ift. kommunikationsnetværket samt afsendelse og modtagelse af kvitteringer. Dokumentet har til hensigt at sikre en ensartet implementering og anvendelse af MedCom-standarder. 

## Målgruppe
Dokumentet målretter sig både it-systemleverandører og implementeringsansvarlige.

## Afgrænsning
Use casene i dette notat beskriver de tekniske handlinger, som ligger før og efter brugeraktørens interaktion med systemet (fx systemets funktionaliteter i kommunikationsnetværket samt afsendelse og modtagelse af kvitteringer). De handlinger/use cases, der vedrører brugeraktørens interaktion med systemet, og som beskriver de forretningsmæssige krav til standarden, optræder som selvstændigt beskrevne use cases i et dokument baseret på ”SKA-4.X.X Forretningsmæssige use cases”.

Tekniske afsender-use cases indledes således med, at systemaktøren henter meddelelsesindholdet fra [*fagsystemets forretningsmæssige udbakke*](#_Toc83807604) og afsluttes med, at systemaktøren sender meddelelsen ved at lægge den i [*fagsystemets tekniske udbakkeReferencer*](#_Referencer). Ligeledes igangsættes tekniske modtager-use cases med, at systemaktøren modtager meddelelsen i [*fagsystemets tekniske indbakke*](#_Toc83807604) og afsluttes med, at systemaktøren lægger meddelelsen i [*fagsystemets forretningsmæssige indbakke*](#_Toc83807604). Se i øvrigt forklaring og illustration i afsnit 1.6.  

## Referencer

|**Materiale/reference**|**Version**|**Link/reference**|**Beskrivelse**|
| :- | :- | :- | :- |
|SKA-4.X.X Forretningsmæssige use cases|SKA-4.XX|LINK|Skabelon, som disse use cases er udarbejdet på baggrund af|

## Læsevejledning for use cases

Use casene beskriver et detaljeret forløb over *systemaktørens* tekniske handlinger, som finder sted før og efter brugeraktørens interaktion med systemet.

Der skelnes mellem tre forskellige typer af use cases:

- **Primære** tekniske** use cases: For hvert teknisk scenarie vil der være beskrevet én primær teknisk use case, som beskriver normalforløbet over systemaktørens interaktion med kommunikationsnetværket.  
- **Alternative** tekniske** use cases: Såfremt der kan være afvigelser til det tekniske normalforløb, vil der i den primære tekniske use case være henvist til alternative (selvstændigt beskrevne) tekniske use cases. 
- **Korrigerende tekniske** use cases: Ligeledes vil der ved korrigerende handlinger til forløbet (typisk rettelser og annulleringer) være henvist til korrigerende (selvstændigt beskrevne) use cases fra den primære use case. De korrigerende use cases vil typisk være generiske på tværs af forskellige use cases.

Alle use cases er opdelt i:

- Afsender (S)-use case: Beskriver use casen fra systemets afsenderside (S = sender)
- Modtager (R)-use case: Beskriver use casen fra systemets modtagerside (R = receiver)

Hver teknisk use case er bygget op af nedenstående elementer.[^1]

|**Element**|**Forklaring**|
| :- | :- |
|ID|Unikt ID|
|Navn|Aktivitet i bydemåde|
|Igangsættende aktør|I de tekniske use cases altid ’systemaktør’|
|Formål|Kort beskrivelse af det tekniske formål, samt eventuel afgrænsning til andre use cases|
|Startbetingelser/forudsætninger|De forudsætninger, der skal være opfyldt for at scenariet/use casen kan gennemføres frem til slutresultatet|
|Igangsættende hændelse|Den begivenhed eller hændelse, som udløser aktørens handlinger i scenariet/use casen|
|Handlinger|Forløbet af handlinger, der – uden afbrydelser – fører fra den igangsættende begivenhed til slutresultatet|
|Slutresultat|Det ønskede tekniske mål|
|Alternative handlinger (A)|Beskrivelse af eventuelle alternative handlinger, der afviger fra handlingerne i normalforløbet (med reference/link til alternative use case(s)|
|Korrigerende handlinger (CANC/CORR)|Beskrivelse af korrigerende handlinger, der foretaget, når et forløb ender med en fejlsituation eller med genoptagelse (med reference/link til korrigerende use cases. Eksempelvis rettelser og annulleringer|

Tabel 1: Oversigt over de elementer, som indgår i de tekniske use cases

## Termer

|**Termer**|**Beskrivelse**|
| :- | :- |
|Fagsystem|Et fagsystem består – ift. meddelelsesforsendelse og -modtagelse – af en forretningsmæssig og en teknisk del.Fagsystemets to dele kan være alt fra et tæt sammenbygget system til to forskellige moduler i samme system, eller to systemer, der er konfigureret til at kommunikere sammen. Dette er uden betydning for use casenes opbygning.|
|Afsendersystem|Fagsystem hos afsender af en meddelelse|
|Modtagersystem|Fagsystem hos modtager af en meddelelse|
|Fagsystemets forretningsmæssige del |I den forretningsmæssige del håndteres alt det faglige, som er fagsystemets primære anvendelsesområde. Fagsystemets forretningsmæssige del består af- Fagsystemets forretningsmæssige indbakke- Fagsystemets forretningsmæssige modul - Fagsystemets forretningsmæssige udbakke|
|Fagsystemets tekniske del |I den tekniske del håndteres kommunikationen med kommunikationsnetværket vedrørende afsendelse og modtagelse af meddelelser og kvitteringer. Her evalueres også hvilken kvitteringstype, der skal retur til afsender af en modtaget meddelelse.Fagsystemets tekniske del består af:- Fagsystemets tekniske indbakke- Fagsystemets tTekniske meddelelsesmodul - Fagsystemets tekniske udbakke|
|Fagsystemets forretningsmæssige modul|I Fagsystemets forretningsmæssige modul håndteres alt det faglige, som er fagsystemets primære anvendelsesområde. Det er bl.a. her slutbrugeren arbejder med brugergrænsefladen i fagsystemet.|
|Fagsystemets forretningsmæssige indbakke|Fagsystemets forretningsmæssige indbakke er en abstrakt term for den indgående funktionalitet mellem fagsystemets tekniske del og dets forretningsmæssige del i indgående retning set ift. den forretningsmæssige del.|
|Fagsystemets forretningsmæssige udbakke|Fagsystemets forretningsmæssige udbakke er en abstrakt term for den udgående funktionalitet mellem fagsystemets forretningsmæssige del og dets tekniske del i udgående retning set ift. den forretningsmæssige del.|
|Fagsystemets tTekniske meddelelsesmodul|Fagsystemets tTekniske meddelelsesmodul håndteres transformationer og valideringer af meddelelserne, og her evalueres også hvilken kvitteringstype, der skal retur til afsender af en modtaget meddelelse. Her håndteres også evt. konvolutindpakninger.|
|Fagsystemets tekniske indbakke|Fagsystemets tekniske indbakke er en abstrakt term for den indgående funktionalitet mellem kommunikationsnetværket og fagsystemets tTekniske meddelelsesmodul i indgående retning set ift. kommunikationsnetværket.Fagsystemets tekniske indbakke er reelt kommunikationsnetværkets aflevering af en meddelelse til fagsystemet. |
|Fagsystemets tekniske udbakke|Fagsystemets tekniske udbakke er en abstrakt term for den udgående funktionalitet mellem fagsystemets forretningsmæssige udbakke og kommunikationsnetværket i udgående retning set ift. fagsystemets forretningsmæssige del.Fagsystemets tekniske udbakke er reelt forsendelse af en meddelelse til kommunikationsnetværket.|
|Standarddokumentationen|En samlet dokumentation bestående af - Forretningsmæssig dokumentation- Forretningsmæssige og tekniske use cases- Profilering af standarden|
|Kommunikationsnetværket |Kommunikationsnetværket er det netværk, som meddelelser fysisk afsendes på. Netværket er pt det samme som VANS- netværket.|
|Forsendelsesflow |Et forsendelsesflow er det samlede antal hændelser, der sker i en konkret meddelelses vej fra slutbrugeren i fFagsystemets forretningsmæssige modul afsender en meddelelse til slutbrugeren i Fagsystemets forretningsmæssige modul hos modtager og det tilhørende kvitteringsflow flyder den modsatte vej til den oprindelige afsender.|
|MeddelelsesId|Meddelelsens unikke Id, som danner baggrund for vurdering af, om en meddelelse tidligere er afsendt/modtaget|
|KuvertId|Forsendelsens unikke Id, som danner baggrund for vurdering af, om en kuvert tidligere er modtaget|
|ACK AA|HL7 kvitteringsterm for en positiv kvittering. ACK AA er HL7s pendant til MedComs Positive CTRL ((X)CTL03)|
|ACK AE|HL7 kvitteringsterm for en negativ kvittering, hvor modtagersystemet har haft en teknisk fejl under modtagelse af meddelelsen således, at den ikke kunne indlæses i systemet. ACK AE er HL7s ikke dækket af MedComs Negative CTRL ((X)CTL02)|
|ACK AR|HL7 kvitteringsterm for en negativ kvittering på en meddelelse, hvis indhold er invalidt ift. standardens profilering. ACK AR er HL7s pendant til MedComs Negative CTRL ((X)CTL02) |

## Illustration af et fagsystem og dets forretningsmæssige og tekniske dele

Illustrationen herunder angiver i detaljer et forsendelsesflow mellem to fagsystemer for en given meddelelse. Indeværende dokument omfatter den tekniske del (markeret med grøn) af forsendelsesflowet, mens dokumentet ”Forretningsmæssige use cases” omfatter den forretningsmæssige del (markeret med rød). 

De tekniske use cases vedrører primært hhv. Fagsystemets Tekniske Meddelelsesmodul og Fagsystemets Tekniske Udbakke i Afsendersystemet og Fagsystemets Tekniske Indbakke og Fagsystemets Tekniske Meddelelsesmodul i Modtagersystemet. Fagsystemets tekniske dele har i afsendersystemet udveksling med Fagsystemets Forretningsmæssige Udbakke og i modtagersystemet med Fagsystemets Forretningsmæssige Indbakke.

![](Aspose.Words.a77aa0f5-ad23-4c34-839d-9463f19dc431.004.png)

## Oversigt over use cases
I denne oversigt over use cases kan det synes mærkeligt, at kvitterings use cases ”vender omvendt” ift. afsendelse og modtagelses use cases for meddelelser. Dette skyldes at use casene skal ses i sammenhæng i et Forsendelsesflow, som indebærer afsendelse/modtagelse af en meddelelse og afsendelse/modtagelse af den tilhørende kvittering.

|**Teknisk hændelse**|**Afsender (S)-use case**|**Modtager (R)-use case**|
| :- | -: | -: |
|Afsend meddelelse|[**S.TC1**](#_Toc82614226)||
|Gensend automatisk meddelelse|[**S.TC2**](#_S.TC2_-_Automatisk)||
|Modtag meddelelse||[**R.TC1** ](#_R.TC1_Modtagelse_af)|
|*Afvis meddelelse pga. invalidt indhold*||[***R.TC1.A1***](#_R.TC1.A1_Afvisning_af)|
|*Afvis meddelelse pga. teknisk fejl I modtagersystemet*||[***R.TC1.A2***](#_R.TC1.A2_Afvisning_af)|
|*Håndtér dubleret meddelelse*||[***R.TC1.A3***](#_R.TC1.A3_Modtagelse_af)|
|Dan kvittering||[**R.TC2**](#_R.TC2_Dan_kvittering)|
|Afsend kvittering||[**R.TC3**](#_R.TC2_Afsendelse_af)|
|Modtag kvittering (ACK AA)|[**S.TC3** ](#_S.TC2_Modtagelse_af)||
|*Modtag negativ kvittering (ACK AE)*|[***S.TC3.A1](#_S.TC2.A1_Modtagelse_af)*** ||
|*Modtag negativ kvittering (ACK AR)*|[***S.TC3.A2](#_S.TC2.A2_Modtagelse_af)*** ||
|Forventet kvittering ikke modtaget|[**S.TC4**](#BKM_D8323758_66B8_46FA_A405_D03A01013483)||

## Grafisk oversigt over use cases

![](Aspose.Words.a77aa0f5-ad23-4c34-839d-9463f19dc431.005.png)

**Figur 1 Grafisk oversigt over tekniske use cases (R = Receiver, S = Sender, TC = Technical (use) Case, ACK AA = Positiv kvittering, ACK AE = Negativ kvittering (teknisk fejl), ACK AR = Negativ kvittering (invalidt indhold),**

Ovenstående grafiske oversigt viser det samlede sæt af use cases, som dette dokument beskriver. I de følgende afsnit er de brudt ned i relevante grupperinger og vises i de følgende kapitler partielt. Teksten er på engelsk.


# Use cases for afsendelse af meddelelser

Indsæt grafik + forklarende tekst til afsendelses use cases

## S.TC1 Afsend meddelelse

|**S.TC1**|**Afsend meddelelse**|
| :- | :- |
|Igangsættende aktør|Systemaktør|
|Formål|At Systemaktør afsender en meddelelse, som er blevet placeret i Fagsystemets forretningsmæssige udbakke |
|Startbetingelser/forudsætninger|Brugeraktør har afsendt en meddelelse|
|Igangsættende hændelse|Systemaktør har lagt et meddelelsesindhold i Fagsystemets forretningsmæssige udbakke med henblik på afsendelse som meddelelse|
|Handlinger|1. Systemaktør henter meddelelsesindholdet fra Fagsystemets forretningsmæssige udbakke|
||2. Systemaktør formaterer meddelelsesindholdet iht. standardens meddelelsesformat|
||3. Systemaktør markerer meddelelse for at ville modtage kvittering jf. Regler i systemerne, som use casene beror på|
||4. Systemaktør sender meddelelsen ved at lægge den i Fagsystemets tekniske udbakke|
|Slutresultat|Systemaktør har lagt en formateret meddelelse markeret med ønske om kvittering i Fagsystemets tekniske udbakke|
|Bemærkninger|Meddelelsen sendes med indhold som beskrevet i standarddokumentationen|

## S.TC2 Gensend automatisk meddelelse

|**S.TC2**|**Gensend automatisk meddelelse**|
| :- | :- |
|Igangsættende aktør|Systemaktør|
|Formål|At Systemaktør automatisk gensender en meddelelse, som er blevet placeret i Fagsystemets forretningsmæssige udbakke |
|Startbetingelser/forudsætninger|Systemaktør har enten - Ikke modtaget kvittering på en meddelelse eller - Modtaget negativ kvittering af typen ACK AE på en meddelelse|
|Igangsættende hændelse|Systemaktør har lagt et meddelelsesindhold i Fagsystemets forretningsmæssige udbakke med henblik på automatisk gensendelse af meddelelsen|
|Handlinger|1. Systemaktør henter meddelelsesindholdet fra Fagsystemets forretningsmæssige udbakke|
||2. Systemaktør formaterer meddelelsesindholdet iht standardens meddelelsesformat|
||3. Systemaktør markerer meddelelse for at ville modtage kvittering jf. Regler i systemerne, som use casene beror på|
||4. Pba. MeddelelsesId genkender Systemaktør meddelelsen som en tidligere afsendt meddelelse og tildeler herved meddelelsen en ny KuvertId. |
||5. Systemaktør sender meddelelsen ved at lægge den i Fagsystemets tekniske udbakke|
|Slutresultat|Systemaktør har lagt en formateret meddelelse markeret med ønske om kvittering i Fagsystemets tekniske udbakke|
|Bemærkninger|Meddelelsen sendes med indhold som beskrevet i standarddokumentationen|

# Use cases for modtagelse af meddelelser

Indsæt forklarende tekst til modtagelses use cases

![](Aspose.Words.a77aa0f5-ad23-4c34-839d-9463f19dc431.006.png)

## R.TC1 Modtag meddelelse

|**R.TC1**|**Modtag meddelelse**|
| :- | :- |
|Igangsættende aktør|Systemaktør|
|Formål|At lægge en meddelelse i Fagsystemets forretningsmæssige indbakke med henblik på forretningsmæssig modtagelse af meddelelsen|
|Startbetingelser/forudsætninger|Kommunikationsnetværket har lagt en meddelelse i Fagsystemets tekniske indbakke|
|Igangsættende hændelse|Systemaktør registrerer, at der er modtaget en meddelelse i Fagsystemets tekniske indbakke |
|Handlinger|1. Systemaktør henter meddelelse i Fagsystemets tekniske indbakke og persisterer den i systemet|
||2. Systemaktør evaluerer meddelelsen positivt (ACK AA) mod standardens profilering|
||3. Systemaktør konstaterer, at meddelelsen er markeret for at ville modtage kvittering jf. Regler i systemerne, som use casene beror på og logger/markerer, at der skal sendes positiv kvittering|
||4. Systemaktør formaterer meddelelsesindholdet iht. fagsystemets meddelelsesformat|
||5. Systemaktør lægger meddelelsesindholdet i Fagsystemets forretningsmæssige indbakke|
|Slutresultat|Systemaktør har lagt et formateret meddelelsesindholdet i Fagsystemets forretningsmæssige indbakke og logget/markeret for, at der skal sendes en positiv kvittering.|
|Alternative handlinger|2a. R.TC1.A1 Afvis meddelelse pga. teknisk invalidt indhold2b. R.TC1.A2 Afvis meddelelse pga. teknisk fejl i modtagersystemet|
|Bemærkninger|Meddelelsen modtages med indhold som beskrevet i standarddokumentationen for den pågældende meddelelse|

## R.TC1.A1 Afvis meddelelse pga. invalidt teknisk indhold

|**R.TC1.A1**|**Afvis meddelelse pga. invalidt teknisk indhold.**|
| :- | :- |
|Reference til use case som denne use case er et alternativ til|[R.TC1 Modtag meddelelse](#_R.TC1_Modtagelse_af)|
|Handlinger|1. Systemaktør henter meddelelsen i Fagsystemets tekniske indbakke og persisterer den i systemet|
||2. Systemaktør evaluerer meddelelsen negativt (ACK AR) mod standardens profilering|
||3. Systemaktør logger/markerer, at der skal sendes negativ kvittering pba. invalidt teknisk indhold.|
|Slutresultat|Systemaktør har afvist en meddelelse modtaget i Fagsystemets tekniske indbakke og logget/markeret for, at der skal sendes en negativ kvittering af typen ACK AR.|
|Bemærkninger||

## R.TC1.A2 Afvis meddelelse pga. teknisk fejl i modtagersystemet

|**R.TC1.A2**|**Afvis meddelelse pga. teknisk fejl i modtagersystemet**|
| :- | :- |
|Reference til use case som denne use case er et alternativ til|[R.TC1 Modtag meddelelse](#_R.TC1_Modtagelse_af)|
|Handlinger|1. Systemaktør henter meddelelsen i Fagsystemets tekniske indbakke og persisterer den i systemet|
||2. Systemaktør evaluerer meddelelsens metadatainformation negativt (ACK AE) pga. en teknisk fejl ifm. modtagersystemets modtagelse af meddelelsen |
||3. Systemaktør logger/markerer, at der skal sendes negativ kvittering pba. teknisk fejl i modtagersystemet.|
|Slutresultat|Systemaktør har afvist en meddelelse modtaget i Fagsystemets tekniske indbakke og logget/markeret for, at der skal sendes en negativ kvittering af typen ACK AE.|
|Bemærkninger||

## R.TC3 Håndtér dubleret meddelelse

|**R.TC3**|**Håndtér af dubleret meddelelse**|
| :- | :- |
|Igangsættende aktør|Systemaktør|
|Formål|At håndtere at samme meddelelse i modtages flere gange fra kommunikationsnetværket|
|Startbetingelser/forudsætninger|Kommunikationsnetværket har lagt en meddelelse i Fagsystemets tekniske indbakke|
|Igangsættende hændelse|Systemaktør registrerer, at der er modtaget en meddelelse i Fagsystemets tekniske indbakke |
|Handlinger|1. Systemaktør henter meddelelse i Fagsystemets tekniske indbakke og persisterer den i systemet|
||2. Systemaktør evaluerer meddelelsen og dens metadatainformation og vurderer den som en dublet af en tidligere modtaget meddelelse.|
||3. Systemaktør konstaterer, at systemet skal sende kvittering af samme type og med samme indhold, som blev sendt som feedback på originalmeddelelsen jf. Regler i systemerne, som use casene beror på og logger/markerer, at en sådan skal sendes.|
|Slutresultat|Systemaktør har evalueret meddelelsen som en dublet og logget/markeret, at systemet skal sende kvittering af samme type og med samme indhold, som blev sendt som feedback på originalmeddelelsen|
|Bemærkninger||

# Use cases for afsendelse af kvittering

Indsæt forklarende tekst til afsendelses use cases

![](Aspose.Words.a77aa0f5-ad23-4c34-839d-9463f19dc431.007.png)

## R.TC2 Dan kvittering

|**R.TC2**|**Dan kvittering** |
| :- | :- |
|Igangsættende aktør|Systemaktør|
|Formål|At Systemaktør danner en korrekt udformet kvittering og lægger denne i Fagsystemets forretningsmæssige udbakke|
|Startbetingelser/forudsætninger|Systemaktør har registreret logningsinformation omkring kvittering for en given meddelelse|
|Igangsættende hændelse|Systemaktør konstater at der er logningsinformation omkring kvittering for en given meddelelse |
|Handlinger|1. Systemaktør henter logningsinformation omkring kvittering|
||2. Systemaktør opretter kvittering pba. logningsinformation og formaterer denne iht. kvitteringens meddelelsesformat|
||3. Systemaktør lægger kvitteringen i Fagsystemets forretningsmæssige udbakke|
|Slutresultat|Systemaktør har dannet korrekt udformet kvittering ved at lægge den i Fagsystemets forretningsmæssige udbakke|
|Alternative handlinger||
|Bemærkninger|Kvitteringen dannes med indhold som beskrevet i kvitteringsstandarden|

## R.TC3 Afsend kvittering

|**R.TC3**|**Afsend kvittering** |
| :- | :- |
|Igangsættende aktør|Systemaktør|
|Formål|At Systemaktør afsender en kvittering, som er blevet placeret i Fagsystemets forretningsmæssige udbakke|
|Startbetingelser/forudsætninger|Systemaktør har dannet kvitteringsindhold |
|Igangsættende hændelse|Systemaktør har lagt et kvitteringsindhold i Fagsystemets forretningsmæssige udbakke med henblik på afsendelse som kvittering|
|Handlinger|1. Systemaktør henter kvitteringsindhold i Fagsystemets forretningsmæssige udbakke|
||2. Systemaktør opretter kvittering pba. kvitteringsindhold og formaterer denne iht. standardens meddelelsesformat|
||3. Systemaktør sender kvitteringen ved at lægge den i Fagsystemets tekniske udbakke|
|Slutresultat|Systemaktør har lagt en formateret kvittering i Fagsystemets tekniske udbakke|
|Alternative handlinger||
|Bemærkninger|Kvitteringen sendes med indhold som beskrevet i kvitteringsstandarden|

# Use cases for modtagelse af kvittering

Indsæt forklarende tekst til modtagelses use cases

![](Aspose.Words.a77aa0f5-ad23-4c34-839d-9463f19dc431.008.png) 

## S.TC3 Modtag kvittering (ACK AA)

|**S.TC3**|**Modtag kvittering (ACK AA)**|
| :- | :- |
|Igangsættende aktør|Systemaktør|
|Formål|At Systemaktør teknisk modtager en korrekt udformet kvittering og markerer den oprindelige afsendte meddelelse som sendt og kvitteret|
|Startbetingelser/forudsætninger|Kommunikationsnetværket har lagt en kvitteringsmeddelelse i Fagsystemets tekniske indbakke|
|Igangsættende hændelse|Systemaktør registrerer, at der er modtaget en kvitteringsmeddelelse i Fagsystemets tekniske indbakke|
|Handlinger|1. Systemaktør henter kvitteringsmeddelelse i Fagsystemets tekniske indbakke og persisterer den i systemet|
||2. Systemaktør evaluerer kvitteringsmeddelelsen teknisk valid (ACK AA) ved brug af Kvitteringsregler|
||3. Systemaktør markerer den oprindelige meddelelse for at være sendt og positivt kvitteret|
||4. Systemaktør udtrækker metadatainformation fra kvitteringen og lægger denne i Fagsystemets forretningsmæssige indbakke|
|Slutresultat|Systemaktør har markeret den oprindelige meddelelse for at være sendt og positivt kvitteret, og har lagt metadatainformation om denne i Fagsystemets forretningsmæssige indbakke.|
|Alternative handlinger|Hvis handlingspunkt 2 ikke er positiv (ACK AA) kan en af følgende 2 handlinger være alternative handlinger:- S.TC3.A1 Modtag negativ kvittering (ACK AE)- S.TC3.A2 Modtag negativ kvittering (ACK AR)|
|Bemærkninger|Kvitteringen er modtaget med indhold som beskrevet i kvitteringsstandarden|

## S.TC3.A1 Modtag negativ kvittering (ACK AE)

|**S.TC3.A1**|**Modtag negativ kvittering (ACK AE) pga. teknisk fejl under modtagelse i modtagersystem**|
| :- | :- |
|Reference til use case som denne use case er et alternativ til|S.TC3 Modtag kvittering (ACK AA)|
|Handlinger|1. Systemaktør henter kvitteringsmeddelelse i Fagsystemets tekniske indbakke og persisterer den i systemet|
||2. Systemaktør evaluerer, om kvitteringsmeddelelsen er teknisk valid ved brug af Kvitteringsregler|
||3. Systemaktør konstaterer, at det er en negativ kvittering af typen ACK AE|
||4. Systemaktør markerer den oprindelige meddelelse for at være fejlet|
||5. Systemaktør markerer den oprindelige meddelelse til gensendelse.|
|Slutresultat|Systemaktør har markeret den oprindelige meddelelse for at være fejlet og markeret den oprindelige meddelelse til gensendelse|
|Bemærkninger|Kvitteringen er modtaget med indhold som beskrevet i kvitteringsstandarden|

## S.TC3.A2 Modtag negativ kvittering (ACK AR)

|**S.TC3.A2**|**Modtag negativ kvittering (ACK AR) pga. invalidt indhold** |
| :- | :- |
|Reference til use case som denne use case er et alternativ til|S.TC3 Modtag kvittering (ACK AA)|
|Handlinger|1. Systemaktør henter kvitteringsmeddelelse i Fagsystemets tekniske indbakke og persisterer den i systemet|
||2. Systemaktør evaluerer kvitteringsmeddelelsen teknisk valid ved brug af Kvitteringsregler|
||3. Systemaktør konstaterer, at det er en negativ kvittering af typen ACK AR|
||4. Systemaktør markerer den oprindelige meddelelse for at være permanent fejlet|
||5. Systemaktør udtrækker metadatainformation fra kvitteringen og lægger denne i Fagsystemets forretningsmæssige indbakke|
|Slutresultat|Systemaktør har markeret den oprindelige meddelelse, som permanent fejlende, og har lagt metadatainformation om dette i Fagsystemets forretningsmæssige indbakke. |
|Bemærkninger|Kvitteringen er modtaget med indhold som beskrevet i kvitteringsstandarden|

## S.TC4 Forventet kvittering ikke modtaget

|**S.TC4**|**Forventet kvittering ikke modtaget**|
| :- | :- |
|Igangsættende aktør|Systemaktør|
|Formål|At Systemaktør håndterer at en teknisk korrekt udformet kvittering ikke er modtaget|
|Startbetingelser/forudsætninger|Kommunikationsnetværket har ikke lagt en kvitteringsmeddelelse i Fagsystemets tekniske indbakke og kvitteringens timer er udløbet|
|Igangsættende hændelse|Systemaktør registrerer, at der ikke er modtaget en kvitteringsmeddelelse i Fagsystemets tekniske indbakke|
|Handlinger|1. Systemaktør antager ved manglende modtagelse af kvittering, at den oprindelige meddelelse ikke er blevet modtaget.|
||2. Systemaktør markerer den oprindelige meddelelse til gensendelse.|
|Slutresultat|Systemaktør har markeret den oprindelige meddelelse for ikke at være modtaget og markeret den oprindelige meddelelse til gensendelse|
|Bemærkninger||

# Regler for systemerne, som use casene beror på

## Meddelelsesregler

|**ID**|**Regel**|
| :- | :- |
|MR1.S|Der skal altid anmodes om kvittering på en FHIR-meddelelse|
|MR2.S|En meddelelse markeres som sendt og modtaget, når der er modtaget en ACK AA kvittering|
|MR3.S|En meddelelse markeres som fejlet, når der er modtaget en negativ Ack AR kvittering|
|MR4.S|En meddelelse markeres som fejlet, når der er modtaget en negativ ACK AE kvittering|
|MR5.R|En meddelelse må forsøges gensendt 3 gange ved modtagelse af en ACK AE Kvittering|
|MR6.R|En meddelelse må forsøges gensendt 3 gange ved manglende modtagelse af en Kvittering|
|MR7.R|En meddelelse består altid af en konvolut og et brev. Konvolutten indeholder altid en KonvolutId og KonvolutTid. Brevet indeholder altid et BrevId og en BrevTid|
|MR8.R|En meddelelse, der gensendes, skal altid opdateres med et nyt tidsstempel = Konvoluttid og en ny identifier = KonvolutId |
|MR9.R|En meddelelse er en dublet, hvis den indeholder samme MessageHeader.Id som en tidligere modtaget meddelelse|

## Kvitteringsregler

|**ID**|**Regel**|
| :- | :- |
|KR1.R|Der skal altid kvitteres på en FHIR-meddelelse|
|KR2.R|Der må aldrig kvitteres på en kvitteringsmeddelelse|
|KR3.R|Hvis der ikke findes fejl under modtagelse af en meddelelse, kvitteres der positivt med ACK AA|
|KR4.R|Hvis der sker en teknisk fejl i modtagersystemet under modtagelse af en meddelelse, kvitteres der negativt med ACK AE|
|KR5.R|Hvis en meddelelse validerer negativt mod standardens profilering, kvitteres der negativt med Ack AR|
|KR6.S|Hvis en kvittering på en meddelelse ikke er modtaget inden 30 minutter, markeres den originale meddelelse til gensendelse.|

## Fejltilstande

|**ID**|**Regel**|
| :- | :- |
|F1.S|Hvis en meddelelse er afsendt/gensendt 3 gange uden at modtage kvittering, sættes meddelelsen i fejltilstand, og afsender skal håndtere problemet uden at bruge videre meddelelseshåndtering.|
|F2.S|Hvis en meddelelse er afsendt/gensendt 3 gange uden at modtage korrekt kvittering, sættes meddelelsen i fejltilstand, og afsender skal håndtere problemet uden at bruge videre meddelelseshåndtering.|
|F3.R|Hvis en meddelelse er modtaget 3 gange, selvom der er afsendt korrekt kvittering, sættes kvitteringen på meddelelsen i fejltilstand, og modtager skal håndtere problemet uden at bruge videre meddelelseshåndtering.|

## Meddelelsestilstand

|**Tilstand**|**Beskrivelse**|
| :- | :- |
|Afventer kvittering|Meddelelsen er sendt, men afventer kvittering|
|Kvitteret|Meddelelsen er sendt og ACK AA kvittering modtaget|
|Fejlet|Meddelelsen er sendt og ACK AE fejlkvittering modtaget, oprindelig meddelelse kan gensendes|
|Permanent fejlende|- Meddelelsen er sendt og fejlkvittering af ACK AR modtaget, oprindelig meddelelse kan ikke gensendes, da den er markeret som havende en teknisk fejl- Kvittering på meddelelse er ikke modtaget, efter at meddelelsen har været gensendt 3 gange|

[^1]: Use casene er udarbejdet med inspiration fra [KOMBIT’s metodehåndbog for use cases](https://www.kombit.dk/metodeh%C3%A5ndb%C3%B8ger)