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
| `personal_npi`                              | Individual (Type 1) NPI           | One per row               |
| `personal_last_name`                        | Provider last name                |                           |
| `organizational_npi`                        | Organizational (Type 2) NPI       | Required if available     |
| `organization_name`                         | Organization name                 |                           |
| `service_address_line1`                     | Primary service location (street) | No names                  |
| `service_address_line2`                     | Address line 2                    |                           |
| `service_address_city`                      | City                              |                           |
| `service_address_state`                     | State (2-letter code)             |                           |
| `service_address_zip_code`                  | ZIP code                          | Prefer 9 digits           |
| `service_address_country_code`              | Country (if outside US)           |                           |
| `is_currently_practicing`                   | Current affiliation               | **Required**; `1 = yes`, `0 = no` |
| `fhir_endpoint_url`                         | FHIR endpoint                     | Required                  |
| `fhir_endpoint_type`                        | Endpoint type                     | e.g., General, Scheduling |
| `fhir_endpoint_smart_capabilities_url`      | SMART capabilities URL            | Optional                  |
| `fhir_endpoint_developer_documentation_url` | Public documentation              | No login required         |
| `fhir_endpoint_developer_signup_url`        | Developer signup page             | Optional                  |
| `fhir_endpoint_swagger_url`                 | Swagger definition                | Optional                  |
| `fhir_endpoint_openapi_url`                 | OpenAPI definition                | Optional                  |
| `fhir_general_sandbox_url`                  | Vendor sandbox                    | Optional                  |
| `fhir_specific_sandbox_endpoint_url`        | Instance sandbox                  | Optional                  |



## Submission Flexibility

To avoid delays:

* If historical data is not ready:

  * Set all `is_currently_practicing = 1`

* If detailed endpoint metadata is not ready:

  * Submit only `fhir_endpoint_url`
  * Leave additional URL fields blank



## Notes

* Prioritize **timely submission over completeness**
* This format supports **short- to medium-term ingestion into the NPD**

### Licensing

All NPD code and data are released as:

* **Open Source / Public Domain**

[https://github.com/DSACMS/npd](https://github.com/DSACMS/npd)



