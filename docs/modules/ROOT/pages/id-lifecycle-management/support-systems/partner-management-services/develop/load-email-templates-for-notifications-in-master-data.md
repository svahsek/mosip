# Load Email Templates for Notifications in Master Data

To get email notifications from the PMS service, all required templates must be added to the Master Data Service, follow the steps below to load the templates.

### Steps to Authenticate the Master Data Service

To access the Master Data Service, follow the steps below to obtain and use a client token via the Auth Manager service.

1. Use the following Swagger URL to interact with the Auth Manager API: `https://api-internal.${env}.mosip.net/v1/authmanager/swagger-ui/index.html?configUrl=/v1/authmanager/v3/api-docs/swagger-config`
2. Use the `/authenticate/clientidsecretkey` endpoint to generate a client token.
3. Once the token is validated successfully, it will be added to the browser cookies automatically. This token will be used for authenticating subsequent requests to the Master Data Service.

**Request payload**:

```
{
  "id": "string",
  "version": "string",
  "requesttime": "2022-12-22T07:13:35.010Z",
  "metadata": {},
  "request": {
    "clientId": "mosip-pms-client",
    "secretKey": "XXXXXX",
    "appId": "partner"
  }
}
```

#### Steps to create a new template type in MasterData:

1. Use the following Swagger URL for Master Data Service: `https://api-internal.{env}.mosip.net/v1/masterdata/swagger-ui/index.html?configUrl=/v1/masterdata/v3/api-docs/swagger-config#/`
2. Use the `POST /templatetypes` endpoint from the Master Data Service to create a new template type.
3. The request body should include the following fields:
   * `code`: Unique identifier for the template type.
   * `description`: Description of the template type.
   * `isActive`: Boolean value indicating whether the template type is active.
   * `langCode`: Language code for the template type.
4. Once the template type is created, it can be used for template creation.

Example Request Body:

```
{ 
  "id": "string", 
  "version": "string", 
  "requesttime": "2025-02-26T07:14:29.119Z", 
  "metadata": {}, 
  "request": 
  { 
    "code": "PARTNER_CERT_EXPIRY_TEMPLATE", 
    "description": "Template type for partner certificate expiry", 
    "isActive": true, 
    "langCode": "fra" 
    } 
  }
```

Make sure to create the following template types for PMS notification templates.&#x20;

Each template type should be created for all six supported languages: English (eng), French (fra), Arabic (ara), Tamil (tam), Hindi (hin) and Kannada (kan).

* ROOT\_CERT\_EXPIRY
* INTERMEDIATE\_CERT\_EXPIRY
* PARTNER\_CERT\_EXPIRY
* WEEKLY\_SUMMARY\_TEMPLATE
* ROOT\_CERT\_EXPIRY\_SUBJECT
* INTERMEDIATE\_CERT\_EXPIRY\_SUBJECT
* PARTNER\_CERT\_EXPIRY\_SUBJECT
* WEEKLY\_SUMMARY\_SUBJECT

#### Steps to add a new template for PMS:

