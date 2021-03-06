# Patient API

## Patient

### Overview
The patient resource contains information about the demographics of a patient.

### Fields
| Name | Description | Type |
| ---- | ---------- | ----------- |
| identifier | The unique value assigned to each patient which discerns them from all others. It can be the patient's unique identifier or the patient’s Nextech chart number | [Identifier](https://www.hl7.org/fhir/datatypes.html#Identifier) |
| race | The race of the patient | [Race](https://www.hl7.org/fhir/v3/Race/cs.html) |
| ethnicity | The ethnicity of the patient | [Ethnicity](https://www.hl7.org/fhir/v3/Ethnicity/cs.html) |
| name | Names of the patient | [HumanName](https://www.hl7.org/fhir/datatypes.html#HumanName) |
| telecom | Contact details for the patient | [ContactPoint](https://www.hl7.org/fhir/datatypes.html#ContactPoint) |
| gender | The gender of the patient | [AdministrativeGender](https://www.hl7.org/fhir/valueset-administrative-gender.html) |
| birthDate | The date of birth of the patient | [date](https://www.hl7.org/fhir/datatypes.html#date) |
| address | Addresses associated with the patient | [Address](https://www.hl7.org/fhir/datatypes.html#Address) |
| communication | A list of Languages which may be used to communicate with the patient about his or her health | [BackboneElement](https://www.hl7.org/fhir/backboneelement.html) |

### Example
<pre class="center-column">{
  "resourceType": "Patient",
  "id": "ad2085b5-b974-401d-bfcb-3b865109fd35",
  "extension": [
    {
      "url": "http://hl7.org/fhir/v3/Race",
      "valueCodeableConcept": {
        "coding": [
          {
            "system": "http://hl7.org/fhir/v3/Race",
            "code": "2106-3"
          }
        ],
        "text": "Caucasian"
      }
    },
    {
      "url": "http://hl7.org/fhir/v3/Ethnicity",
      "valueCodeableConcept": {
        "coding": [
          {
            "system": "http://hl7.org/fhir/v3/Ethnicity",
            "code": "2186-5"
          }
        ],
        "text": "Not Hispanic or Latino"
      }
    }
  ],
  "identifier": [
    {
      "use": "official",
      "value": "ad2085b5-b974-401d-bfcb-3b865109fd35"
    },
    {
      "use": "usual",
      "value": "4471"
    }
  ],
  "name": [
    {
      "text": "Jane L Smith",
      "family": "Smith",
      "given": [
        "Jane",
        "L"
      ]
    }
  ],
  "telecom": [
    {
      "system": "email",
      "value": "jsmith@email.com"
    },
    {
      "system": "phone",
      "value": "346-555-3682"
    }
  ],
  "gender": "female",
  "birthDate": "1968-02-04",
  "address": [
    {
      "use": "home",
      "type": "both",
      "line": [
        "3485 Forest Lane",
        "Apt 324"
      ],
      "city": "Houston",
      "state": "TX",
      "postalCode": "77014"
    }
  ],
  "communication": [
    {
      "language": {
        "coding": [
          {
            "system": "BCP-47",
            "code": "en"
          }
        ],
        "text": "English"
      },
      "preferred": true
    }
  ]
}
</pre>
&nbsp;
### *Search*
Searches for all patients matching the given search criteria. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria.

### HTTP Request 
`GET /Patient?{parameters}`

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| family | query | The family (last) name of the patient | No | string |
| given | query | The given (first) name of the patient | No | string |
| birthdate | query | The patient's date of birth formatted as YYYY-MM-DD | No | dateTime |
| phone | query | The patient's phone number which will be matched against any phone number (home, cell, etc.) | No | string |
| email | query | The patient's email address | No | string |
| address-city | query | The city of the patient's address | No | string |
| address-state | query | The state of the patient's address | No | string |
| address-postalcode | query | The postal (zip) code of the patient's address | No | string |
| identifier | query | The unique value assigned to each patient which discerns them from all others. It can be the patient's unique identifier or the patient’s Nextech chart number | No | string |

#### Example: Get the patient of a specific chart number

<pre class="center-column">
GET https://api.nextech.com/Patient/12345
</pre>

#### Example: Get all patients who live within a specific zip code

<pre class="center-column">
GET https://api.nextech.com/Patient?address-postalcode=12345
</pre>

#### Example: Get all patients with birth dates between and including 1/1/1981 through 5/31/1981

<pre class="center-column">
GET https://api.nextech.com/Patient?birthDate=ge1981-01-01&birthDate=lt1981-06-01
</pre>
&nbsp;

### Patient ID Search
Attempts to find a single patient that matches the given search criteria and if
successful returns only that patient's unique identifier.   

_At least one of query parameters is required to perform a search._

### HTTP Request 
`GET /Patient/ID?{parameters}` 

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| family | query | The family (last) name of the patient | No | string |
| given | query | The given (first) name of the patient | No | string |
| birthdate | query | The patient's date of birth formatted as YYYY-MM-DD | No | dateTime |
| phone | query | The patient's phone number which will be matched against any phone number (home, cell, etc.) | No | string |
| email | query | The patient's email address | No | string |
| address-city | query | The city of the patient's address | No | string |
| address-state | query | The state of the patient's address | No | string |
| address-postalcode | query | The postal (zip) code of the patient's address | No | string |
| identifier | query | The unique value assigned to each patient which discerns them from all others. It can be the patient's unique identifier or the patient’s Nextech chart number | No | string |

#### Example: Get the unique identifier of a patient given first name, last name, and birthdate

<pre class="center-column">
GET https://api.nextech.com/Patient/ID?family=Smith&given=John&birthDate=eq1972-04-21
</pre>
&nbsp;

## Allergy Intolerance
Get a bundle of allergies for a single patient   

_RESTful searching for allergies by last update date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne._

### HTTP Request
`GET /Patient/{patientUID}/AllergyIntolerance`

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of allergy last update date filters | No | array |


## CCDA Summary
Get a CCDA summary document for the specified patient.

### HTTP Request 
`GET /Patient/{patientUid}/Binary/$autogen-ccd-if` 

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUid | path | The patient's unique identifier (can be found by patient ID search method) | Yes | string |
| start | query | The start date for which the CCD should be generated (if not specified then all records              starting with the patient's first visit are included) | No | dateTime |
| end | query | The end date for which the CCD should be generated (if not specified then all records              through the patient's latest visit are included) | No | dateTime |


## Care Plan
Get a bundle of care plans for a single patient.   

_RESTful searching for care plans by visit date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne._

### HTTP Request 
`GET /Patient/{patientUID}/CarePlan` 

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of visit date filters | No | array |


## Clinical Impression
Get a bundle of clinical impressions for a patient.   

_RESTful searching for clinical impressions by visit date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne._

### HTTP Request 
`GET /Patient/{patientUID}/ClinicalImpression` 

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of visit date filters | No | array |

## Condition
Get a bundle of conditions for a single patient.   

_RESTful searching for conditions by onset date and abatement date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne._

### HTTP Request 
`GET /Patient/{patientUID}/Condition` 

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| onset-date | query | The collection of condition onset date filters | No | array |
| abatement-date | query | The collection of condition abatement date filters | No | array |

## Device
Get a bundle of devices for a patient.

### HTTP Request 
`GET /Patient/{patientUID}/Device` 

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of device effective date filters | No | array |

## Encounter
Get a bundle of encounters for a single patient.   

_RESTful searching for conditions by encounter date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne._

### HTTP Request 
`GET /Patient/{patientUID}/Encounter` 

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of encounter date filters | No | array |


## Goal
Get a bundle of goals for a single patient.   

_RESTful searching for goals by visit date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne._

### HTTP Request 
`GET /Patient/{patientUID}/Goal` 

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of visit date filters | No | array |


## Immunization
Get a bundle of immunizations for a single patient.   

_RESTful searching for current immunizations by administration date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne._

### HTTP Request 
`GET /Patient/{patientUID}/Immunization` 

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of current immunization administration date filters | No | array |


## Medication Dispensement
Get a bundle of medication dispensements for a single patient.   

_RESTful searching for medication dispensements by preparation date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne._

### HTTP Request 
`GET /Patient/{patientUID}/MedicationDispense` 

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| whenprepared | query | The collection of preparation date filters | No | array |


## Medication Statements
Get a bundle of medication statements for a single patient.   

_RESTful searching for medication statements by effective date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne._

### HTTP Request 
`GET /Patient/{patientUID}/MedicationStatement` 

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| effective | query | The collection of effective date filters | No | array |


## Observation
Get a bundle of diagnostic observations for a single patient.   

This request requires a category code to search on. The following category codes are supported:
- laboratory
- social-history
- vital-signs

_RESTful searching for observations by date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne._

### HTTP Request 
`GET /Patient/{patientUid}/Observation` 

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUid | path | The unique identifier acquired from the patient search | Yes | string |
| category | query | The category of observation to load | Yes | string |
| date | query | The collection of observation obtained date filters | No | array |


## Procedure
Get a bundle of procedures for a single patient.   

_RESTful searching for procedures by performed date is supported. See https://www.hl7.org/fhir/search.html for instructions on formatting search criteria. The following search prefixes are supported: lt, gt, eq, le, ge, ne._

### HTTP Request 
`GET /Patient/{patientUID}/Procedure` 

### Parameters
| Name | Located in | Description | Required | Type |
| ---- | ---------- | ----------- | -------- | ---- |
| patientUID | path | The unique identifier acquired from the patient search | Yes | string |
| date | query | The collection of procedure performed date filters | No | array |
