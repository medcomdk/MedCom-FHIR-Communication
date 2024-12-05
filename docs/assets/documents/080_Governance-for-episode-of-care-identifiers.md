# Governance for episode of care identifiers

## General in FHIR messages
When relevant it is possible to include an episode of care identifier, it is contained in the [MedComCoreEncounter profile](https://medcomfhir.dk/ig/core/StructureDefinition-medcom-core-encounter.html) or a specialization of this profile. The episode of care identifier can be a locally defined UUID for the specific admission/contact or it can be an LPR3 identifier. The identifier is used for linking messages exchanged during a specific message flow. When the episode of care identifier is received e.g. in a ReportOfAdmission (Danish: Indlæggelsesrapport), ProgressOfCarePlan (Danish: Plejeforløbsplan), HospitalNotification (Danish: Advis om sygehusophold) or a previous CareCommunication (Danish: Korrespondancemeddelelse), it **SHALL** be returned in the following message. If a correspondance, e.g. CareCommunication, concerns an admission with an episode of care identifier, the identifier can be included in the initial message.

**In case only one episode of care identifier is included in the initial message, either a locally defined UUID for the specific admission/contact or an LPR3 identifier:** The following messages exchanged **SHALL** return this episode of care identifier, regardless of whether it is a locally defined UUID or an LPR3 identifier. If more identifiers are subsequently added, these can be ignored (or returned if possible).

**In case more episode of care identifiers are included in the initial message:** The following messages exchanged **SHALL** return the locally defined UUID for the specific admission/contact. The other identifiers can be ignored (or returned if possible).

### System for locally defined episode of care identifiers
When a locally defined identifier for the specific admission/contact is included in a message, a system for the identifier shall also be included. The system is used to destinguish between the LPR3 identifier and the locally defined identifier. In the latter case, a new slice in the Encounter.episodeOfCare shall be added and the Encounter.episodeOfCare.identifier.system shall be added. The datatype of the system is Unique Resource Identifier Reference (uri), meaning that the system **SHALL** be absolut or relative unique. It is recommended to use SOR-endpoint, which is also definied in the MessageHeader.source.endpoint. This is shown in the XML-snippet and examples below.

```xml
 <episodeOfCare>
    <identifier>
      <system value="https://sor2.sum.dsdn.dk/#id=265161000016000"/>
      <value value="bd481c38-a921-11ed-afa1-0242ac120002"/>
    </identifier>
  </episodeOfCare>
```

## General use in OIOXML end EDIFACT messages
The general use of an episode of care identifier in OIOXML and EDIFACT messages is described in the <a href="http://svn.medcom.dk/svn/releases/Standarder/National%20Sygehus-Kommunesamarbejde/1.0.3/Bilag/Flow%20hjemmepleje-sygehus.pdf" target="_blank">document for municipality and hospital messages (pdf). The document is in Danish.</a>


## Discrepancy between FHIR and OIOXML/EDIFACT
In FHIR messages all episode of care identifiers **SHALL** be a UUID with a hyphen (-), as displayed in the example above. Due to a limitation in the OIOXML/EDIFACT messages all episode of care identifiers **SHALL** be a UUID without a hyphen, hence only numbers and characters. 

It is the systems responsibility to keep track of episode of care identifiers with and without hyphen. 