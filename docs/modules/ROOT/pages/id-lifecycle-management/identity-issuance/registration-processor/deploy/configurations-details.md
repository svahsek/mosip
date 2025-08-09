# Configurations Details

### Overview

This guide details the configuration updates required in MOSIP to enable CRVS-initiated birth and death registration requests. It covers ID schema changes to add key fields, updates to authentication policies, property files, and identity mapping, along with new Camel routes and workflow settings. These changes ensure the proper handling and processing of vital events within the MOSIP ecosystem.

#### ID Schema Update for Initiating Infant Birth Requests <a href="#id-schema-update-for-initiating-infant-birth-requests" id="id-schema-update-for-initiating-infant-birth-requests"></a>

Before initiating an infant birth registration request from the CRVS system, updating the ID schema in MOSIP to include the necessary fields required for capturing introducer information is essential.

The following fields should be added to support the processing of infant birth registration requests:

* **introducerInfoToken** _(Optional)_
  * **Description**: A user information token representing the individual reporting the infant's birth to CRVS.

#### ID Schema Update for Initiating Death Requests <a href="#id-schema-update-for-initiating-death-requests" id="id-schema-update-for-initiating-death-requests"></a>

Before initiating a death registration request from the CRVS system, updating the ID schema in MOSIP to include the necessary fields required for capturing information related to the deceased and informant is essential.

The following fields should be added to support the processing of death registration requests:

* **deceasedDeclarationDate** _(Optional)_
  * **Description**: The date on which the individual was declared deceased.
* **declaredAsDeceased** _(Mandatory)_
  * **Description**: A flag indicating that the individual has been officially declared deceased.
* **typeOfDeath** _(Optional)_
  * **Description**: Specifies the nature of the death, such as _natural_ or _jurisdictional_.
* **deceasedInformer** _(Optional)_
  * **Description**: A user information token representing the individual reporting the death to CRVS.

{% hint style="info" %}
**Note**: The field `declaredAsDeceased` is mandatory and must be included in the ID schema to initiate any death registration request. The remaining fields can be configured based on specific use case requirements.
{% endhint %}

#### Configuring mosip-auth-policy <a href="#configuring-mosip-auth-policy" id="configuring-mosip-auth-policy"></a>

After updating the ID schema with the necessary fields for birth/death registration, corresponding changes must be applied to the default authentication policy. This step ensures that the new fields are correctly reflected in the ID authentication module particularly required when the authentication process involves the national ID of a deceased individual.

To include the new attributes in the authentication policy:

1. Update the existing `policy_file_id` by appending the newly added fields.
2. Execute the upgrade script to apply the changes.

Below is a sample SQL script for updating  `default-authpolicy` to include the field `declaredAsDeceased`:

```sql
UPDATE pms.auth_policy SET policy_group_id='mpolicygroup-default-auth', "name"='mpolicy-default-auth', descr='mpolicy-default-auth', policy_file_id='{"shareableAttributes":[{"attributeName":"fullName","source":[{"attribute":"fullName"}],"encrypted":true},{"attributeName":"dateOfBirth","source":[{"attribute":"dateOfBirth"}],"encrypted":true},{"attributeName":"gender","source":[{"attribute":"gender"}],"encrypted":true},{"attributeName":"phone","source":[{"attribute":"phone"}],"encrypted":true},{"attributeName":"email","source":[{"attribute":"email"}],"encrypted":true},{"attributeName":"addressLine1","source":[{"attribute":"addressLine1"}],"encrypted":true},{"attributeName":"addressLine2","source":[{"attribute":"addressLine2"}],"encrypted":true},{"attributeName":"addressLine3","source":[{"attribute":"addressLine3"}],"encrypted":true},{"attributeName":"region","source":[{"attribute":"region"}],"encrypted":true},{"attributeName":"province","source":[{"attribute":"province"}],"encrypted":true},{"attributeName":"city","source":[{"attribute":"city"}],"encrypted":true},{"attributeName":"postalCode","source":[{"attribute":"postalCode"}],"encrypted":true},{"attributeName":"zone","source":[{"attribute":"zone"}],"encrypted":true},{"attributeName":"preferredLang","source":[{"attribute":"preferredLang"}],"encrypted":false},{"attributeName":"individualBiometrics","group":"CBEFF","source":[{"attribute":"individualBiometrics"}],"encrypted":true,"format":"extraction"},{"attributeName":"declaredAsDeceased","source":[{"attribute":"declaredAsDeceased"}],"encrypted":true}],"dataSharePolicies":{"typeOfShare":"Data Share","validForInMinutes":"30","transactionsAllowed":"2","encryptionType":"Partner Based","shareDomain":"datashare.datashare","source":"ID Repository"}}' , policy_type='DataShare', "version"='1', policy_schema='https://schemas.mosip.io/v1/auth-policy', valid_from_date='2025-03-17 11:53:55.388', valid_to_date='2025-04-28 09:37:00.000', is_active=true, cr_by='admin', cr_dtimes='2025-03-17 11:53:55.388', upd_by='admin', upd_dtimes='now()', is_deleted=false, del_dtimes=NULL WHERE id='mpolicy-default-auth';
```

#### **Properties Added** <a href="#properties-added" id="properties-added"></a>

The following property files have been updated with the mentioned properties to support the new functionality:

#### **application-default.properties:** <a href="#application-default.properties" id="application-default.properties"></a>

* `mosip.kernel.idobjectvalidator.mandatory-attributes.reg-processor.crvs_new`\
  Mandatory attributes for infant birth registration flow.
* `mosip.kernel.idobjectvalidator.mandatory-attributes.reg-processor.crvs_death`\
  Mandatory attributes for death registration flow.
* `provider.packetreader.crvs1`\
  Packet reader for the source with the name CRVS1. This property should be updated if the source name is changed.
* `provider.packetwriter.crvs1`\
  Packet writer for the source with the name CRVS1. This property should be updated if the source name is changed.

#### **Fields Added to identity-mapping JSON:** <a href="#fields-added-to-identity-mapping-json" id="fields-added-to-identity-mapping-json"></a>

* deceasedDeclarationDate
* declaredAsDeceased
* typeOfDeath

#### **New Camel Routes:** <a href="#new-camel-routes" id="new-camel-routes"></a>

* registration-processor-camel-routes-crvs\_death-default.xml\
  New Camel route for death registration packet processing.
* registration-processor-camel-routes-infant-crvs\_new-default.xml\
  New Camel route for infant birth registration packet processing.

#### **registration-processor-default.properties:** <a href="#registration-processor-default.properties" id="registration-processor-default.properties"></a>

* `registration.processor.additional-process.category-mapping`\
  Mapping of the additional process to the internal process.
* `registration.processor.vid-support-for-update`\
  Enables VID support for updates.
* `mosip.regproc.workflow-manager.instance.api-id`\
  Unique ID for the workflow instance API.
* `mosip.regproc.workflow-manager.instance.version`\
  A version of the workflow instance API.
* `registration.processor.notification.additional-process.category-mapping`\
  Mapping of the additional process to the internal process for notification.

For more details on ID schema and configurations please refer [here](https://docs.mosip.io/1.2.0/id-lifecycle-management/identity-issuance/registration-client/deploy/registration-client-configuration).
