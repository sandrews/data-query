## Argonaut Data Query Implementation Guide

The Argonaut Data Query Implementation Guide is based upon the core [FHIR] API and documents the:

 - Security and Authorization
 - Data element query of the ONC Common Clinical Data Set
 - Document query of static documents

#### Use Cases

This specification describes four use cases and sets search expectations for each. For complete details and background, see [Use Cases] for the Argonaut Project.

1.  Patient  uses  provider-approved  web  application  to  access  health  data
2.  Patient  uses  provider-­approved  mobile  app  to  access  health  data
3.  Clinician  uses  provider­-approved  web  application  to  access  health  data
4.  Clinician  uses  provider­-approved  mobile  app  to  access  health  data

Note, the Common MU Data Set referenced in the Use Cases is now the ONC 2015 Common Clinical Data Set .

[Use Cases]: http://argonautwiki.hl7.org/images/e/ec/Argonaut_UseCasesV1-1.pdf

#### Security

-----------------------------------------------

Argonaut uses SMART on FHIR authorization for apps that connect to EHR data. For details, see [SMART on FHIR Authorization Guide] and the [Argonaut Sprint Definitions].

  [SMART on FHIR Authorization Guide]: http://fhir-docs.smarthealthit.org/argonaut-dev/authorization/
  [Argonaut Sprint Definitions]: https://github.com/argonautproject/implementation-program/wiki

#### Data Element Query

  ----------------------

  The Argonaut data element query IGs are intended to meet the 2015 Edition certification criterion for Patient Selection 170.315(g)(7) and Application Access – Data Category Request 170.315(g)(8). They were created for each of the 2015 Edition Common Clinical Data Set. Where applicable they are based on the HL7 U.S. [Data Access Framework] (DAF) FHIR DSTU2 Implementation Guide. However, the Argonaut use case and requirements per resource are a subset of those of the DAF implementation guide.

  The table below lists the FHIR Resources used for the corresponding 2015 Edition Common Clinical Data Set (CCDS) Data elements:

  No| CCDS Data Element | FHR Resource
  ---|---|---|
  (1) |  Patient Name | Patient
  (2) |  Sex | Patient
  (3) |  Date of birth | Patient
  (4) |  Race | Patient
  (5) |  Ethnicity | Patient
  (6) |  Preferred language | Patient
  (7) |  Smoking status | Observation
  (8) |  Problems | Condition
  (9) |  Medications | Medication, MedicationStatement, MedicationOrder
  (10) |  Medication allergies | AllergyIntolerance
  (11) |  Laboratory test(s) | Observation, DiagnosticReport
  (12) |  Laboratory value(s)/result(s) | Observation, DiagnosticReport
  (13) |  Vital signs | Observation
  (14) |  (no longer required) | -
  (15) |  Procedures | Procedure
  (16) |  Care team member(s) | CarePlan
  (17) |  Immunizations | Immunization
  (18) |  Unique device identifier(s) for a patient’s implantable device(s) | Device
  (19) |  Assessment and plan of treatment | CarePlan
  (20) |  Goals | Goal
  (21) |  Health concerns | Condition

*Note on Searches based on a date or date range:*

  Allergies, Immunizations, Medications, Problems and Health Concerns, UDI, Smoking Status do not require a date range search since a system should return all relevant resources.

  Date range search requirements are included in the Quick Start section for the following resources - Vital Signs, Laboratory Results, Goals, Procedures, and Assessment and Plan of Treatment.


 [Data Access Framework]: http://hl7.org/fhir/daf/daf.html

#### Document Query

 ------------------

 For the Argonaut Document Query Implementation guide, we are focused on the provider and patient access and retrieval of a patient's existing C-CDA formats - specifically, transition of care and patient summary CCDs required for Meaningful Use.  However other document types like PDF documents can be retrieved too. These are exposed in FHIR using a [DocumentReference Resource] to index/search for them. This guide provides the minimal requirements to fetch a URL link to either a) patient's existing documents which have been indexedlike C-CDA or b) a “virtual” documents such as a CCD that could be created “on-demand”.

 The Document itself can be subsequently retrieved using the link provided from the DocumentQuery search results. The link could be ,for example, a [FHIR endpoint] to a [Binary Resource] or some other document repository. The details of how to retrieve the document are not covered in this guide.

 **Use Case**

 Patient or Provider search for a patient's Documents

 **Example Search**

 -   Locate a patient's [CCD document] from a recent or current encounter

 **Assumptions and Preconditions**

 -   Initial search for a reference to a document instead of documents itself ( retrieval of actual document is a two-step process)
 -   Documents may or may not already exist and be indexed prior to the search
 -   Document references may be created “on-demand” when requested
 -   Documents may be created “on-demand” when requested
 -   Details of document retrieval is out of scope


[DocumentReference Resource]: http://hl7.org/fhir/DSTU2/documentreference.html
[FHIR endpoint]: http://hl7.org/fhir/http.html
[Binary Resource]: http://hl7.org/fhir/binary.html
[CCD document]: https://en.wikipedia.org/wiki/Continuity_of_Care_Document
[FHIR]: http://hl7.org/fhir