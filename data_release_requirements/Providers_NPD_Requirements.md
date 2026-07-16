
# Providers — NPD Requirements

Copied from GA_Requirements_CleanDraft_07_01

| Requirement and explanatory text | Document page(s) |
|---|---:|
| **National Provider Directory Publication**<br><br>**Maintain NPD information.**<br><br>Most provider identity, organizational affiliation, and location data is already established through the National Provider Identifier (NPI) registry and, for Medicare-enrolled providers, through PECOS, which the NPD relies on as authoritative sources.<br><br>Providers must ensure that additional HTE-specific information — network/endpoint information, verification metadata, and any HTE-relevant attributes not captured by NPI or PECOS — is published to the NPD in a complete, accurate, and timely manner. This may be carried out on the provider's behalf by the provider's EHR vendor or by their CMS-aligned network. | 15 |
| **What this means in practice**<br> | 

You need to either:  
A. Email or Slack Fred Trotter, either the provider list data or a link to the release of the data on your website! Please use the format specified in [../data_release_specifications/GeneralProviderEndpointAndAffiliationData.md](../data_release_specifications/GeneralProviderEndpointAndAffiliationData.md) or tell us how you need to vary from it if neeeded.
B. If you cannot create a report with the data in this format or a similar one on your EHR system without the help of your vendor:
B1. And if your EHR Vendor is NOT a member of the CMS Health Tech Echosystem! you can email a person at your EHR vendor a link to this data specification and cc Fred Trotter so that we can provide technical assistance to your EHR vendor in implementing the report. 
B2. If your EHR Vendor IS a part of the CMS Health Tech Ecosystem, please slack Fred Trotter and every EHR company representative on the EHR system slack so that we can coordinate getting a report built that exports this data! 
C. If you believe that your EHR vendor is already reporting this information to the Health Tech Ecosystem on your behalf, please slack or email Fred Trotter to confirm that we have the report has been released correctly. 

|
| **Delegation**<br><br>**Primary Entities (Providers) may authorize Assignees to execute queries on their behalf for any permitted Purpose of Use.**<br><br>A Primary Entity is the entity or organization that holds the permitted-purpose relationship with the patient. An Assignee is a third-party organization authorized through a Business Associate Agreement (BAA) or other applicable legal authority.<br><br>Delegation must be established and verified through the National Provider Directory (NPD) using CMS-approved IAL2 identity verification. Participants responding to queries may rely on NPD delegation records to determine whether a request is authorized. If a Primary Entity has the legal authority to query for a given Purpose of Use, that authority may be exercised directly or through an authorized Assignee regardless of the network, connection, or software system used to execute the query. | 15–16, 27–28 |
| **What this means in practice**<br> |

Work in Progress.

 |
| **National Provider Directory Registration**<br><br>**Providers can verify their identity and credentialing in the National Provider Directory (NPD).**<br><br>Provider identity, affiliations, Medicare enrollment, and verified endpoints will be represented in the NPD. Providers are not required to complete IAL2 verification in NPD for GAP, but it is highly encouraged. Providers can flag credentialing inaccuracies if identified. Providers can update credentials and other pertinent information directly in NPD. Known information regarding providers can be supplied indirectly via EHRs, proxies, or CMS Aligned Networks. | 27 |
| **What this means in practice**<br> |

Once the NPD Registration system has launched, please have one physician, nurse or other clinician with an individual NPI record visit [https://directory.cms.gov/](https://directory.cms.gov) and update your data there. 

|
