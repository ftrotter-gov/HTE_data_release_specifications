# Payer sourced Provider Data Without Endpoints


## Overview

Long term, the National Provider Directory (NPD) will retrieve data directly from EHR systems and CMS-aligned Health Technology Ecosystem (HTE) data networks via FHIR APIs. This data should eventually be accessible without authentication through organizational FHIR endpoints.

In the short term, we need accurate data describing:

* How to reach organizations and clinicians via FHIR endpoints
* Historical clinician affiliations (to support patient search)

This document defines a **lightweight CSV specification** to support rapid data submission for NPD ingestion.



## Data Model

* Each row represents a **PractitionerRole-level record**
* Include:

  * Active clinicians
  * Clinicians who practiced at the organization within the past **10 years** (if available)

### Inclusion Criteria

Include a row when:

* A clinician (Personal NPI) has billed **more than 10 patients** under an Organizational NPI

Notes:

* A clinician may appear **multiple times** (once per organization)
* If no Organizational NPI exists, leave that field blank



## File Specifications

* Format: **RFC 4180-compliant CSV**
* Use **exact column headers** listed below
* Fields marked with `*` are **required**



## CSV Schema

| Column                                      | Description                       | Notes                     |
| - |  | - |
| `submitter_name`                            | Submitting organization           | e.g., Epic, Cerner        |
| `submitting_for_name`                       | Organization represented          | e.g., hospital system     |
| `Personal_NPI *`                            | Individual (Type 1) NPI           | One per row               |
| `personal_last_name`                        | Provider last name                |                           |
| `Organizational_NPI *`                      | Organizational (Type 2) NPI       | Required if available     |
| `organization_name`                         | Organization name                 |                           |
| `Service Address Line1`                     | Primary service location (street) | No names                  |
| `Service Address Line2`                     | Address line 2                    |                           |
| `Service Address City`                      | City                              |                           |
| `Service Address State`                     | State (2-letter code)             |                           |
| `Service Address zip code`                  | ZIP code                          | Prefer 9 digits           |
| `Service Address country code`              | Country (if outside US)           |                           |
| `is_currently_practicing *`                 | Current affiliation               | `1 = yes`, `0 = no`       |
| `FHIR_Endpoint_URL *`                       | FHIR endpoint                     | Required                  |
| `FHIR_Endpoint_Type`                        | Endpoint type                     | e.g., General, Scheduling |
| `FHIR_Endpoint_SMART_Capabilities_URL`      | SMART capabilities URL            | Optional                  |
| `FHIR_Endpoint_Developer_Documentation_URL` | Public documentation              | No login required         |
| `FHIR_Endpoint_Developer_Signup_URL`        | Developer signup page             | Optional                  |
| `FHIR_Endpoint_Swagger_URL`                 | Swagger definition                | Optional                  |
| `FHIR_Endpoint_OpenAPI_URL`                 | OpenAPI definition                | Optional                  |
| `FHIR_General_Sandbox_URL`                  | Vendor sandbox                    | Optional                  |
| `FHIR_Specific_Sandbox_Endpoint_URL`        | Instance sandbox                  | Optional                  |



## Submission Flexibility

To avoid delays:

* If historical data is not ready:

  * Set all `is_currently_practicing = 1`

* If detailed endpoint metadata is not ready:

  * Submit only `FHIR_Endpoint_URL`
  * Leave additional URL fields blank



## Notes

* Prioritize **timely submission over completeness**
* This format supports **short- to medium-term ingestion into the NPD**

### Licensing

All NPD code and data are released as:

* **Open Source / Public Domain**

[https://github.com/DSACMS/npd](https://github.com/DSACMS/npd)



