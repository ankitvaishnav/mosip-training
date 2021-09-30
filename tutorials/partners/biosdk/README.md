# BioSDK

## Setup

### BioSDK service VM
Ideally, vendor setups the BioSDK service from you and gives you the url to access the APIs

Useful commands (Tech5):
* Go to VM: `ssh -i <key.pem> user@ip`
* Check if service is running: `docker ps`
* Run service: `docker run -d -p 80:9977 --name t5-biosdk-service-c3.0  <image name, it will be given by T5>`
* Check service logs: `docker logs -f t5-biosdk-service-c3.0`

### MOSIP configuration

#### Update IDA properties
```properties
mosip.biosdk.default.host=http://13.233.66.241
mosip.biosdk.default.service.url=${mosip.biosdk.default.host}/biosdk-service
```
