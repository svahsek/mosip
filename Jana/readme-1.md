# Mock ABIS

## Overview
- A module to mock ABIS functionality for testing non-production MOSIP
    deployments.
- This module also provides swagger API to test only INSERT/IDENTIFY functionality.

## Requirements
Partner certificate (in case of encryption is enabled) cbeff.p12 we put
into resource folder.
<!--
Which Partner Certificate?
Can we refer to some topic here which explains this?
It is saying  we are putting cbeff.p12 into resource folder - Can we point to this within topic here itself (as bookmark)?
-->

### Setup

In case of partner based encryption. Upload the certificate by using swagger upload certificate request.
<!--
Can we also mention the steps 
-->


# Server deployment (for [sandbox]{.underline} deployment)

Docker based <!-- Can we explain this -->

**Steps**:

* Go to REPO_ROOT/mock-abis. <!-- You are saying go to mock-abis repo under MOSIP root repo and in next step you are saying build the code -->

* Build the code: `[mvn]{.underline} clean install -Dmaven.test.skip=true -Dgpg.skip=true`.

* Create a docker image: docker build . --file[Dockerfile]{.underline} --tag mock-abis. <!-- Create docker image? -->

* Push the [docket]{.underline} image to docker registry. You can directly use these images for running mock ABIS. <!-- move it to docker registry .... and cal also run it directly? -->
-- 

**Please check [Dockerfile]{.underline} for passing [env]{.underline} properties**

Swagger [url]{.underline}:`https://<hostname>/v1/mock-abis-service/swagger-ui.html#/`





# Local [dev]{.underline} against Server (for testing against server)

This section is for the developers to run mock-abis locally against MOSIP server

Steps:

* Go to REPO_ROOT/mock-abis.

* Setting ABIS queue [conf]{.underline} (here queue details will be for server's queue):

1) Create registration-processor-abis.json in resources.

2) Copy the contents of registration-processor-abis-sample.json to registration-processor-abis.json.

3) Update registration-processor-abis.json with the correct queue details. <!-- what is correct queue detail -->

4) Download the latest kernel-auth-adapter from
`https://mvnrepository.com/artifact/io.mosip.kernel/kernel-auth-adapter`and save into [lib]{.underline} folder.

* Build the code: `[mvn]{.underline} clean install-Dmaven.test.skip=true -Dgpg.skip=true`.

* Run the jar: `java
-Dloader.path=[lib]{.underline}/kernel-auth-adapter-1.3.0-SNAPSHOT.jar
-Dlocal.development=true -Dabis.bio.encryption=true
-Dspring.profiles.active=local -Dmosip_host=https://<server
[hostname]{.underline}> -jar target/mock-abis-1.3.0-SNAPSHOT.jar`.

Flags:

* local.development (true: whenever running locally, this will take the registration-processor-abis.json from resources)

* abis.bio.encryption (true: in case if partner based encryption)

* mosip_host ([hostname]{.underline} of the MOSIP server)

Swagger [url]{.underline}: `http://localhost:8081/v1/mock-abis-service/swagger-ui.html#/`




# Fully local (for active development)

This section is for developers to run mock-abis locally against a queue, messages can be inserted directly to the queue and respective mock-abis
responses can be [analysed]{.underline}.

## Requirements:

* Local ActiveMQ server

Running ActiveMQ locally:

* Go to REPO_ROOT/mock-abis/[activemq]{.underline}

* use the docker compose file to create a local [activemq]{.underline}
server: `docker-compose up`

* Open [activemq]{.underline} web console: `http://localhost:8161/`

Steps:

* Go to REPO_ROOT/mock-abis.

* Setting ABIS queue [conf]{.underline} (here queue details will be for local queue):

1) Create registration-processor-abis.json in resources.

2) Copy the contents of registration-processor-abis-sample.json to registration-processor-abis.json.

3) Update registration-processor-abis.json with the correct queue details.

``` json
 {
"abis": [

 {

 "name": "ABIS",

 "host": "",

 "port": "",

 "brokerUrl": "tcp://{env}.mosip.net: {port}",

 "inboundQueueName": "ctk-to-abis ",

 "outboundQueueName": "abis-to-ctk ",

 "pingInboundQueueName": "ctk-to-abis ",

 "pingOutboundQueueName": "abis-to-ctk ",

 "userName": "artemis",

 "password": "{password}",

 "typeOfQueue": "ACTIVEMQ",

 "inboundMessageTTL": 2700

 }

 ]

 }
 ```

4) * for local database we use following

``` 
javax.persistence.jdbc.url=jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1

javax.persistence.jdbc.driver=org.h2.Driver

javax.persistence.jdbc.user=sa

javax.persistence.jdbc.password=sa

hibernate.ddl-auto=update

hibernate.temp.use_jdbc_metadata_defaults = false

hibernate.dialect = org.hibernate.dialect.H2Dialect
```

5) Download the latest kernel-auth-adapter from `https://mvnrepository.com/artifact/io.mosip.kernel/kernel-auth-adapter` and save into `[lib]{.underline}` folder.

* Build the code: `[mvn]{.underline} clean install
-Dmaven.test.skip=true -Dgpg.skip=true`.

