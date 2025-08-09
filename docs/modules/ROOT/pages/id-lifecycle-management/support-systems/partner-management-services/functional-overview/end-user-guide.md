# Authentication Partner

## PMS Admin (Partner Admin)

**Partner Management System (PMS) is used by both; PMS Admin and Partner**\
**User.**

* Partner Administrator: Partner Admin
* Partners: Partner User

## What all activities does a 'Partner Admin' perform for Authentication Partner?

Being a 'Partner Admin' you can perform following 3 activities to\
complete the end to end functionality pertaining to Authentication\
partner.

* Upload Root CA and Sub CA Certificates
* Create Policy Group and Policy
* Approve/Reject Policy

### Upload Root CA and Sub CA

Only after you 'Upload Root CA and Sub CA Certificates Interface)' that a Partner will then be able to 'Upload CA signed\
Partner Certificate.

As a process of Partner onboarding onto PMS after successful registration, Partner is required to **Upload CA signed Partner Certificate** on behalf of their organisation which would be used to build a trust store in MOSIP to cryptographically validate that they are from a trusted organisation to perform authentication of citizens. Also this certificate is used to encrypt the response shared in e-KYC.

{% hint style="warning" %}
**Important:**

Before a Partner will be able to '**Upload 'CA Signed Certificate**' it is prerequisite that the '**Partner Admin**' must\
upload the **Root CA** and **Sub CA**.
{% endhint %}

#### To Upload Root CA and Sub CA Certificates

1. In 'Certificate Trust Store' click on 'Upload Trust Certificate'.
2. Select the Partner Domain- AUTH in Upload Trust Certificate page.
3. Choose the **Root CA Certificate** to upload (only files with extensions as .cer or .pem).
4. Click Submit.
5. Similarly, sub/intermediate CA certificate should be uploaded by following the above steps (1-4).

<figure><img src="../../../../../Users/keshavsingh/Office/PMS/half/media/image1.png" alt=""><figcaption><p>image</p></figcaption></figure>

### Creating Policy Group and Policy

As Partner Admin you are required to '**Create Policy Group**' and '**Create Policy(s)**' which a 'Partner' will be able to select while self-registering on PMS.

