```
The plan is to write a boilerplate app for the microbit in ionic & cordova.
```


Install node.js
Install Java JDK
Install Android SDK

Install ionic & cordova
`npm install -g cordova ionic`

make project
`ionic start MicrobitProject blank`

add platform
`cordova platform add android --save`

check platform requirements
`cordova requirements`

see: https://cordova.apache.org/docs/en/latest/guide/cli/

```
Requirements check results for android:
Java JDK: installed 1.8.0
Android SDK: installed true
Android target: not installed
Please install Android target: "android-24".

Hint: Open the SDK manager by running: "C:\Users\anonymous\AppData\Local\Android\sdk\tools\android.bat"
You will require:
1. "SDK Platform" for android-24
2. "Android SDK Platform-tools (latest)
3. "Android SDK Build-tools" (latest)
Gradle: installed
Error: Some of requirements check failed
```

Install the `android-24` target. Run the `.bat` file.

bower must be installed globaly:

npm install -g bower
