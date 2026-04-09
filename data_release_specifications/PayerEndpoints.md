# CSV Payer FHIR Endpoint Data

## Overview

Health plans are required to publish multiple types of FHIR endpoints under:

* **CMS-9115-F**
* **CMS-0057-F**

In total, there are **at least five required endpoint types**, plus one optional type.



## Payer FHIR Endpoint Types

### Required by existing regulations

* **Provider Directory API** (CMS-9115-F)
* **Patient Access API** (CMS-9115-F, CMS-0057-F)
* **Payer-to-Payer API** (CMS-9115-F, CMS-0057-F)
* **Provider Access API** (CMS-0057-F)
* **Prior Authorization API** (CMS-0057-F)

### Optional

* **Formulary API** (may be publicly accessible without authentication)



## File Requirements

* Format: **CSV**
* Structure: One row per **payer endpoint**
* Some fields are **conditionally required** (see notes below)



## CSV Schema

| Column                 | Description                         | Notes                                    |
| - | -- | - |
| `enumeration_approach` | Identifier type used in this row    | e.g., HIOS, UUID                         |
| `Payer ID`             | CMS-issued payer identifier or UUID | **Required**                             |
| `Payer LBN`            | Legal Business Name                 | **Required**                             |
| `Plan ID`              | Plan identifier                     | Required if multiple endpoints per payer |
| `Plan Name`            | Plan name                           | Required if multiple endpoints per payer |
| `FHIR_URL`             | FHIR endpoint URL                   | **Required**                             |
| `FHIR_URL_vendor`      | Vendor name                         | **Required**                             |
| `FHIR_URL_Type`        | Endpoint type                       | See values below                         |
| `Sandbox FHIR URL`     | Sandbox/testing endpoint            | Optional                                 |
| `Documentation URL`    | Developer documentation             | Optional                                 |
| `Swagger URL`          | Swagger definition                  | Optional                                 |
| `Open API URL`         | OpenAPI definition                  | Optional                                 |
| `Well-known URL`       | SMART-on-FHIR well-known endpoint   | Optional                                 |



## Valid Values: `FHIR_URL_Type`

* `provider_directory_api`
* `patient_access_api`
* `payer_to_payer_api`
* `provider_access_api`
* `prior_authorization_api`
* `formulary_api`



## Notes

* Use **Plan-level fields** (`Plan ID`, `Plan Name`) only when:

  * Different plans have different FHIR endpoints

* Otherwise:

  * Leave them blank

* UUIDs may be used where CMS-issued identifiers are unavailable

* This specification is **evolving** and will likely change based on feedback

👉 Please share feedback in Slack

