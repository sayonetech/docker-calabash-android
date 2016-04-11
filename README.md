# Calabash test environment for android applications on docker

Calabash is an acceptance testing tool for android and IOS applications. The requied packages will be installed by building an image from the Docker file. And the packages are listed below.

  - Java openjdk 7
  - Android-sdk_r24.4.1
  - Calabash-android
  - Ruby 2.3.0

### Installation

You need docker installed globally:

```sh
$ git clone [git-repo-url] calabash-android
$ docker build -t <image name as you wish> .
  
"Make sure that the "." is not missing when you buid the image"

$ docker run --name <container name> -i <image name>
"The parameters can be varied according to the environments"
```
### Fixing keystore related issues after set up

After setting up the container the keystore related issues ma raise. The following steps will help to fix the issue
* Navigate to  /.android directory .
* Remove the existing debug.keystore file in case one exist
* Apply the command 
```
$keytool -genkey -v -keystore debug.keystore -alias androiddebugkey -storepass android -keypass android -keyalg RSA -keysize 2048 -validity 10000
```
* Following that navigate to the directory where the feature files exist and setup the calabash android by using the command
```
$ calabash-android setup
```
* The resign the new debug.keystore file using the command
``` 
$ calabash-android resign <apk path>
```
* And finally run the test by using the command 
``` 
$ calabash-android run <apk path>
```