* Run the jar: `java
-Dloader.path=[lib]{.underline}/kernel-auth-adapter-1.3.0-SNAPSHOT.jar
-Dlocal.development=true -Dabis.bio.encryption=true
-Dspring.profiles.active=local -Dmosip_host=https://<server
[hostname]{.underline}> --add-opens
java.xml/jdk.xml.internal=ALL-UNNAMED --add-opens
java.base/java.lang.reflect=ALL-UNNAMED --add-opens
java.base/java.lang.stream=ALL-UNNAMED --add-opens
java.base/java.time=ALL-UNNAMED --add-opens
java.base/java.time.LocalDate=ALL-UNNAMED --add-opens
java.base/java.time.LocalDateTime=ALL-UNNAMED --add-opens
java.base/java.io.Reader=ALL-UNNAMED --add-opens
java.base/java.util.Optional=ALL-UNNAMED --add-opens
java.base/java.time.LocalDateTime.date=ALL-UNNAMED -jar
target/mock-abis-1.3.0-SNAPSHOT.jar`.

* Add message directly to queue and view responses from mock ABIS

Flags:

* local.development (true: whenever running locally)

* abis.bio.encryption (true: in case if partner based encryption)

* mosip_host ([hostname]{.underline} of the MOSIP server)

Swagger [url]{.underline}:`http://localhost:8081/v1/mock-abis-service/swagger-ui/index.html#/`

![](media/image1.png){width="6.268055555555556in" height="3.5243055555555554in"}

## APIs for configuration and expectation setting

[Sample expectations](./[docs]{.underline}/sampleExpectations.md)

### Update configuration

[Url]{.underline}: http://{host}/v1/mock-abis-service/config/configure

Method: POST

Request:

```[json]{.underline}

{

"findDuplicate": "false"

}

```

Response:

```text

Successfully updated the configuration

```

### Get configuration

[Url]{.underline}: http://{host}/v1/mock-abis-service/config/configure

Method: GET

Response:

```[json]{.underline}

{

"findDuplicate": false

}

```

### Set Expectation**

[Url]{.underline}: http://{host}/v1/mock-abis-service/config/expectation

Method: POST

Request:

```[json]{.underline}

{

"id": "<Hash of the [biometric]{.underline}>",

"version": "[xxxxx]{.underline}",

"[requesttime]{.underline}": "2021-05-05T05:44:58.525Z",

"actionToInterfere": "Identify/ Insert",

"forcedResponse": "Error",

"errorCode": "",

"delayInExecution": "",

"gallery": {

"referenceIds": [

{

"referenceId": "<Hash of the duplicate [biometric]{.underline}>"

}

]

}

}

```

Response:

```text

Successfully inserted expectation $expectation_id

```

### Get Expectations

[Url]{.underline}: http://{host}/v1/mock-abis-service/config/expectation

Method: GET

Response:

```[json]{.underline}

{

"[abshd]{.underline}": {

"id": "[abshd]{.underline}",

"version": "[xxxxx]{.underline}",

"[requesttime]{.underline}": "2021-05-05T05:44:58.525Z",

"actionToInterfere": "Identify/ Insert",

"errorCode": "",

"delayInExecution": "",

"forcedResponse": "Error/Success",

"gallery": {

"referenceIds": [

{

"referenceId": "[xxxxxx]{.underline}"

},

{

"referenceId": "[xxxxxx]{.underline}"

}

]

}

},

"[dffefe]{.underline}": {

"id": "[dffefe]{.underline}",

"version": "[xxxxx]{.underline}",

"[requesttime]{.underline}": "2021-05-05T05:44:58.525Z",

"actionToInterfere": "Identify/ Insert",

"forcedResponse": "Error/Success",

"errorCode": "",

"delayInExecution": "",

"gallery": {

"referenceIds": [

{

"referenceId": "[xxxx]{.underline}"

},

{

"referenceId": "[xxxxxx]{.underline}"

}

]

}

}

}

```

### Delete Expectation

[Url]{.underline}:
http://{host}/v1/mock-abis-service/config/expectation/{id}

Method: DELETE

Response:

```text

Successfully deleted expectation $expectation_id

```

## Tips & tricks

1) While setting the expectation the hash of [iso]{.underline} image
should be taken, directly taking [bdb]{.underline} hash will not work.

```text

formula for hash: SHA256_hash(base64_decode([bdb]{.underline}))

```

2) Use get cached [biometics]{.underline} to check whether the hashes
are proper.

**## Developer (tips and trick)**

This section is for the developers, for developing this modules fast &
efficiently

1) Use local profile: `-Dspring.profiles.active=local`. Pass this as
VM options

2) Pass: `mosip_host=https://<mosip host>` as [env]{.underline}
variable.

3) Setting ABIS queue [conf]{.underline}:

* Create registration-processor-abis.json in resources

* Copy the contents of registration-processor-abis-sample.json to
registration-processor-abis.json

* Update registration-processor-abis.json with the correct queue
details

By performing the above steps, you are ready to run mock-ABIS in local
machine

## APIs

API documentation is available
[here](https://mosip.github.io/documentation/).

## License

This project is licensed under the terms of [[Mozilla]{.underline}
Public License 2.0](LICENSE).

D:ProjectMosiptest>git clone
https://github.com/mosip/mosip-mock-services.git

Cloning into 'mosip-mock-services'...

remote: Enumerating objects: 10666, done.

remote: Counting objects: 100% (3214/3214), done.

remote: Compressing objects: 100% (1190/1190), done.

remote: Total 10666 (delta 1663), reused 2835 (delta 1488), pack-reused
7452 (from 1)Receiving objects: 100% (10666/10666), 149.56 MiB | 6.67
MiB/s

Receiving objects: 100% (10666/10666), 150.17 MiB | 6.73 MiB/s, done.

Resolving deltas: 100% (3218/3218), done.

Updating files: 100% (444/444), done.

D:ProjectMosiptest>cd mosip-mock-services

D:ProjectMosiptestmosip-mock-services>cd mock-abis

D:ProjectMosiptestmosip-mock-servicesmock-abis>mvn clean
install -Dgpg.skip=true
