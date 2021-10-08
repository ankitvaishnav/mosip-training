# Tech5

## Windows SDK

### Setup

* Got sdkDependency.zip from url
* Downloaded face_sdk_cpu.zip (4 GB)
* Create a folder "native"
```text
Folders/ files inside native folder
<dir /B>

face_sdk (unzipped face_sdk_cpu.zip, copied from face_sdk_cpu/share)
face_sdk.dll
face_sdk.lic
face_sdk_utils.exe
fingersdk_utils.exe
iris_sdk.dll
iris_sdk.lic
iris_sdk_ankit.req
iris_sdk_jni.dll
iris_utils.exe
T5FaceNativeJNI.dll
T5FingerClientNativeJNI_x64.dll
tech5_client.lic
Tech5_ClientEdition_x64.dll
```
* Create config.properties parallel to native folder and update property `RemoteLicensingCachePath`
```text
irisThreshold=6.0
fingerThreshold=6.0
faceThreshold=6.0
writeFiles=true

loadFace=false
loadFinger=true
loadIris=false

fingerToken=DF7210B36C3E33ABD8FC2607263A00E33EFD1E3D945CA32087DE6F14A0468B4A

QualityVersion=100
RemoteLicensingCachePath=D:\\clients\\guinea_111\\guinea-1.1.1-v1\\native
RemoteLicensingToken=E4002379F2B4566D3B0EC63B1A4293EDB66AE2CC2098464B1EB777E7AB5ACF3A
UseBackgroundChecker=true
UseBlurChecker=true
UseFaceColorChecker=true
UseGlassesSmileOcclusionChecker=true
UseHotSpotsChecker=true
UseMaskChecker=true
UseOverexposureChecker=true
UseRedEyesChecker=true
UseRemoteLicensing=1
UseRotationChecker=true

FaceDetectorVersion=200
AlignmentVersion=103
BuilderVersion=105
FaceDetectoConfidence=0.9f
AgeGenderVersion=100
BatchSize=1
ComputeDevice=-1
FaceSelectorAlg=2

mBuilderVersion=105
mMatcherFirListHint=100000
mMatcherTableCode=gn
```
* Add few properties in run.bat and update them accordingly
```text
set path=%path%;"D:\clients\guinea_111\guinea-1.1.1-v1\native"
set FACE_SDK_BIN_ROOT="D:\clients\guinea_111\guinea-1.1.1-v1\native\face_sdk"
```

* Copy the jars inside sdkDependency.zip to regclient lib folder
```text
Files inside sdkDependency/lib
<dir /B>

ABISTech5FaceSDKAdapter.jar
client.jar
common.jar
commons-codec-1.9.jar
irisSDK1_0.jar
Tech5-winSdkv1.5.jar
```

### Generate license

#### Face license

* Run these commands in cmd to create face license
```text
set FACE_SDK_REMOTE_LICENSE_DEFAULT=1
set FACE_SDK_REMOTE_LICENSE_TOKEN=66C1746DE795D39A173DD51CFFB3256ED319B4163104ACBB522B502A113F8D87
face_sdk_utils.exe --license
```
* Above commands will generate a license file in %temp% folder... face_sdk66C1746DE795D39A173DD51CFFB3256ED319B4163104ACBB522B502A113F8D87.lic
* Copy license file to native folder and rename the file to `face_sdk.lic`
# it will generate a license file in %temp% folder... face_sdk66C1746DE795D39A173DD51CFFB3256ED319B4163104ACBB522B502A113F8D87.lic

#### Finger license
* Run following command in native folder:`fingersdk_utils.exe --fetch-license --token DF7210B36C3E33ABD8FC2607263A00E33EFD1E3D945CA32087DE6F14A0468B4A --output tech5_client.lic`

#### Iris license
* Run following command in native folder: `iris_utils.exe --request`
* It will create iris_sdk.req file in native folder
* Give this file to Tech5 to get the license