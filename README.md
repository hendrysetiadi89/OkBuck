## Migrate to OkBuck

**What’s New?**
1. Faster build / compile / install
2. Restructured `build.gradle` for all modules
3. Upgrade gradle to version 4.4

**Getting Started**
1. **[Optional]** (_you can use Android Studio_), Install Intellij IDEA CE (https://www.jetbrains.com/idea/download/) and you can import your settings from Android Studio
2. **[Optional]** Install Buck for IDEA plugin
3. Install watchman (https://facebook.github.io/watchman/docs/install.html)
4. Switch / pull from `release`
5. Change `gradle.properties` like `distributionUrl=https\://services.gradle.org/distributions/gradle-4.4-all.zip`
6. Run : `./gradlew :buckWrapper`
7. Run : `./buckw build`
8. Add configuration at .buckconfig file
```
[httpserver]
    port = 0
[android]
    sdk_path = {YOUR_SDK_PATH}
```
8. Run : `./buckw project  --ide intellij`
9. You re done!

## What you should know?
1. Do not use any butterknife func/annotation/or whatever on application level
2. Please add depedency at build.gradle like we do
3. If you are developing react native submodule, you need to ignore the project folder (since a lot of `node_modules` dependencies also using buck as their build system). Add these codes to your `.buckconfig` file.
```
[project]
  ignore = reactnative-apps
```

## How to use?
- how to build? `./buckw build [target module]`
- how to install `./buckw install --run [target module]`
- how to install & run in multiple devices `./buckw install -x -r [target module]`
- how to clean `./buckw clean`
- for more `./buckw build tool`
- how to get adb list active device `adb devices`
- how to get list of emulator `emulator -list-avds`
- how to run emulator `emulator -avd {YOUR_EMULATOR}`


## Known Issue

#### 1. SSL error

SSL error when running `./gradlew :buckWrapper`

Network issue, you can use your personal hotspot

#### 2. Res Folder
```
ERROR: resource directory 'buck-out/bin/.okbuck/cache/__unpack_com.google.firebase.firebase-core-11.0.4.aar#aar_unzip__/res' does not exist
```
Please add new directory `res` manually at `buck-out/bin/.okbuck/cache/__unpack_com.google.firebase.firebase-core-11.0.4.aar#aar_unzip__` 

#### 3. Error node_modules
```
BUILD FAILED: //node_modules/react-native/local-cli/templates/HelloWorld/android/keystores:debug: parameter 'store': no such file or directory 'node_modules/react-native/local-cli/templates/HelloWorld/android/keystores/debug.keystore'
```

Delete `node_modules` directory first

#### 4. Python 2.7
```
WARNING: Output when parsing /Users/lavekush/work/android-tokopedia-core/customerapp/BUCK:
| Traceback (most recent call last):
|   File "/Users/lavekush/work/android-tokopedia-core/.buckd/tmp/buck_run.Xt7LNQ/buck_python_program516334172286234110/__main__.py", line 10, in <module>
|     from buck_parser import buck
|   File "/Users/lavekush/work/android-tokopedia-core/.buckd/resources/26845eb89ba4464586787533d08984a993f247d4/buck_server/buck_parser/buck.py", line 6, in <module>
| ModuleNotFoundError: No module named '__builtin__'
Parsing buck files: finished in 1.6 sec
BUILD FAILED: Buck wasn't able to parse /Users/lavekush/work/android-tokopedia-core/customerapp/BUCK:
No content to map due to end-of-input
 at [Source: com.google.common.io.CountingInputStream@65ab134a; line: 1, column: 0]
```

Make sure you have Python 2.7 installed and must be present in `path` variable of system, with 777 permission

#### 5. Jar not found
```
BUILD FAILED: The rule //.okbuck/cache:YouTubeAndroidPlayerApi.YouTubeAndroidPlayerApi.jar could not be found.
Please check the spelling and whether it exists in /Users/zulfikarrahman/Documents/worktokopedia/.okbuck/cache/BUCK.

This error happened while trying to get dependency '//.okbuck/cache:YouTubeAndroidPlayerApi.YouTubeAndroidPlayerApi.jar' of target '//sellerapp:src_stagingDebug'
```
If you were prompted with jar not found error, please delete cache folder on `.okbuck/cache` and rebuild project using `./buckw build`

#### 6. Design
If you find any issue with design (icon, view, or some sh*t) when build with `buck`. That maybe because duplicate naming variable at `strings.xml`, `dimens.xml`, `styles.xml`, `themes.xml` or `drawable`. So be careful :) 

