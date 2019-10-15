# Generate signing keys (SHA1, SHA256) for Android app from the command line (flutter)

[Posted at SO](https://stackoverflow.com/a/58375353/10797095)

Run `gradlew signingReport` from the `android` directory under the root of your flutter project:
```
myflutterproject/android$ ./gradlew signingReport
```
This assumes you have JAVA_HOME and PATH to bin directory set.

If you do not have the full JDK installed, the location of the Java Runtime Environment (JRE) embedded with Android Studio can be found by running:

`$ flutter doctor -v`

With a default Android Studio installation the location of the JRE should be:

`/opt/android-studio/jre/bin/`

To set the `JAVA_HOME` environment variable and PATH to the bin directory, add the following lines to your `~/.bashrc` file:
```
export JAVA_HOME=/opt/android-studio/jre
export PATH=$PATH:$JAVA_HOME/bin
```
(Close and reopen the terminal window before use)

