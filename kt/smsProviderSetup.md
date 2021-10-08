# Custom SMS Provider

## Development

Implement [SMSServiceProvider interface](https://github.com/mosip/commons/blob/1.1.5/kernel/kernel-core/src/main/java/io/mosip/kernel/core/notification/spi/SMSServiceProvider.java)

Please check [msg91 implementation](https://github.com/mosip/mosip-ref-impl/tree/1.1.5/kernel/kernel-smsserviceprovider-msg91)

## Deployment (1.1.5)

Steps:
* Build the SMSProvider implementation jar and push it to local artifactory
* Update SMSProvider implementation jar name ($provider_name) in kernel-notification-service dockerfile.
* Build and run a new docker image for kernel-notification-service

### Building and deploying SMS provider implementation jar

Build the SMSProvider implementation jar and push it to local artifactory. Currently the default path to push the jar is libs-release-local/io/mosip/kernel/. For example, libs-release-local/io/mosip/kernel/$provider_name.

### Updating kernel-notification-service dockerfile

Update SMSProvider implementation jar name ($provider_name) in kernel-notification-service dockerfile. Currently, it uses kernel-smsserviceprovider-msg91:

```text
    wget -q --show-progress "${runtime_dep_url_env}/kernel-smsserviceprovider-msg91.jar" -O "${loader_path_env}"/kernel-smsserviceprovider-msg91.jar;
```

You can update it with your own implementation name

### Build and run new docker image for kernel-notification-service

Github actions will take care of building and creating image. Use this image to run the pod.
