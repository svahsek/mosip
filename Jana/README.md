# Converters

# Overview
This repository contains the source code for the Converters module, which enables the conversion of ISO biometric and document data into standard image formats such as JPEG or PNG. The module exposes API endpoints for configuring and handling conversion operations.

## Databases
Refer to SQL scripts.

## Build & run (for developers)

The project requires the following:

Java Development Kit (JDK): Version 21.0.4
Maven: Version 3.9.6

1. Build and install:
 - Navigate to the project directory:

    ```shell
    $ cd converters/kernel-bio-converter
    ```
2. Download the latest kernel-auth-adapter from https://mvnrepository.com/artifact/io.mosip.kernel/kernel-auth-adapter and save into lib folder.

3. Build the project:

```shell
    $ mvn install -DskipTests=true -Dgpg.skip=true
```
4. Run the jar locally:

    ```java
    $ java -Dloader.path=lib/kernel-auth-adapter-latestname.jar 
    --add-modules=ALL-SYSTEM 
    --add-opens java.xml/jdk.xml.internal=ALL-UNNAMED 
    --add-opens java.base/java.lang.reflect=ALL-UNNAMED 
    --add-opens java.base/java.lang.stream=ALL-UNNAMED 
    --add-opens java.base/java.time=ALL-UNNAMED
    --add-opens java.base/java.time.LocalDate=ALL-UNNAMED 
    --add-opens java.base/java.time.LocalDateTime=ALL-UNNAMED 
    --add-opens java.base/java.time.LocalDateTime.date=ALL-UNNAMED 
    --add-opens java.base/jdk.internal.reflect.DirectMethodHandleAccessor=ALL-UNNAMED  -jar target/latestjarname.jar.
    ```

Swagger url: [Swagger UI](http://localhost:8098/v1/converter-service/swagger-ui/index.html)

5. Use the jar as library:

```maven
		<dependency>
			<groupId>io.mosip.kernel</groupId>
			<artifactId>kernel-bio-converter</artifactId>
			<version>${kernel.bioconverter.version}</version>
			<classifier>lib</classifier>
		</dependency>
```

# Docker Instructions

1. To build a Docker image for a specific service, navigate to the service folder:

```shell
    $ cd <service folder>
```

2. Build the Docker image:

```shell
    $ docker build -f Dockerfile
```
        
## Channel:
Default channel is HTTP (POST)

## APIs for configuration and Expectation setting
[Sample expectations](../Action/docs/sampleExpectations.md)

### Update configuration

**Url**: http://{host}/v1/converter-service/convert

Method: POST

## Request:

```json
{
  "id": "sample-converter",
  "version": "1.0",
  "requesttime": "2022-02-22T16:46:09.499Z",
  "request": {
    "values": {
      "Left Thumb": "<base64 url encoded bdb>",
      "Right Iris": "<base64 url encoded bdb>"
    },
    "sourceFormat": "string",
    "targetFormat": "string",
    "sourceParameters": {
      "key": "value"
    },
    "targetParameters": {
      "key": "value"
    }
  }
}
```

| **Property**          | **Description**                                                                  |
| ----------------------| -------------------------------------------------------------------------------- |
| values 					      | key-value pairs, with base64 url encoded data                                    |
| sourceFormat 			    | Http mime types, ISO formats [ISO19794_4_2011, ISO19794_5_2011, ISO19794_6_2011] |
| sourceParameters 		  | key-value pairs [IMAGE/JPEG, IMAGE/PNG]                                          |
| targetFormat 			    | Http mime types, ISO formats                                                     |
| targetParameters 		  | key-value pairs                                                                  |


## Response:
```json
{
  "id": "sample-converter",
  "version": "1.0",
  "responsetime": "2022-02-22T16:46:09.513Z",
  "errors": [
    {
      "errorCode": "string",
      "errorMessage": "string"
    }
  ],
  "response": {
    "Left Thumb": "<base64 url encoded converted data>",
    "Right Iris": "<base64 url encoded converted data>"
  }
}
```

| **Property** | **Description**                                                                            |
| :--------    | :----------------------------------------------------------------------------------------- |
| response     | key-value pairs, with base64 url encoded converted data                                    |


## Error-codes:


| **Code**     | **Description**                  	                                                         |
| :----------- | :------------------------------------------------------------------------------------------ |
| MOS-CNV-001  | Input Source Request may be null or Source Format may be null or Target Format may be null	 |
| MOS-CNV-002  | Invalid Request Value	                                                                     |
| MOS-CNV-003  | Invalid Source Value or Source Format not supported					                               |
| MOS-CNV-004  | Invalid Target Value or Target Format not supported					                               |
| MOS-CNV-005  | Source value can not be empty or null					                                             |
| MOS-CNV-006  | Source not valid base64urlencoded					                                                 |
| MOS-CNV-007  | Could not read Source ISO Image Data				                                                 |
| MOS-CNV-008  | Source not valid ISO ISO19794_4_2011				                                                 |
| MOS-CNV-009  | Source not valid ISO ISO19794_5_2011					                                               |
| MOS-CNV-010  | Source not valid ISO ISO19794_6_2011					                                               |
| MOS-CNV-011  | Target format not valid 																	                                   |
| MOS-CNV-500  | Technical Error																				                                     |


## Configuration

[Configuration-Admin](https://github.com/mosip/mosip-config/blob/develop/admin-default.properties) and [Configuration-Application](https://github.com/mosip/mosip-config/blob/develop/application-default.properties) defined here.

## Deploy
To deploy Admin on Kubernetes cluster using Dockers refer to [Sandbox Deployment](https://docs.mosip.io/1.2.0/deployment/sandbox-deploymen)

## Test
Automated functional tests available in [Functional Tests repo](https://github.com/mosip/mosip-functional-tests)

## APIs
API documentation is available [here](https://mosip.github.io/documentation/).

## License
This project is licensed under the terms of [Mozilla Public License 2.0](../Action/LICENSE).