# Governance of Terminologies

All CodeSystems, ValueSets and ConceptMaps will have a status, version, and a latest changed date. The status indicates if the CodeSystems, ValueSets or ConceptMaps is draft, active, or retired. If the status is active the terminology is ready for use. 

There may be multiple versions of the same CodeSystems, ValueSets or ConceptMaps, but only one will be active. Version and date will together indicate the newest version. Under the ‘Previous versions’ the historical changes to the CodeSystems, ValueSets or ConceptMaps can be seen [Work in progress]. 

No updates will be made without consulting relevant working groups beforehand. 

## CodeSystems

No code in a CodeSystem will be deleted, nor will the meaning of a code be changed. Incompatible versions of a CodeSystem will have a unique name.   
However, codes in CodeSystems may be deprecated with a deprecation date and new codes may be added to the CodeSystem. In both cases will the version and date for latest change be updated. 

## ValueSets

As a starting point all ValueSets are extensionally defined, which means that codes from CodeSystems are explicitly listed in each ValueSet. Therefore, will ValueSets not automatically be expanded when a CodeSystem is, it requires a change in the ValueSet.

A ValueSet may be more or less static. ValueSets used for messaging purposes will rarely change, whereas ValueSets used to describe the content of a message may change more frequently, depending on the requirement of the project. No changes will be made without consulting relevant working groups. In exceptional cases, it is possible to specify when defining a value set that it must not be changed or versioned.

Value Sets are valid until the date of a newer version of this ValueSet is reached, then the newer version is valid. If a code in a CodeSystem is deprecated, a new version of the ValueSet is created, which will be valid.

## ConceptMaps

As for ValueSets, the ConceptMaps may be more or less static, where the once used for messaging purposes will rarely change, and the once used to describe the content of a message may change more frequently. 

A ConceptMap is valid until the date of a newer version of this ConceptMap is reached, then the newer version is valid. If a code in a CodeSystem is deprecated, a new version of the ConceptMaps is created, which will be valid.