New Templates are avaliable here [https://github.com/mosip/partner-management-services/tree/develop/docs/templates](https://github.com/mosip/partner-management-services/tree/develop/docs/templates)

1. Use the `POST /templates` endpoint from the Master Data Service to add new templates for the PMS module.
2. The request body must include the following fields:
   * `id`: ID of the template.
   * `name`: Name of the template.
   * `description`: Description of the template.
   * `fileFormatCode`: Format of the template file (e.g., html or txt).
   * `model`: Template model type (e.g., velocity).
   * `fileText`: Content of the template in the specified format.(**If the file contains HTML content, all double quotes** " **within the content should be escaped using a backslash** \\")
   * `moduleId`: Unique identifier for the PMS module.
   * `moduleName`: Name of the module (e.g., PMS).
   * `templateTypeCode`: Code of the template type.
   * `langCode`: Language code for the template.
   * `isActive`: Boolean value indicating whether the template is active.
3. Once the template is created, it will be stored in the mosip\_master database.

Example Request Body:

```
{
  "id": "string",
  "version": "string",
  "requesttime": "2025-02-26T04:06:44.594Z",
  "metadata": {},
  "request": {
    "id": null,
    "name": "partner-certificate-expiry-template-eng",
    "description": "Template for partner certificate expiry",
    "fileFormatCode": "html",
    "model": "velocity",
    "fileText": "<!DOCTYPE html><html lang=\"en\"><head><meta charset=\"UTF-8\" /><meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\" /><style></style></head></html>",
    "moduleId": "10007",
    "moduleName": "PMS",
    "templateTypeCode": "PARTNER_CERT_EXPIRY_TEMPLATE",
    "langCode": "eng",
    "isActive": true
  }
}
```

Also add all the templates listed in the tables below with the specified **ID**, **name**, **description**, and other relevant details as provided.

<table><thead><tr><th width="76.73220825195312">ID</th><th width="159.65484619140625">Name</th><th width="174.5645751953125">Description</th><th>File Fomat Code</th><th>Template Type Code</th><th>LangCode</th></tr></thead><tbody><tr><td>3516</td><td>root-certificate-expiry-template-eng</td><td>Template for root certificate expiry</td><td>html</td><td>ROOT_CERT_EXPIRY_TEMPLATE</td><td>eng</td></tr><tr><td>3517</td><td>root-certificate-expiry-template-fra</td><td>Modèle d'expiration du certificat racine</td><td>html</td><td>ROOT_CERT_EXPIRY_TEMPLATE</td><td>fra</td></tr><tr><td>3518</td><td>root-certificate-expiry-template-ara</td><td>نموذج لانتهاء صلاحية شهادة الجذر</td><td>html</td><td>ROOT_CERT_EXPIRY_TEMPLATE</td><td>ara</td></tr><tr><td>3519</td><td>root-certificate-expiry-template-hin</td><td>रूट प्रमाणपत्र समाप्ति के लिए टेम्पलेट</td><td>html</td><td>ROOT_CERT_EXPIRY_TEMPLATE</td><td>hin</td></tr><tr><td>3520</td><td>root-certificate-expiry-template-kan</td><td>ಮೂಲ ಪ್ರಮಾಣಪತ್ರದ ಮುಕ್ತಾಯ ದಿನಾಂಕದ ಟೆಂಪ್ಲೇಟ್</td><td>html</td><td>ROOT_CERT_EXPIRY_TEMPLATE</td><td>kan</td></tr><tr><td>3521</td><td>root-certificate-expiry-template-tam</td><td>ரூட் சான்றிதழ் காலாவதிக்கான டெம்ப்ளேட்</td><td>html</td><td>ROOT_CERT_EXPIRY_TEMPLATE</td><td>tam</td></tr><tr><td>3522</td><td>intermediate-certificate-expiry-template-eng</td><td>Template for intermediate certificate expiry</td><td>html</td><td>INTERMEDIATE_CERT_EXPIRY_TEMPLATE</td><td>eng</td></tr><tr><td>3523</td><td>intermediate-certificate-expiry-template-fra</td><td>Modèle d'expiration de certificat intermédiaire</td><td>html</td><td>INTERMEDIATE_CERT_EXPIRY_TEMPLATE</td><td>fra</td></tr><tr><td>3524</td><td>intermediate-certificate-expiry-template-ara</td><td>نموذج انتهاء صلاحية الشهادة المتوسطة</td><td>html</td><td>INTERMEDIATE_CERT_EXPIRY_TEMPLATE</td><td>ara</td></tr><tr><td>3525</td><td>intermediate-certificate-expiry-template-hin</td><td>मध्यवर्ती प्रमाणपत्र समाप्ति के लिए टेम्पलेट</td><td>html</td><td>INTERMEDIATE_CERT_EXPIRY_TEMPLATE</td><td>hin</td></tr><tr><td>3526</td><td>intermediate-certificate-expiry-template-kan</td><td>ಮಧ್ಯಂತರ ಪ್ರಮಾಣಪತ್ರ ಮುಕ್ತಾಯಕ್ಕಾಗಿ ಟೆಂಪ್ಲೇಟ್</td><td>html</td><td>INTERMEDIATE_CERT_EXPIRY_TEMPLATE</td><td>kan</td></tr><tr><td>3527</td><td>intermediate-certificate-expiry-template-tam</td><td>இடைநிலை சான்றிதழ் காலாவதிக்கான டெம்ப்ளேட்</td><td>html</td><td>INTERMEDIATE_CERT_EXPIRY_TEMPLATE</td><td>tam</td></tr><tr><td>3528</td><td>partner-certificate-expiry-template-eng</td><td>Template for partner certificate expiry</td><td>html</td><td>PARTNER_CERT_EXPIRY_TEMPLATE</td><td>eng</td></tr><tr><td>3529</td><td>partner-certificate-expiry-template-fra</td><td>Modèle d'expiration du certificat de partenaire</td><td>html</td><td>PARTNER_CERT_EXPIRY_TEMPLATE</td><td>fra</td></tr><tr><td>3530</td><td>partner-certificate-expiry-template-ara</td><td>نموذج انتهاء صلاحية شهادة الشريك</td><td>html</td><td>PARTNER_CERT_EXPIRY_TEMPLATE</td><td>ara</td></tr><tr><td>3531</td><td>partner-certificate-expiry-template-hin</td><td>भागीदार प्रमाणपत्र समाप्ति के लिए टेम्पलेट</td><td>html</td><td>PARTNER_CERT_EXPIRY_TEMPLATE</td><td>hin</td></tr><tr><td>3532</td><td>partner-certificate-expiry-template-kan</td><td>ಪಾಲುದಾರ ಪ್ರಮಾಣಪತ್ರದ ಮುಕ್ತಾಯ ದಿನಾಂಕದ ಟೆಂಪ್ಲೇಟ್</td><td>html</td><td>PARTNER_CERT_EXPIRY_TEMPLATE</td><td>kan</td></tr><tr><td>3533</td><td>partner-certificate-expiry-template-tam</td><td>கூட்டாளர் சான்றிதழ் காலாவதிக்கான டெம்ப்ளேட்</td><td>html</td><td>PARTNER_CERT_EXPIRY_TEMPLATE</td><td>tam</td></tr><tr><td>3534</td><td>weekly-summary-template-eng</td><td>Template for weekly summary notifications</td><td>html</td><td>WEEKLY_SUMMARY_TEMPLATE</td><td>eng</td></tr><tr><td>3535</td><td>weekly-summary-template-fra</td><td>Modèle pour les notifications récapitulatives hebdomadaires</td><td>html</td><td>WEEKLY_SUMMARY_TEMPLATE</td><td>fra</td></tr><tr><td>3536</td><td>weekly-summary-template-ara</td><td>نموذج لإشعارات الملخص الأسبوعية</td><td>html</td><td>WEEKLY_SUMMARY_TEMPLATE</td><td>ara</td></tr><tr><td>3537</td><td>weekly-summary-template-hin</td><td>साप्ताहिक सारांश अधिसूचनाओं के लिए टेम्पलेट</td><td>html</td><td>WEEKLY_SUMMARY_TEMPLATE</td><td>hin</td></tr><tr><td>3538</td><td>weekly-summary-template-kan</td><td>ವಾರದ ಸಾರಾಂಶ ಅಧಿಸೂಚನೆಗಳಿಗಾಗಿ ಟೆಂಪ್ಲೇಟ್</td><td>html</td><td>WEEKLY_SUMMARY_TEMPLATE</td><td>kan</td></tr><tr><td>3539</td><td>weekly-summary-template-tam</td><td>வாராந்திர சுருக்க அறிவிப்புகளுக்கான டெம்ப்ளேட்</td><td>html</td><td>WEEKLY_SUMMARY_TEMPLATE</td><td>tam</td></tr><tr><td>3540</td><td>root-certificate-expiry-sub-template-eng</td><td>Subject template for root certificate expiry</td><td>txt</td><td>ROOT_CERT_EXPIRY_SUBJECT</td><td>eng</td></tr><tr><td>3541</td><td>root-certificate-expiry-sub-template-fra</td><td>Modèle de sujet pour l'expiration du certificat racine</td><td>txt</td><td>ROOT_CERT_EXPIRY_SUBJECT</td><td>fra</td></tr><tr><td>3542</td><td>root-certificate-expiry-sub-template-ara</td><td>نموذج موضوعي لانتهاء صلاحية شهادة الجذر</td><td>txt</td><td>ROOT_CERT_EXPIRY_SUBJECT</td><td>ara</td></tr><tr><td>3543</td><td>root-certificate-expiry-sub-template-hin</td><td>रूट प्रमाणपत्र समाप्ति के लिए विषय टेम्पलेट</td><td>txt</td><td>ROOT_CERT_EXPIRY_SUBJEC</td><td>hin</td></tr><tr><td>3544</td><td>root-certificate-expiry-sub-template-kan</td><td>ಮೂಲ ಪ್ರಮಾಣಪತ್ರದ ಮುಕ್ತಾಯ ದಿನಾಂಕದ ವಿಷಯ ಟೆಂಪ್ಲೇಟ್</td><td>txt</td><td>ROOT_CERT_EXPIRY_SUBJEC</td><td>kan</td></tr><tr><td>3545</td><td>root-certificate-expiry-sub-template-tam</td><td>மூலச் சான்றிதழ் காலாவதிக்கான பொருள் டெம்ப்ளேட்</td><td>txt</td><td>ROOT_CERT_EXPIRY_SUBJEC</td><td>tam</td></tr><tr><td>3546</td><td>intermediate-certificate-expiry-sub-template-eng</td><td>Subject template for intermediate certificate expiry</td><td>txt</td><td>INTERMEDIATE_CERT_EXPIRY_SUBJECT</td><td>eng</td></tr><tr><td>3547</td><td>intermediate-certificate-expiry-sub-template-fra</td><td>Modèle de sujet pour l'expiration du certificat intermédiaire</td><td>txt</td><td>INTERMEDIATE_CERT_EXPIRY_SUBJECT</td><td>fra</td></tr><tr><td>3548</td><td>intermediate-certificate-expiry-sub-template-ara</td><td>نموذج موضوعي لانتهاء صلاحية الشهادة المتوسطة</td><td>txt</td><td>INTERMEDIATE_CERT_EXPIRY_SUBJECT</td><td>ara</td></tr><tr><td>3549</td><td>intermediate-certificate-expiry-sub-template-hin</td><td>इंटरमीडिएट प्रमाणपत्र समाप्ति के लिए विषय टेम्पलेट</td><td>txt</td><td>INTERMEDIATE_CERT_EXPIRY_SUBJECT</td><td>hin</td></tr><tr><td>3550</td><td>intermediate-certificate-expiry-sub-template-kan</td><td>ಮಧ್ಯಂತರ ಪ್ರಮಾಣಪತ್ರ ಮುಕ್ತಾಯಕ್ಕಾಗಿ ವಿಷಯ ಟೆಂಪ್ಲೇಟ್</td><td>txt</td><td>INTERMEDIATE_CERT_EXPIRY_SUBJECT</td><td>kan</td></tr><tr><td>3551</td><td>intermediate-certificate-expiry-sub-template-tam</td><td>இடைநிலை சான்றிதழ் காலாவதிக்கான பொருள் வார்ப்புரு</td><td>txt</td><td>INTERMEDIATE_CERT_EXPIRY_SUBJECT</td><td>tam</td></tr><tr><td>3552</td><td>partner-certificate-expiry-sub-template-eng</td><td>Subject template for partner certificate expiry</td><td>txt</td><td>PARTNER_CERT_EXPIRY_SUBJECT</td><td>eng</td></tr><tr><td>3553</td><td>partner-certificate-expiry-sub-template-fra</td><td>Modèle de sujet pour l'expiration du certificat du partenaire</td><td>txt</td><td>PARTNER_CERT_EXPIRY_SUBJECT</td><td>fra</td></tr><tr><td>3554</td><td>partner-certificate-expiry-sub-template-ara</td><td>نموذج موضوعي لانتهاء صلاحية شهادة الشريك</td><td>txt</td><td>PARTNER_CERT_EXPIRY_SUBJECT</td><td>ara</td></tr><tr><td>3555</td><td>partner-certificate-expiry-sub-template-hin</td><td>भागीदार प्रमाणपत्र समाप्ति के लिए विषय टेम्पलेट</td><td>txt</td><td>PARTNER_CERT_EXPIRY_SUBJECT</td><td>hin</td></tr><tr><td>3556</td><td>partner-certificate-expiry-sub-template-kan</td><td>ಪಾಲುದಾರ ಪ್ರಮಾಣಪತ್ರದ ಮುಕ್ತಾಯದ ವಿಷಯ ಟೆಂಪ್ಲೇಟ್</td><td>txt</td><td>PARTNER_CERT_EXPIRY_SUBJECT</td><td>kan</td></tr><tr><td>3557</td><td>partner-certificate-expiry-sub-template-tam</td><td>கூட்டாளர் சான்றிதழ் காலாவதிக்கான பொருள் டெம்ப்ளேட்</td><td>txt</td><td>PARTNER_CERT_EXPIRY_SUBJECT</td><td>tam</td></tr><tr><td>3558</td><td>weekly-summary-subject-template-eng</td><td>Subject template for weekly summary notifications</td><td>txt</td><td>WEEKLY_SUMMARY_SUBJECT</td><td>eng</td></tr><tr><td>3559</td><td>weekly-summary-subject-template-fra</td><td>Modèle de sujet pour les notifications récapitulatives hebdomadaires</td><td>txt</td><td>WEEKLY_SUMMARY_SUBJECT</td><td>fra</td></tr><tr><td>3560</td><td>weekly-summary-subject-template-ara</td><td>قالب موضوعي لإشعارات الملخص الأسبوعي</td><td>txt</td><td>WEEKLY_SUMMARY_SUBJECT</td><td>ara</td></tr><tr><td>3561</td><td>weekly-summary-subject-template-hin</td><td>साप्ताहिक सारांश अधिसूचनाओं के लिए विषय टेम्पलेट</td><td>txt</td><td>WEEKLY_SUMMARY_SUBJECT</td><td>hin</td></tr><tr><td>3562</td><td>weekly-summary-subject-template-kan</td><td>ವಾರದ ಸಾರಾಂಶ ಅಧಿಸೂಚನೆಗಳಿಗಾಗಿ ವಿಷಯ ಟೆಂಪ್ಲೇಟ್</td><td>txt</td><td>WEEKLY_SUMMARY_SUBJECT</td><td>kan</td></tr><tr><td>3563</td><td>weekly-summary-subject-template-tam</td><td>வாராந்திர சுருக்க அறிவிப்புகளுக்கான தலைப்பு டெம்ப்ளேட்</td><td>txt</td><td>WEEKLY_SUMMARY_SUBJECT</td><td>tam</td></tr></tbody></table>

#### Steps to edit templates:

1. To update an existing template, use the `PUT /templates` endpoint from the Master Data Service.
2. This allows modifications to attributes such as `name`, `description`, `fileFormatCode`, `fileText`, and other relevant fields, except `langCode` and `id`, which cannot be changed.
