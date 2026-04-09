# CEHRT Client FHIR Organizational Identifier Reports


## Introduction

Certified EHR Technology (CEHRT) vendors are required to publish their clients’ FHIR endpoints in a way that enables:

* Discovery by other entities
* At-scale lookup via the National Provider Directory (NPD)

However, many CEHRT vendors do not currently meet this requirement.

CMS hopes to soon begin providing data reports to CEHRT vendors, and the public, starting with CMS Health Tech Ecosystem participants to help them understand:

* Regulatory requirements
* Their current level of compliance


## Existing Regulatory Requirements

HHS / ONC / ASTP regulations require CEHRT vendors to publish:

* Client FHIR endpoints
* Associated organizational information

This must be done using specific **FHIR resource bundles**.

### HTI-1 Final Rule (HTI1-FR)

Under the [Health Data, Technology, and Interoperability Final Rule (HTI1-FR)](https://www.federalregister.gov/documents/2024/01/09/2023-28857/health-data-technology-and-interoperability-certification-program-updates-algorithm-transparency-and#p-1182):

* CEHRT vendors must include **facility-level identifiers**
* These identifiers must be included in the [service base URL publication](https://www.ecfr.gov/current/title-45/part-170/section-170.404#p-170.404%28b%29%282%29)

ONC/ASTP later clarified what qualifies as a valid *facility-level identifier*.


## Current Ecosystem Behavior

* The **ONC/ASTP Lantern project**:

  * Downloads CEHRT-published endpoints nightly
  * Merges and republishes the dataset
  * Includes any provided organizational identifiers

* The **CMS National Provider Directory (NPD)**:

  * Also regularly ingests this data

### Key Issue

* Most CEHRT vendors **do not publish valid identifiers**


## CMS NPD approach

To properly associate endpoints with individual practitioners, any data ingetion process must have:

* **Preferred:** Organizational NPI (ONPI)
* **Acceptable alternative:** CCN

At this time:

* CMS is **not yet proposing additional regulatory requirements**
* Instead our focus is on:

  * Communicating expectations
  * Improving compliance with existing HTI1-FR requirements



## CEHRT Vendor Reports: Data Structures

These reports are based on **Lantern data**:

* Source: [https://lantern.healthit.gov/](https://lantern.healthit.gov/)



### 1. Lantern Data Report

* Raw Lantern dataset filtered to your EHR company
* Used to verify that all client endpoints are correctly published



### 2. Organizational Summary

Aggregated view by organization:

* `organization_name` — Organization name
* `best_npi_status` — Best NPI status across all records
* `distinct_endpoints` — Number of unique endpoints
* `distinct_addresses` — Number of unique addresses
* `distinct_npis` — Number of unique NPIs



### 3. Vendor Summary

Single-row summary at the CEHRT vendor level:

#### Core Metrics

* `api_developer_name` — CEHRT vendor name
* `total_organizations` — Total distinct organizations
* `total_endpoints` — Total distinct endpoints
* `total_addresses` — Total distinct addresses
* `total_distinct_npis` — Total distinct NPIs

#### Identifier Quality Metrics

* `orgs_with_valid_npi` — Count of organizations with valid NPIs

* `percent_orgs_with_valid_npi` — Percent with valid NPIs

* `orgs_with_ccn_instead` — Count using CCN instead of NPI

* `percent_orgs_with_ccn_instead` — Percent using CCN

* `orgs_with_clia_instead` — Count using CLIA instead of NPI

* `percent_orgs_with_clia_instead` — Percent using CLIA

* `orgs_with_uuid_instead` — Count using UUID instead of NPI

* `percent_orgs_with_uuid_instead` — Percent using UUID

* `orgs_with_invalid_npi` — Count with invalid NPIs

* `percent_orgs_with_invalid_npi` — Percent with invalid NPIs

* `orgs_with_missing_identifier` — Count missing identifiers

* `percent_orgs_with_missing_identifier` — Percent missing identifiers



If you want, I can also:

* Align this stylistically with your previous FHIR CSV doc
* Or turn both into a single cohesive “CMS ecosystem reporting spec” document
