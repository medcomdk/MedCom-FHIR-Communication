# &nbsp; &nbsp;

## Table of content

* [governance-of-terminologies](#governance-of-terminologies)
  * [codesystems](#codesystems)
  * [valuesets](#valuesets)
  * [conceptmaps](#conceptmaps)

## Governance of Terminologies

All CodeSystems, ValueSets and ConceptMaps will have a status, and a latest changed date. The status indicates if the CodeSystems, ValueSets or ConceptMaps is draft, active, or retired. If the status is active the terminology is ready for use.

No updates will be made without consulting relevant working groups beforehand.

### CodeSystems

No code in a CodeSystem will be deleted, nor will the meaning of a code be changed. Incompatible versions of a CodeSystem will have a unique name.
However, codes in CodeSystems may be deprecated with a deprecation date and new codes may be added to the CodeSystem. In both cases will the version and date for latest change be updated.

### ValueSets

Some ValueSets are intensional defined, meaning that all codes from a CodeSystem is included. Whenever the CodeSystem is updated, so is the ValueSet. For intensional defined ValueSets, there will always only be one active ValueSets, with a date for latest update. ValueSets used to describe the content of a message, such as [MedComCareCommunicationCategoryCodes](https://build.fhir.org/ig/medcomdk/dk-medcom-terminology/ValueSet-medcom-careCommunication-categories.html)

Other ValueSets are extensional defined, meaning that means that codes from CodeSystems are explicitly listed in each ValueSet. Therefore, will ValueSets not automatically be expanded when a CodeSystem is, it requires a change in the ValueSet. These ValueSets are used to describe the codes used for routing of a message and the logical setup within a system, such as [MedComHospitalNotificationMessageActivityCodes](https://build.fhir.org/ig/medcomdk/dk-medcom-terminology/ValueSet-medcom-hospitalNotification-messageActivities.html). There may be more than one active ValueSet, as changes may take time to implement.

In exceptional cases, it is possible to specify when defining a ValueSet that must not be changed or versioned.

### ConceptMaps

As for ValueSets, the ConceptMaps may be more or less static, where the once used for messaging purposes will rarely change, and the once used to describe the content of a message may change more frequently.

A ConceptMap is valid until the date of a newer version of this ConceptMap is reached, then the newer version is valid. If a code in a CodeSystem is deprecated, a new version of the ConceptMaps is created, which will be valid.
