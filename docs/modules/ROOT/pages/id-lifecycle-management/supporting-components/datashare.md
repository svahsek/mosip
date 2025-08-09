# Datashare

## Overview

The DataShare service is used to share data with other entrusted services and partners. The mechanism shares are the following:

1. Retrieves and stores data to be shared in [Object Store](persistence/object-store.md) and returns a Datashare URL.
2. It fetches data from the Object Store when the Datashare URL is called.

The sharing of data is controlled by the [Datashare policy](../support-systems/partner-management-services/pms-existing/partner-policies.md#datashare-policy).

Data is encrypted before sharing it with partners. Learn more about [datashare encryption](../../readme/principles/privacy-and-security/data-protection.md#datashare).

The relationship of Datashare Service with other services is explained here. _NOTE: The numbers do not signify the sequence of operations or control flow. Arrows indicate the data flow._

![](../../.gitbook/assets/datashare.png)

1. ABIS Handler Stage creates datashare for ABIS.
2. Manual Adjudication Stage creates datashare for adjudication.
3. Verification Stage creates datashare for verification.
4. Datashare Service calls [Policy Manager Service](../support-systems/partner-management-services/#policy-management-service) to get the policy for creating shares.
5. It calls the [Keymanager](../supporting-services/keymanager/) Service to encrypt data as per policy.
6. Stores datashare inside [object store](persistence/object-store.md).
7. Retrieves datashare from the object store when the datashare URL is called.
8. External systems like [ABIS](biometrics/abis.md), Print System, Adjudication system etc. calls Datashare Service to get the datashare.
9. Print Service creates UIN PDF and uploads to datashare through Credential.
10. [Partner Manager Service](../support-systems/partner-management-services/) creates credentials for CA certificates to be used by [ID Authentication](../identity-verification/id-authentication.md).
11. Printing Stage creates credentials for printing systems and sends the data through datashare.
12. [ID Repository](../identity-issuance/id-repository/) Service sends data to ID Authentication system through Credential.
