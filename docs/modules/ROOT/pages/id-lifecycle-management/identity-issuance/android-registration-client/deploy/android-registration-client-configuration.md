# Configuration Guide

This guide provides a comprehensive list of configurable properties for the Android Registration Client. Please note that this list is not exhaustive but serves as a helpful checklist for reviewing commonly configured properties.

It is important to acknowledge that all properties listed in this guide are automatically synchronized with the Android Registration Client. These properties are sourced from the `registration-default.properties` file.

1. In the **`registration-default.properties`** file, update the following property to specify the field values on which you want to enable the handle. Ensure that these field values match the field values in the **IDSchema.**

```properties
mosip.registration.default-selected-handle-fields=email,phone
```

2. In the **`id-authentication-default.properties`** file, update the **Regex** to validate handles with the provided key as the postfix:

```properties
mosip.ida.handle-types.regex={ '@email' : '.*@email$', '@phonenumber' : '.*@phonenumber$' }
```

3. In the **`id-repository-default.properties`** file, map the postfix values with the corresponding field values:

```properties
mosip.identity.fieldid.handle-postfix.mapping={'email':'@email', 'phone':'@phonenumber'}
```

#### Configuration files

* `application-default.properties`
* `registration-default.properties`

#### SBI related configurations

Timeouts in milliseconds are set during any HTTP calls to SBI.

```
mosip.registration.mdm.connection.timeout=10000
mosip.registration.mdm.RCAPTURE.connection.timeout=40000
mosip.registration.mdm.MOSIPDINFO.connection.timeout=5000
mosip.registration.mdm.MOSIPDISC.connection.timeout=5000
```

Quality score threshold based on modality, Possible values 1 to 100

```
mosip.registration.leftslap_fingerprint_threshold=40
mosip.registration.rightslap_fingerprint_threshold=40
mosip.registration.thumbs_fingerprint_threshold=40
mosip.registration.iris_threshold=60
mosip.registration.face_threshold=9
```

Retry attempts, Possible values 1 to 10

```
mosip.fingerprint_authentication.quality_score=30
mosip.iris_authentication.quality_score=30
mosip.face_authentication.quality_score=30
```

Quality score threshold based on the modality for operator authentication, Possible values 1 to 100\`

```
mosip.fingerprint_authentication.quality_score=30
mosip.iris_authentication.quality_score=30
mosip.face_authentication.quality_score=30 
```

#### Batch Size

Jobs like RID sync, packet upload, and status sync are carried out in batches, several registration records are to be executed in a batch on every trigger.

```
mosip.registration.rid_sync_batch_size=5
mosip.registration.packet_upload_batch_size=5
mosip.registration.status_sync_batch_size=5 
```

#### Scheduled Jobs

Default CRON expression for scheduling the Jobs.

`mosip.registration.sync_jobs_restart_freq=0 0 */11 ? * *`

#### Other Configurations

*   Enables/disables reviewer authentication on any biometric exception during registration

    `mosip.registration.reviewer_authentication_configuration=Y`
*   If enabled, cross-check of resident's biometrics with locally stored operator biometric templates.

    `mosip.registration.mds.deduplication.enable.flag=N`
*   Minimum disk space required to create a packet - in MB

    `mosip.registration.disk_space_size=5`
*   Maximum no. of days for approved packet pending to be synced to a server beyond which Registration Client is frozen for registration

    `mosip.registration.last_export_registration_config_time=100`
*   No. of days beyond audit creation date to delete audits

    `mosip.registration.audit_log_deletion_configured_days=10`
*   The maximum duration to which registration is permitted without sync of master data

    `mosip.registration.sync_transaction_no_of_days_limit=5`
*   Allowed several invalid login attempts

    `mosip.registration.invalid_login_count=50`
*   Configuration is used to check if any sync job is missed/ failed beyond expected days, this configuration is checked every time the operator clicks on any registration process. We follow the below convention to create this config key.

    `mosip.registration.job api name as in sync_job_def table.frequency=value in days`

#### Date formats

*   Date format to be displayed on acknowledgment slip, default value - dd/MM/yyyy hh:mm a

    `mosip.registration.application_date_format`
*   Date format to be displayed on Registration Client dashboard, default format - dd MMM hh:mm a

    `mosip.registration.dashboard_date_format`

#### Supporting properties for 1.1.5.x server compatibility

Due to the absence of UI specifications in the 1.1.5.x versions, the android regclient addresses backward compatibility by migrating the schema of these versions to the LTS UI Spec structure.

To facilitate this migration, certain configurations and templates have been incorporated to ensure compatibility with the 1.1.5.x server. The list of these configurations is provided below.

* `mosip.registration.consent-screen-template-name=reg-consent-screen-content-template`

The consent screen is not a part of 1.1.5.x schema structure. So, we are completely fetching this consent screen content from `master.template` table, and the `templateTypeCode` for the consent screen content is mentioned in the above configuration.

* `mosip.registration.individual-biometrics-id=individualBiometrics`

The id of individual biometrics should be mentioned in the above property according to the configured 1.1.5.x schema.

* `mosip.registration.introducer-biometrics-id=guardianBiometrics`

The id of guardian/ introducer biometrics should be mentioned in the above property according to the configured 1.1.5.x schema.

* `mosip.registration.infant-agegroup-name=INFANT`

The age-group name for infants (aged below 5 years) which is configured in the configured server should be mentioned in the above property.

* `mosip.registration.agegroup-config={"INFANT":{"bioAttributes":["face"],"isGuardianAuthRequired":true},"ADULT":{"bioAttributes":["leftEye","rightEye","rightIndex","rightLittle","rightRing","rightMiddle","leftIndex","leftLittle","leftRing","leftMiddle","leftThumb","rightThumb","face"],"isGuardianAuthRequired":false},"SENIOR_CITIZEN":{"bioAttributes":["leftEye","rightEye","rightIndex","rightLittle","rightRing","rightMiddle","leftIndex","leftLittle","leftRing","leftMiddle","leftThumb","rightThumb","face"],"isGuardianAuthRequired":false}}`

The above property indicates a list of age groups, required bio-attributes, and a flag that indicates whether guardian authentication is required or not. This property should be changed according to the server configuration and requirements.

* `mosip.registration.allowed-bioattributes=leftEye,rightEye,rightIndex,rightLittle,rightRing,rightMiddle,leftIndex,leftLittle,leftRing,leftMiddle,leftThumb,rightThumb,face`

The above property defines the list of bio-attributes that are allowed for scanning during registration. If there are any changes in the server, it should be changed accordingly.

* `mosip.registration.default-app-type-code=000`

The above property defines the default applicantTypeCode. In LTS, we have applicanttype.mvel script to fetch the documents according to age, gender, and some other attributes. Based on the applicant details, the script returns an applicantTypeCode which can be any value from “000” to “014”, and respective documents will be fetched from `master.applicant_valid_document table`. Since we do not have this script defined in 1.1.5.x to handle this, we have added a default `applicantTypeCode`.

#### Templates

Ensure that the preview and acknowledge templates are present in the `template table` of `mosip_master` database with the following type code:

`reg-android-preview-template-part`

`reg-android-ack-template-part`

#### Logout <a href="#logout-.1" id="logout-.1"></a>

Logout from ARC will check for any running background tasks in the background. Ask the user if the user still wants to logout from the application.

* If the user clicks on logout on the popup, all the jobs running and scheduled jobs will stop.
* If no jobs are running in the background, the user will simply log out and navigate to the login screen.
* No configuration changes are required to log out of ARC.
