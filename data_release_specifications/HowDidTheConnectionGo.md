# CSV FHIR Endpoint Data (HowDidTheConnectionGo)

## Overview

This is a data specification that will allow PHRs, Patient Apps, and other entities that are making FHIR connection requests on behalf of patients to release their success rates on a per-FHIR endpoint basis. If you choose to make such a release. Please let the NPD team at CMS know so that we can integrate your data into the National Provider Directory. 

Long term, we plan to collect information about problematic FHIR endpoints through an FHIR-like API and/or web-based interface.

In the short term, HTE participants can share insights about issues they encounter with FHIR endpoints in real-world usage, using this standard.

## Submission Guidance

* You may submit data in **any format**.
* If you have an existing FHIR endpoint database:

  * Provide a **CSV export**
  * Include a **description of the columns**

### Important

* **Do NOT include any patient PII** in your submission.

## Optional Standard Format

To align with the future feedback API, you may use the following CSV structure.

---

## CSV Schema

| Column                                      | Description                                 | Notes                         |
| ------------------------------------------- | ------------------------------------------- | ----------------------------- |
| `FHIR_scope_g10patientaccess`               | API type                                    | Required                      |
| `FHIR_URL`                                  | FHIR endpoint URL (or `"URL missing"`)      | Required                      |
| `FHIR_URL_vendor`                           | EHR vendor name                             | Required                      |
| `ONPI_sought`                               | Organizational NPI                          | ONPI or blank                 |
| `PNPI_sought`                               | Clinician NPI (if known)                    | PNPI or blank                 |
| `HL7ID_sought`                              | Vendor-listed identifier (if not NPI)       | HL7ID or blank                |
| `provider_name_text`                        | Provider name                               |                               |
| `reporting_period_start_date`               | Reporting start date                        |                               |
| `reporting_period_end_date`                 | Reporting end date                          |                               |
| `endpoint_total_count`                      | Total requests to endpoint                  | Denominator for error rates   |
| `endpoint_down_count`                       | 5xx errors                                  |                               |
| `endpoint_missing_404_count`                | 404 (not found) errors                      |                               |
| `endpoint_unauthorized_403_count`           | 403 errors                                  | Consider threshold for issues |
| `endpoint_response_time_count`              | Responses >200 ms                           |                               |
| `chpl_servicebaseurl_listing`               | Link to vendor service base URL list        |                               |
| `chpl_servicebaseurl_listing_noncomformant` | Non-conformance to HTI-1                    |                               |
| `endpoint_token_failure_count`              | Token incorrectly rejected                  |                               |
| `endpoint_sandbox_unavailable`              | No sandbox/test user (1 = unavailable)      |                               |
| `endpoint_documentation_unavailable`        | Documentation unavailable (1 = no, 0 = yes) |                               |
| `endpoint_ial2_fail_count`                  | IAL2 failures (if applicable)               |                               |
| `endpoint_incorrect_count`                  | Incorrect endpoint provided                 |                               |
| `endpoint_missing_count`                    | Missing endpoints / FHIR not enabled        |                               |
| `other_complaint_text`                      | Additional notes                            |                               |
| `fhir_compliance_percent`                   | % of non-compliant FHIR responses           |                               |
| `Is_known_good`                             | Latest connection succeeded                 | Yes/No                        |

---

## Notes

* You may submit your full FHIR endpoint database, but **priority is on endpoints with issues**.
* This format is **still evolving** and may change based on feedback.

Please share suggestions or improvements in the Health Tech Ecosystem Slack. https://www.cms.gov/priorities/health-technology-ecosystem/overview
