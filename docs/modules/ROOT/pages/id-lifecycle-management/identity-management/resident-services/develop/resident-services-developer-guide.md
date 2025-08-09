# Developers Guide

## Overview

[Resident Services](https://docs.mosip.io/1.2.0/modules/resident-services) are the self-services used by residents themselves via a portal. The Resident Portal is a web-based UI application that provides residents of a country with services related to their Unique Identification Number (UIN).

The documentation here will guide you through the prerequisites required for the developer's setup.

## Software setup

Below is a list of tools required in Resident Services:

1. JDK 11
2. Any IDE (like Eclipse, IntelliJ IDEA)
3. Apache Maven (zip folder)
4. pgAdmin
5. Postman
6. Git
7. Notepad++ (optional)
8. lombok.jar (file)
9. settings.xml (document)

Follow the steps below to set up Resident Services on your local system:

1. Download `lombok.jar` and `settings.xml` from [here](https://github.com/mosip/documentation/tree/1.2.0/docs/_files/resident-services-config-files).
2. Install Apache Maven.
3. Copy the `settings.xml` to ".m2" folder `C:\Users\<username>\.m2`.
4. Install Eclipse.
5.  Open the `lombok.jar` file and wait for some time until it completes the scan for Eclipse IDE and then click `Install/Update`. Specify the eclipse installation location if required by clicking the ‘Specify location…’ button. Then, click `Install/Update` the button to proceed.

    ![](../../../../.gitbook/assets/lombok-configuration.png)
6. Check the Eclipse installation folder `C:\Users\userName\eclipse\jee-2021-12\eclipse` to see if `lombok.jar` is added. By doing this, you will not have to add the dependency of `lombok` in your `pom.xml` file separately as it is auto-configured by Eclipse.
7.  Configure the JDK (Standard VM) with your Eclipse by traversing through `Preferences → Java → Installed JREs`.

    ![](../../../../.gitbook/assets/installed-jre.png)

## Code setup

For the code setup, clone the repository and follow the guidelines mentioned in the [Code Contributions](https://docs.mosip.io/1.2.0/community/code-contributions).

### Importing and building a project

1. Open the project folder where `pom.xml` is present.
2. Open the command prompt from the same folder.
3. Run the command `mvn clean install -Dgpg.skip=true -DskipTests=true` to build the project and wait for the build to complete successfully.
4.  After building a project, open Eclipse and select `Import Projects → Maven → Existing Maven Projects → Next → Browse to project directory → Finish`.

    ![](../../../../.gitbook/assets/import-project.png)
5. After successful importing of the project, update the project by right-clicking on `Project → Maven → Update Project`.

## Environment setup

1.  For the environment setup, you need an external JAR that is available [here](https://oss.sonatype.org/#nexus-search;gav~~kernel-auth-adapter~1.2.0-SNAPSHOT~~) with different versions. Download the below-mentioned JARs with appropriate latest/appropriate versions. You will need to input the appropriate artifact ID and version and other inputs.

    a. `icu4j.jar`

    b. `kernel-auth-adapter.jar`

    c. `kernel-ref-idobjectvalidator.jar`

    d. `kernel-transliteration-icu4j.jar`

    E.g.: You can download `kernel-auth-adapter.jar` and add to the project `Libraries → Classpath → Add External JARs → Select Downloaded JAR → Add → Apply and Close`).

    ![](../../../../.gitbook/assets/add-external-library.png)
2.  Clone [mosip-config repository](https://github.com/mosip/mosip-config).

    a. As Resident Services is using two properties files- `resident-default.properties` and `application-default.properties`. But for the local running of the application, you need to provide additional/overriding properties such as secrets, passwords, and properties passed by the environment which can be added to new files `application-dev-default.properties` (common properties for all modules) and `resident-dev-default.properties` (Resident service-specific properties).

    b. You will have to create both the property files according to your environment and put them in `mosip-config folder` (cloned). The same files are available below for reference.

    These two files are loaded by the application by specifying the application names in the Application VM arguments like- `Dspring.cloud.config.name=application,resident,application-dev`, `resident-dev` (also detailed in a later section).
3. To run the server, two files are required- `kernel-config-server.jar` and `config-server-start.bat`.
4.  Put both files in the same folder and point to the property- `Dspring.cloud.config.server.native.search-locations` to `mosip-config` folder in `config-server-start.bat` file and also check the version of `kernel-config-server.jar` towards the end of the command.

    Example:

    ```
    java -jar -Dspring.profiles.active=native  -
    Dspring.cloud.config.server.native.search-
    locations=file:C:\Users\myDell\mosipProject\mosip-config -
    Dspring.cloud.config.server.accept-empty=true  -
    Dspring.cloud.config.server.git.force-pull=false -
    Dspring.cloud.config.server.git.cloneOnStart=false -
    Dspring.cloud.config.server.git.refreshRate=0 kernel-config-server-1.2.0-20201016.134941-57.jar
    ```

* As mentioned earlier, you will have to create property files according to your environment like `resident-env-default` and `application-env-default` (here env represents environment name). Both files will contain different configurations such as `resident-env-default` will have config properties (e.g., secrets, passcodes, etc) used for the resident-services module only and `application-env-default` is used for environment-specific changes and can be used for other modules as well.
* In this example, currently, these two files are created for the dev environment and hence the files have suffixes of `-dev`. If you want to run it for a different environment such as qa, create these two files with `-qa` suffixes, and then you will also need to provide the appropriate VM argument for that referring to qa environment.

For instance,

* Add `mosip.resident.client.secret=***********` property to be able to use a decrypted passcode and run it on your local machine.
* If you check the URLs present in `application-default` the file, they are set to module-specific URLs, but you need to use internal/external environment URLs to access the APIs by using an application-dev-default file.
* In `application-dev-default` file, assign environment domain URL to `mosipbox.public.url` , and change all other URLs with ${mosipbox.public.url}.
* It results in `mosipbox.public.url=internal/externalAPI` (e.g., mosipbox.public.url=https://api-internal.dev.mosip.net) and it will connect with the Development environment.

5.  Run the server by opening the `config-server-start.bat` file.

    ![](../../../../.gitbook/assets/resident-dev-img1.png)

#### Configurations to be done in Eclipse

1.  Open Eclipse and run the project for one time as a Java application, so that it will create a Java application which you can see in debug configurations, and then change its name. (e.g.: project name with the environment - "Resident-dev").

    ![](../../../../.gitbook/assets/resident-dev-img2.jpg)
2.  Open the Arguments tab and specify Application VM arguments: For example, for a development environment:

    ```
    -Dspring.profiles.active=default -
     Dspring.cloud.config.uri=http://localhost:51000/config -
     Dspring.cloud.config.label=master -Dsubdomain=dev -
     Dspring.cloud.config.name=application,resident,application-dev,resident-dev --illegal-access=permit.
    ```

    Save this run configuration as ‘Resident-dev’ .

    For `qa` environment, you can create `Resident-qa` run configuration with VM argument as below.

    Example:

    ```
    -Dspring.profiles.active=default -
    Dspring.cloud.config.uri=http://localhost:51000/config -
    Dspring.cloud.config.label=master -Dsubdomain=qa -
    Dspring.cloud.config.name=application,resident,application-qa,resident-qa --illegal-access=permit
    ```

    ![](../../../../.gitbook/assets/resident-dev-img3.png)
3. Click `Apply` and then debug it (starts running). In the console, you can see a message like `Started ResidentBootApplication in 34.078 seconds (JVM running for 38.361)`.

### Resident services API

* For API documentation, refer [here](https://mosip.stoplight.io/docs/resident/9a5192571fc51-document).
* The APIs can be tested with the help of Postman or Swagger-UI.
* Postman is an API platform for building and using APIs. Postman simplifies each step of the API lifecycle and streamlines collaboration so you can create better APIs—faster. It is a widely used tool for API testing. Below you will find the APIs postman collection of resident-services.
* Swagger is an interface description language for describing restful APIs expressed using JSON. You can access Swagger-UI of resident-services for the dev-environment from `https://api-internal.dev.mosip.net/resident/v1/swagger-ui.html` and localhost from `http://localhost:8099/resident/v1/swagger-ui.html`.
* Download the JSON collection available below and import it to your postman. [Resident-Service-APIs.postman\_collection-latest.json](https://github.com/mosip/documentation/tree/1.2.0/docs/_files/resident-services-config-files).

![](../../../../.gitbook/assets/resident-dev-img4.png)

* Create an environment as shown in the image below.

This environment is created for dev. Give the variable name as `url` and set both values as `https://api-internal.dev.mosip.net`.

![](../../../../.gitbook/assets/resident-dev-img5.png)

* Similarly, create another environment as shown below.

This environment is created for localhost. Give the variable name as `url` and set both values as `http://localhost:8099`.

![](../../../../.gitbook/assets/resident-dev-img6.jpg)
