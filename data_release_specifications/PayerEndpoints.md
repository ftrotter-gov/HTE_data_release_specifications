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
| `payer_id`             | CMS-issued payer identifier or UUID | **Required**                             |
| `payer_lbn`            | Legal Business Name                 | **Required**                             |
| `plan_id`              | Plan identifier                     | Required if multiple endpoints per payer |
| `plan_name`            | Plan name                           | Required if multiple endpoints per payer |
| `fhir_url`             | FHIR endpoint URL                   | **Required**                             |
| `fhir_url_vendor`      | Vendor name                         | **Required**                             |
| `fhir_url_type`        | Endpoint type                       | See values below                         |
| `sandbox_fhir_url`     | Sandbox/testing endpoint            | Optional                                 |
| `documentation_url`    | Developer documentation             | Optional                                 |
| `swagger_url`          | Swagger definition                  | Optional                                 |
| `open_api_url`         | OpenAPI definition                  | Optional                                 |
| `well_known_url`       | SMART-on-FHIR well-known endpoint   | Optional                                 |

> Note: All column names are strict `snake_case` (lowercase, numbers, and underscores only).



## Valid Values: `fhir_url_type`

* `provider_directory_api`
* `patient_access_api`
* `payer_to_payer_api`
* `provider_access_api`
* `prior_authorization_api`
* `formulary_api`



## Notes

* Use **Plan-level fields** (`plan_id`, `plan_name`) only when:

  * Different plans have different FHIR endpoints

* Otherwise:

  * Leave them blank

* UUIDs may be used where CMS-issued identifiers are unavailable

* This specification is **evolving** and will likely change based on feedback

👉 Please share feedback in Slack