As an admin you will also have privilege to '**Approve Policy Request**' when a Partner selects a Policy and it comes to you for\
approval, You can read more about this [**here**](end-user-guide.md#approve-policy-request).

#### Create Policy group

* Login as Partner Admin into the PMS portal.
* All the policy groups created so far by Partner Admin/ Policy Manager are displayed on 'List of Policy Groups' page.

<figure><img src="../../../../.gitbook/assets/temp-auth-partner-image2.png" alt=""><figcaption><p>Create Policy Group</p></figcaption></figure>

* On clicking the 'Create Policy Group' option on the top right of the screen, we can create a Policy Group by providing suitable name and description that is self explanatory for partners, who would be selecting them during Partner Policy Request to create API Key/ OIDC Client etc.

<figure><img src="../../../../.gitbook/assets/temp-auth-partner-image3.png" alt=""><figcaption><p>Caption</p></figcaption></figure>

* On click of Submit, a success message appears.

<figure><img src="../../../../.gitbook/assets/temp-auth-partner-image4.png" alt=""><figcaption><p>Caption</p></figcaption></figure>

#### Create Auth policy

Once you 'Create Policy' you will also be required to activate it and then it will reflect when a Partner wants to select a policy. You can also change the status of **Policy Group** ( Deactivate) or edit it using the Action menu as shown below.

1. On clicking Authentication Policy tab, List of all previously created Authentication Policies are displayed.

On clicking Authentication Policy tab, List of all previously created Authentication Policies are displayed.

<figure><img src="../../../../.gitbook/assets/temp-auth-partner-image5.png" alt=""><figcaption><p>Caption</p></figcaption></figure>

On clicking 'Create Authentication Policy' button, Partner Admin/Policy manager is navigated to Create Authentication Policy page where details such as policy group, policy name, description etc will have to be entered.

Note: Only active policy groups are available in the policy group dropdown.

Click on the upload button to upload policy data . Only json files are allowed for upload.

<figure><img src="../../../../.gitbook/assets/temp-auth-partner-image6.png" alt=""><figcaption><p>Caption</p></figcaption></figure>

On clicking on Save as Draft, following success message appears.

<figure><img src="../../../../.gitbook/assets/temp-auth-partner-image7.png" alt=""><figcaption><p>Caption</p></figcaption></figure>

On clicking 'Go Back', admin is navigated back to tabular view where the policy is saved as 'draft' status.

To **publish policy** which is currently in draft status, click on 'publish' option in action menu. A popup window appears seeking for confirmation to publish.

<figure><img src="../../../../.gitbook/assets/temp-auth-partner-image8.png" alt=""><figcaption><p>Caption</p></figcaption></figure>

On clicking Publish, a success message appears . Click on close to close the window.

<figure><img src="../../../../.gitbook/assets/temp-auth-partner-image9.png" alt=""><figcaption><p>Caption</p></figcaption></figure>

The given policy changes to 'Activated' status after being published.Once activated, the admin cannot edit the policy, hence the option is disabled.

#### Approve Policy Request

When a Partner have chosen a 'Policy Group' and the 'Policy', an approval request will come to you and you can approve or reject a '**Policy Request**' using '**Request Policy**' screen.

When a Partner have chosen a 'Policy Group' and the 'Policy' an approval request will come to you and you can approve or reject a '**Policy Request**' using '**Request Policy**' screen.

* Click on **Partner Policy Linking** in the admin dashboard.
* Select the policy mapping that needs an approval.The options provided for policy linking requests in 'Pending for Approval' are to Approve/ Reject. Also an option to view the policy request details is also provided.

<figure><img src="../../../../.gitbook/assets/temp-auth-partner-image10.png" alt=""><figcaption><p>Caption</p></figcaption></figure>

On clicking the Approve/ Reject option, the window appears - and partner admin can click on either Approve or Reject to take appropriate action.

<figure><img src="../../../../.gitbook/assets/temp-auth-partner-image11.png" alt=""><figcaption><p>Caption</p></figcaption></figure>

The status- Approved / Rejected gets updated in the tabular view.

<figure><img src="../../../../.gitbook/assets/temp-auth-partner-image12.png" alt=""><figcaption><p>Caption</p></figcaption></figure>

## Authentication Partner Workflow

To be able to access the services by PMS and to validate that the partner is from a trusted organisation, undergoing self registration on PMS and uploading CA signed certificate is necessary'.

* Self Register on PMS Interface
* Upload CA signed Certificate

### Self-Register on PMS as Authentication Partner

1. The Authentication Partner can register themselves on MOSIP PMS portal by clicking **Register** on the Login Page, a form comes up.
2. Enter the Authentication Partner details:
   1. Partner type (Authentication Partner)
   2. First and Last name
   3. Organization Name
   4. Address, Phone number
   5. e-mail, Username and password

<figure><img src="../../../../.gitbook/assets/pms_register_as_partner.png" alt=""><figcaption><p>Keshav Singh</p></figcaption></figure>

2. **Click** on **Register**, a popup comes up which asks you to '**Choose a Policy Group**' and seeks you to '**Agree to Terms and Conditions**' before you can be considered as 'Authentication Partner.
3. Select the relevant/applicable **Policy Group** on **Select Policy Group** popup using **Policy Group** dropdown by reading through policy group description in dropdown.

<figure><img src="../../../../.gitbook/assets/pms_select_policy_group.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/pms_select_policy_group_2.png" alt=""><figcaption></figcaption></figure>

4. On Submit it will ask you to read through ‘**Terms and Condition**’ and having carefully read through it you can agree and accept it.

<figure><img src="../../../../.gitbook/assets/pms_self_register_terms_and_condition.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Validations**:

* User can select only one **Policy Group** per **Partner Type**.
* Policy selected once cannot be edited later.
* Terms & Conditions: Partner consent refers to voluntary and informed agreement provided by a partner user on behalf of the Partner Organisation, to a specific action or process where the users have a clear understanding of what they are consenting to. User consent is important to ensure data privacy, where it is compliant to obtain explicit consent from partners before collecting, processing, or sharing their personal/ organisation level data.
* A detailed description explaining which of their personal and organisation data is used and for what purposes it will be used in PMS will be informed while seeking user consent.
{% endhint %}

### CA Signed Partner Certificate Upload / Download or Re-Upload

User is now in [**Home Page/Dashboard**](end-user-guide.md#interface-overview) where the following features are provided to Authentication Partner: 1) Partner Certificate, 2) Policies and 3) Authentication Services: OIDC Client and API Key generation.

These features can also be accessed by clicking on side panel (in the form of icons) or clicking on the hamburger menu <img src="../../../../.gitbook/assets/pms_hamburger_menu.png" alt="" data-size="line"> on the top left which is available across all screens of PMS to help user to easily navigate.

Once registered, as a process of Partner onboarding onto PMS after successful registration, user is required to perform upload CA signed Partner Certificate on behalf of their organisation which would be used to build a trust store in MOSIP to cryptographically validate that they are from a trusted organisation to perform authentication of citizens. Also this certificate is used to encrypt the response shared in e-KYC.

{% hint style="info" %}
**Tips**:

Later when required a Partner can also ‘Download Certificate’ and ‘Re-Upload Certificate’ (As the need may be).
{% endhint %}

{% hint style="info" %}
Important:

Before a Partner can upload a ‘CA Signed Certificate’ it is prerequisite that the ‘Partner Admin’ should have already had uploaded the **Root CA** and **Sub CA** certificates.
{% endhint %}

#### To Upload CA signed Certificate

1. Go to **Authentication Partner** (New UI) -> **Dashboard.**

<figure><img src="../../../../.gitbook/assets/pms_dashboard.png" alt=""><figcaption></figcaption></figure>

2. Click on **Partner Certificate** option, Click on the **Upload** button to upload the partner certificate signed by CA.

<figure><img src="../../../../.gitbook/assets/pms_upload_partner_vertificate_1.png" alt=""><figcaption></figcaption></figure>

3. Select the CA signed partner certificate from local system by tapping on the upload section (blue area).

<figure><img src="../../../../.gitbook/assets/pms_upload_partner_vertificate_2.png" alt=""><figcaption></figcaption></figure>

3. Certificate is successfully fetched from local system.

<figure><img src="../../../../.gitbook/assets/pms_upload_partner_vertificate_3.png" alt=""><figcaption></figcaption></figure>

4. Click on **Submit**, Partner Certificate is uploaded successfully.

<figure><img src="../../../../.gitbook/assets/pms_upload_partner_vertificate_4.png" alt=""><figcaption></figcaption></figure>

5. On closing the popup, The user can view the uploaded certificate details in the form of a list view.

<figure><img src="../../../../.gitbook/assets/pms_upload_partner_vertificate_5.png" alt=""><figcaption></figcaption></figure>

#### Download Certificate

There is also an option to download initially uploaded CA signed certificate and also the MOSIP Signed Certificate.

#### Re-Upload Certificate

Reuploading certifacte is required in cases when MOSIP Signed Certificate gets expired after one year.

{% hint style="info" %}
**Note:**

'MOSIP Signed Certifcate has a validity of 1 year from the time of Partner Certificate Upload.
{% endhint %}

You must ensure that you re-upload the partner certificate again so that new MOSIP signed certificate can be generated and other functionalities such as Request Policy, Authentication Policies can function.

### Request Policy

**Pre-Requisite**: **Policy Manager** (in our case '**Admin**') must have created a [**Policy Group**](end-user-guide.md#create-policy-group) and then created a [**Policy**](end-user-guide.md#create-an-auth-policy) within it for the Partner to be able to ‘**Request a Policy**’.

#### To Request a Policy

1. Click on the 'Request Policy' option in User homepage/dashboard.
   1. Each policy name is provided with policy description, You can make a suitable policy selection. You can provide appropriate request comments and submit the policy request details. A message conveying Policy request submitted successfully to admin is displayed.

<figure><img src="../../../../.gitbook/assets/pms_request_policy_1.png" alt=""><figcaption></figcaption></figure>

2. This newly created policy request will be in ‘Pending for Approval’ status. You can also click on action menu to see all the submitted policy details irrespective of its status.

<figure><img src="../../../../.gitbook/assets/pms_request_policy_2.png" alt=""><figcaption></figcaption></figure>

3. Once the request is approved (Partner Admin will [**Approve Policy Request**](end-user-guide.md#approve-policy-request)). Once the request is approved you can view the status turns to ‘Approved’ status.

<figure><img src="../../../../.gitbook/assets/pms_request_policy_3.png" alt=""><figcaption></figcaption></figure>

## Authentication Service

After the partner has selected a policy group, uploaded partner certificate, requested for policy and also got admin approval - partner can now perform 'Authentication Services':

* OIDC Client: Create OIDC Client for approved policy
* API Key : Generate API Key for approved policy

**Prerequisites**: Policy requested by the **Partner** must be already approved by **Policy Manager** (Read More [**here**](end-user-guide.md#approve-policy-request)).

#### Creating OIDC Client

* The authentication partner needs to provide the following details to create OIDC Client
  * Select suitable Authentication policy for OIDC Client creation. Only the policies that are APPROVED by admin will be available in dropdown for selection.
  * Enter the public key in JWK format, name or label for OIDC Client, LogoURI and one or more Redirect URI.
  * On successful submission, user can find this record in tabular list of submitted OIDC Client details in ‘Activated’ status. Tabular list and individual view of submitted OIDC Client details along with OIDC Client ID, Edit OIDC Client details and Deactivate OIDC Client can also be seen from here.

<figure><img src="../../../../.gitbook/assets/OIDC_client_creation_1.png" alt=""><figcaption></figcaption></figure>

* Once the details are in Activated status, user will be able to view the OIDC Client ID generated, by clicking on the eye icon ( <img src="../../../../.gitbook/assets/OIDC_client_creation_2_eye_icon.png" alt="" data-size="line">). clicking on the OIDC Client ID eye icon, opens a popup window which displays the Client ID and a copy button.
* This Client ID can then be consumed in eSignet to perform authentication. Client ID can be accessed by clicking on eye icon.
* User can utilize this OIDC Client ID to perform eSignet based authentication of citizens

<figure><img src="../../../../.gitbook/assets/OIDC_client_creation_3.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/OIDC_client_creation_4.png" alt=""><figcaption></figcaption></figure>

* The user can also view every OIDC Client detail individually using the View option

<figure><img src="../../../../.gitbook/assets/OIDC_client_creation_5.png" alt=""><figcaption></figcaption></figure>

* The user can also edit the OIDC Client details in Activated status (only OIDC Client Name, LogoURI and RedirectURI are editable) by selecting the edit option in Action Menu.

<figure><img src="../../../../.gitbook/assets/OIDC_client_creation_6.png" alt=""><figcaption></figcaption></figure>

* User can deactivate the OIDC Client ID by clicking on deactivate option . The deactivate popup window appears and on clicking confirm, the OIDC Client record is changed to Deactivated status. **Once deactivated, the client ID can not be used anymore for authentication**.

<figure><img src="../../../../.gitbook/assets/OIDC_client_creation_7.png" alt=""><figcaption></figcaption></figure>

#### API Key Generation

The authentication partner needs to provide the following details to generate API Key

* Select suitable Authentication policy for API Client. Only the policies that are **Approved** by admin will be available in dropdown for selection.

1. Enter an appropriate name or label for API Key to be generated and submit, On successful submission, a popup window displays API Key along with a copy button.

<figure><img src="../../../../.gitbook/assets/pms_generating_api_key_1.png" alt=""><figcaption></figcaption></figure>

2.  This API Key can be viewed by user in PMS application only once due to security reasons, hence the user is well notified with an appropriate message in the same API Key popup window to avoid closing the window unless user has not copied the API Key.\\

    <figure><img src="../../../../.gitbook/assets/pms_generating_api_key_2.png" alt=""><figcaption></figcaption></figure>
3.  User can find this record in tabular list of submitted API details in ‘Activated’ status.

    <figure><img src="../../../../.gitbook/assets/pms_generating_api_key_3.png" alt=""><figcaption></figcaption></figure>
4. User can either view individual API Key entries or view the consolidated list in tabular view.

<figure><img src="../../../../.gitbook/assets/pms_generating_api_key_4.png" alt=""><figcaption></figcaption></figure>

5. You also have an option to deactivate an API Key, which thereafter cannot be used for authentication. On clicking confirm, the API Key record is changed to Deactivated status. Once deactivated, it cannot be activated again. You may need to generate a new API key as per requirement.

<figure><img src="../../../../.gitbook/assets/pms_generating_api_key_5.png" alt=""><figcaption></figcaption></figure>

## Interface Overview

PMS (Partner Management System) is going under a comprehensive overhaul. This revamp includes improving usability and elevate the overall user experience (UX). The focus is to bring user centered design to PMS, make the PMS more intuitive, efficient, and aligned with our partners' evolving needs.

The PMS Interface 'Card View' for 'Authentication Partner' presents you with following features, These features can also be accessed by clicking on side panel (in the form of icons) or expanding the hamburger menu ( <img src="../../../../.gitbook/assets/pms_hamburger_menu.png" alt="" data-size="line">) on the top left which is available across all screens of PMS to help user to easily navigate.

Card view presentation is there for each functionality with brief description to help you understand the services offered in Partner User Dashboard.

After successfully registering you can access the Home Page / Dashboard. You will be able to view the features and functionalities on the dashboardand based on your Partner Type.

Note: You can access the partner dashboard only when you are duly registered and have selected the 'Policy Group'.

<figure><img src="../../../../.gitbook/assets/pms_dashboard.png" alt=""><figcaption></figcaption></figure>

Each functionality that the user can perform is displayed in each card so that there is independent navigation for each tasks.

* Partner Certificate: Upload or Reupload CA Signed Partner Certificate and Download CA Signed Partner Certificate & corresponding MOSIP Signed Certificate
* Policies: Request for a policy within the selected policy group, tabular list of requested policies along with status of admin approval, view requested policy details along with admin comments/status.
* Authentication Services:
  * OIDC Client : Create OIDC Client for approved policy, tabular list and individual view of submitted OIDC Client details along with OIDC Client ID, Edit OIDC Client details and Deactivate OIDC Client
  * API Key : Generate API Key for approved policy, tabular list and individual view of submitted API Key details and Deactivate API Key.

You can view your organisation name and username on the top right called 'User Profile', logout options is also placed here only.

## Reupload a new partner certificate through the following steps

1. Login to PMS and Go to Dashboard.
2. Click on Partner Certificate option in the dashboard / side panel / hamburger menu ( <img src="../../../../.gitbook/assets/pms_hamburger_menu.png" alt="" data-size="line"> ), you will be redirected to list view of partner certificate.

<figure><img src="../../../../.gitbook/assets/pms_dashboard.png" alt=""><figcaption></figcaption></figure>

3. Click on Re-Upload button of Authentication Partner Type.

<figure><img src="../../../../.gitbook/assets/pms_reupload_partner_certificate_1.png" alt=""><figcaption></figcaption></figure>

4. Re-upload certificate pop-up window appears. The time and date of previous certificate upload is also displayed for user reference. Click on the certificate upload section (blue area) to upload a new partner certificate from the local system.

<figure><img src="../../../../.gitbook/assets/pms_reupload_partner_certificate_2.png" alt=""><figcaption></figcaption></figure>

5. After selecting the certificate from local system, the fetched certificate name is displayed.

<figure><img src="../../../../.gitbook/assets/pms_reupload_partner_certificate_3.png" alt=""><figcaption></figcaption></figure>

6. Click on Submit, Partner certificate upload success message is displayed.

<figure><img src="../../../../.gitbook/assets/pms_reupload_partner_certificate_4.png" alt=""><figcaption></figcaption></figure>

7. Click on Close to come back to list view of partner certificate.

<figure><img src="../../../../.gitbook/assets/pms_reupload_partner_certificate_5.png" alt=""><figcaption></figcaption></figure>

### Forgot Password

You can retrieve password in case you are unable to recall.

1. Click on **Forgot Password** link displayed on login page to reset password.

<figure><img src="../../../../.gitbook/assets/pms_forgot_password_2.png" alt=""><figcaption></figcaption></figure>

2. Enter registered email address and submit, a message is displayed informing user that further instructions to reset password has been sent on te email address entered.

<figure><img src="../../../../.gitbook/assets/pms_forgot_password_3.png" alt=""><figcaption></figcaption></figure>

3. Click on the Reset password link received on his email address, you will be redirected to Change Password screen.

<figure><img src="../../../../.gitbook/assets/pms_forgot_password_5.png" alt=""><figcaption></figcaption></figure>

4. Enter a new password that adheres to password policy and re enter to confirm before you save it.

<figure><img src="../../../../.gitbook/assets/pms_forgot_password_4.png" alt=""><figcaption></figcaption></figure>

5. After clicking submit, This new password will be further used in subsequent logins
