# Get android apk debug signing key

## Context

Building a debug android release in flutter. Firebase requires a signing key to enable some functionality (Google sign in, dynamic links etc).

Working on a Chromebook (i.e. linux system) with Android Studio installed.

`$ /opt/android-studio/jre/bin/./keytool -list -v -keystore ~/.android/debug.keystore  -alias androiddebugkey -storepass android -keypass
 android`
 
The location of JRE embedded with Android Studio (full JDK is not installed) is discoverable using `$ flutter doctor -v`

