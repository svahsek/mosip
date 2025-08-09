# Collab Guide

[Android Registration Client (ARC)](../) is a tablet application that serves as portable version of the existing desktop [Registration Client](https://docs.mosip.io/1.2.0/modules/registration-client). It can be accessed through Android devices and also meets mobility requirements of countries adopting MOSIP Identity.

The primary objective of the tablet version is to facilitate the registration process for residents who are not able to physically visit Registration centers and also serve remote locations where setting up Registration centers is not feasible. To address this challenge, the ARC was developed enabling Operators / Supervisors to easily access the remote areas and maximize resident registrations across the country.

This guide serves as a tool to demonstrate the impressive capabilities of MOSIP's system. Additionally, the primary user of this guide will be the Operator / Supervisor trying to register individuals for generating UIN.

Let's embark on this journey together to explore the potential of ARC.

{% hint style="info" %}
For developers setting up ARC locally, refer [Developers Guide](https://docs.mosip.io/1.2.0/modules/android-registration-client/android-registration-client-developer-guide).
{% endhint %}

## Pre-requisites

* Reliable and consistent Internet connectivity
* Tablets running Android version 10 to 13
* Tablets with a minimum of 4 GB RAM
* The tablets should be capable of capturing fingerprints, IRIS, and face (photo) biometrics. Additionally, they should also have the ability to scan documents. However, if the tablets do not support these capabilities, MOCK SBI can be used as an alternative.

{% hint style="info" %}
**Note**: For Mock MDS, click [here](https://drive.google.com/drive/folders/14q7E5pZtfj0eimF3JGzlVfU4eV-MRPCQ) to download the Mock MDS in your system folder, which will enable you to simulate biometric capture (without real biometric devices).
{% endhint %}

* The following details are required to access ARC in the [Collab](https://collab.mosip.net/) environment:
  * UIN or a VID
  * Machine details
* To obtain your UIN credentials for the Collab environment follow the below steps:
  * The provision of a Unique Identification Number (UIN) as a demonstration credential will enable you to have a firsthand experience of the ARC's capabilities and explore its various features.
  * Please fill out the [form](https://docs.google.com/forms/d/e/1FAIpQLScq-HoYkbx37iKtm_v17dn8UZTih-Xv_P93Ew3GEl8H-vH-qA/viewform) with the correct details and submit the form. Upon receiving the form, we will generate a demo credential for you. We will also register you as an Operator on Keycloak and map your device to the center to which your credential is required to be mapped.

## Step-by-Step Process

Mentioned below are the steps to download, install, and use ARC.

**Step 1**: Download and install the APK on an Android tablet. Visit the [Android Registration Client](https://collab.mosip.net/#/dashboard) to access ARC in the Collab environment.

**Step 2**: Install ARC and launch it.

**Step 3**: Login as an Operator with the credentials received and wait for synchronization to complete.

**Step 4**:  Refer to our comprehensive [User Guide](https://docs.mosip.io/1.2.0/modules/android-registration-client/android-registration-client-user-guide) document to learn how to register and use ARC.

**Note**: Please be advised that if the Android Registration Client is uninstalled and then re-installed, the aforementioned steps will need to be repeated from the start.

## Additional Resources

* To know more about features of the Android Registration Client, click [here](https://docs.mosip.io/1.2.0/modules/android-registration-client).
* To learn more about the ARC configurations, click [here](https://docs.mosip.io/1.2.0/modules/android-registration-client/android-registration-client-configuration).

## Get in Touch

If you require any assistance or encounter any issues during the testing and integration process, kindly reach out to us through the support provided below.

* Navigate to [Community](https://community.mosip.io/).
* Provide a detailed description about the support you require or provide complete information about the issue you have encountered, including steps to reproduce, error messages, logs and any other required details.

_Thank you. Wishing you a pleasant experience!_
