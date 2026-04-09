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
| `Personal_NPI *`                            | Individual (Type 1) NPI                   | Required                  |
| `personal_last_name`                        | Provider last name                        |                           |
| `Organizational_NPI *`                      | Organizational (Type 2) NPI               | Required if available     |
| `organization_name`                         | Organization name                         |                           |
| `Service Address Line1`                     | Primary service location (street address) | No names                  |
| `Service Address Line2`                     | Address line 2                            |                           |
| `Service Address City`                      | City                                      |                           |
| `Service Address State`                     | State (2-letter code)                     |                           |
| `Service Address zip code`                  | ZIP code                                  | Prefer 9 digits           |
| `Service Address country code`              | Country code (if outside US)              |                           |
| `is_currently_practicing *`                 | Whether clinician is currently practicing | `1 = yes`, `0 = no`       |
| `FHIR_Endpoint_URL *`                       | FHIR endpoint URL                         | Required                  |
| `FHIR_Endpoint_Type`                        | Endpoint type                             | e.g., General, Scheduling |
| `FHIR_Endpoint_SMART_Capabilities_URL`      | SMART capabilities endpoint               | URL or blank              |
| `FHIR_Endpoint_Developer_Documentation_URL` | Public developer docs                     | Must not require login    |
| `FHIR_Endpoint_Developer_Signup_URL`        | Developer signup page                     |                           |
| `FHIR_Endpoint_Swagger_URL`                 | Swagger definition                        |                           |
| `FHIR_Endpoint_OpenAPI_URL`                 | OpenAPI definition                        |                           |
| `FHIR_General_Sandbox_URL`                  | Vendor-level sandbox                      |                           |
| `FHIR_Specific_Sandbox_Endpoint_URL`        | Instance-specific sandbox                 |                           |


## Submission Flexibility

To avoid delays:

* If historical affiliation data is not ready:

  * Submit with all values set to `1` for `is_currently_practicing`

* If detailed FHIR metadata is not ready:

  * Submit with:

    * Only `FHIR_Endpoint_URL`
    * Leave additional endpoint-related fields blank



## Notes

* This dataset enables **short- to medium-term ingestion into the NPD**
* Priority is on **timely submission over completeness**

### Licensing

All public releases of NPD-related code and data are:

* **Open Source / Public Domain**

See: [https://github.com/DSACMS/npd](https://github.com/DSACMS/npd)



Source: 
