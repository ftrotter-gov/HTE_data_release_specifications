
# EHR Vendors — NPD Requirements

Copied from GA_Requirements_CleanDraft_07_01

| Requirement and explanatory text | Document page(s) |
|---|---:|
| **National Provider Directory Integration**<br><br>**Support creation, maintenance, and submission of provider directory entries in the National Provider Directory (NPD).**<br><br>EHRs must integrate with the NPD to publish provider organization, location, endpoint, and verification metadata. EHRs may submit on behalf of providers or incorporate intermediary partners. EHRs must query NPD to validate identity and trust for inbound requests. | 32 |
| **What this means in practice**<br> | All EHRs should be reporting [Organizational NPIs in their Client FHIR endpoints](../data_release_specifications/CEHRT_Vendor_Reporting.md).<br> If they would like to, EHR vendors can also use this mechanism to publish their individual NPI links to FHIR endpoints. <br><br> Alternatively, EHR vendors can choose to release data under the [General Endpoint and Affiliation Data Release Specification](../data_release_specifications/GeneralProviderEndpointAndAffiliationData.md). <br><br>In either case please slack Fred Trotter in the ecosystem with the location of the data (or send the data itself).

|
