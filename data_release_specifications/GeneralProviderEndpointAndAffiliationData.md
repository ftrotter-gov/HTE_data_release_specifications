General Provider Endpoint and Affiliation Data
=========================


## Overview

Long term, the National Provider Directory (NPD) will retrieve data directly from EHR systems and CMS-aligned Health Technology Ecosystem (HTE) [Data Networks](https://www.cms.gov/health-technology-ecosystem/categories), as well as other organizations that have Provider Endpoint data, using FHIR APIs. This data should eventually be accessible without authentication via organizational FHIR endpoints.

In the short term, we need accurate data on:

* How to reach organizations and individual clinicians via FHIR endpoints
* Historical clinician affiliations (to support patient search use cases)

This document defines a **lightweight CSV specification** to enable rapid data submission for NPD ingestion.


## General Guidance

* Each row should correspond to a **PractitionerRole-level record**
* Include:

  * Active clinicians
  * Clinicians who practiced at the organization within the past **10 years** (when possible)

### Inclusion Rule

* If a clinician (Personal NPI) has billed/seen **more than 10 patients** under an Organizational NPI:

  * Include a row for that pairing
* A clinician may appear **multiple times** (once per hosting organization)


## File Contents

* Format: **RFC 4180-compliant CSV**
* Use the exact column headers listed below
* Fields marked with `*` are **Required** to meet this CSV Specification. However, if you have data that does not meet this specification and wish to release it, please contact the NPD Team!


## CSV Schema

| Column                                      | Description                               | Notes                     |
| ------------------------------------------- | ----------------------------------------- | ------------------------- |
| `submitter_name`                            | Organization submitting the CSV           | e.g., Cerner, Epic        |
| `submitting_for_name`                       | Organization represented in the data      | e.g., hospital system     |
| `personal_npi`                              | Individual (Type 1) NPI                   | Required                  |
| `personal_last_name`                        | Provider last name                        |                           |
| `organizational_npi`                        | Organizational (Type 2) NPI               | Required if available     |
| `organization_name`                         | Organization name                         |                           |
| `service_address_line1`                     | Primary service location (street address) | No names                  |
| `service_address_line2`                     | Address line 2                            |                           |
| `service_address_city`                      | City                                      |                           |
| `service_address_state`                     | State (2-letter code)                     |                           |
| `service_address_zip_code`                  | ZIP code                                  | Prefer 9 digits           |
| `service_address_country_code`              | Country code (if outside US)              |                           |
| `is_currently_practicing`                   | Whether clinician is currently practicing | **Required**; `1 = yes`, `0 = no` |
| `fhir_endpoint_url`                         | FHIR endpoint URL                         | Required                  |
| `fhir_endpoint_type`                        | Endpoint type                             | e.g., General, Scheduling |
| `fhir_endpoint_smart_capabilities_url`      | SMART capabilities endpoint               | URL or blank              |
| `fhir_endpoint_developer_documentation_url` | Public developer docs                     | Must not require login    |
| `fhir_endpoint_developer_signup_url`        | Developer signup page                     |                           |
| `fhir_endpoint_swagger_url`                 | Swagger definition                        |                           |
| `fhir_endpoint_openapi_url`                 | OpenAPI definition                        |                           |
| `fhir_general_sandbox_url`                  | Vendor-level sandbox                      |                           |
| `fhir_specific_sandbox_endpoint_url`        | Instance-specific sandbox                 |                           |


## Submission Flexibility

To avoid delays:

* If historical affiliation data is not ready:

  * Submit with all values set to `1` for `is_currently_practicing`

* If detailed FHIR metadata is not ready:

  * Submit with:

    * Only `fhir_endpoint_url`
    * Leave additional endpoint-related fields blank



## Notes

* This dataset enables **short- to medium-term ingestion into the NPD**
* Priority is on **timely submission over completeness**

### Licensing

All public releases of NPD-related code and data are:

* **Open Source / Public Domain**

See: [https://github.com/DSACMS/npd](https://github.com/DSACMS/npd)



Source: 
