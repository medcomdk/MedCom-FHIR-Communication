#  Governance for displaying MedCom FHIR Messages

All elements marked as MustSupport **SHALL** be presented or easily accessed on the display of the reader of a received message.

The message as a whole coherent object **SHALL** be present for easy access for the reader.

The receiving application **SHALL** be able to show only relevant information for the different receiver roles in the receiving organization, eg. only persons in clinical roles **SHALL** be able to read clinical content

All applications **MUST** be able to print relevant messages, due to Danish legislation. Previously, MedCom has tested this, but it is now up to the vendors to ensure they support this. When printing the relevant message the patient's Civil Registration Number (Danish: CPR) **SHALL** be present on each printed page.