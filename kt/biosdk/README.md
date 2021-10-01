# BioSDK

## BioSDK service VM

### Setup
Ideally, vendor gives you a docker image the BioSDK service from you and gives you the url to access the APIs

Requirements:
* docker

Useful commands (Tech5):
* Go to VM: `ssh -i <key.pem> user@ip`
* Check if service is running: `docker ps`
* Run service: `docker run -d -p 80:9977 --name t5-biosdk-service  <image name, it will be given by T5>`
* Check service logs: `docker logs -f t5-biosdk-service`

### MOSIP configuration

#### Update IDA properties
```properties
mosip.biosdk.default.host=http://13.233.66.241
mosip.biosdk.default.service.url=${mosip.biosdk.default.host}/biosdk-service
```

## Windows BioSDK for Registration client

### Setup
There are no standard setup instructions as it depends on how vendor implemented the SDK.

### Registration properties (mosip-config)
```properties
mosip.biometric.sdk.provider.finger.classname=io.mosip.mock.sdk.impl.SampleSDK
mosip.biometric.sdk.provider.iris.classname=io.mosip.mock.sdk.impl.SampleSDK
mosip.biometric.sdk.provider.face.classname=io.mosip.mock.sdk.impl.SampleSDK
```
