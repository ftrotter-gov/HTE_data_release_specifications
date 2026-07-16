# Payer Well-Known JSON Example

## Overview

This folder contains an example of the `.well-known/payer-endpoints` JSON file
that health insurance payers are expected to publish at the root of their domain:

    https://{payer-domain}/.well-known/payer-endpoints

This file provides a single, machine-discoverable entry point to all required
payer data publications, enabling automated discovery without manual registry
maintenance.

## Structure

### `resourceType`
References the Da Vinci HRex well-known definition that this file extends.

### `identifier`
A payer identifier using a CMS or payer-defined naming system.

### `payer_uuid`
A stable UUID for this payer, for use in systems that need a durable identifier
independent of naming conventions.

### `string_search_match`
A list of human-readable strings (plan names, brand names, DBA names) that
can be used to match this payer record in search contexts.

### `endpoints`
A flat key-value map of named endpoints. Keys follow the convention:

    {endpoint_type}#{disambiguator}

For Da Vinci FHIR endpoints, the disambiguator is the **spec version**:

    davinci_provider_directory_endpoint#1.1

When multiple instances of the same endpoint type exist, the disambiguator
identifies **what makes them different**. For Da Vinci endpoints this is
typically spec version. For Transparency in Coverage ToC files (see below)
it is the issuer ID, since a carrier may have multiple licensed issuers each
publishing a separate ToC file.

## Endpoint Types

### Da Vinci FHIR Endpoints
Standard Da Vinci implementation guide endpoints, keyed by spec name and
version. See the [Da Vinci implementation guides](https://hl7.org/fhir/us/davinci-hrex/)
for valid spec names and versions.

### Transparency in Coverage Table of Contents

```json
"tic_table_of_contents#issuer-11111": "https://example.com/mrf/2025-01-01_example-payer_issuer-a_index.json",
"tic_table_of_contents#issuer-22222": "https://example.com/mrf/2025-01-01_example-payer_issuer-b_index.json"
```

These keys point to Transparency in Coverage (TiC) Table of Contents files,
as required under CMS-1715-F and conforming to the
[CMS price transparency guide schema](https://github.com/CMSgov/price-transparency-guide/tree/master/schemas/table-of-contents).

The disambiguator after `#` is the **issuer ID** rather than a spec version,
because a carrier holding company typically has multiple licensed insurance
issuers, each publishing a separate ToC file under the CMS TiC schema.
