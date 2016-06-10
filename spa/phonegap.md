# PhoneGap

Vamos a crear una aplicación mediante PhoneGap. Echa un [vistazo primero al diseño y  arquitectura de una aplicación en PhoneGap](http://media.formandome.es/phonegap/presentacion/phonegap_intro.html).

```
cordova run android
ANDROID_HOME=/home/juanda/Android/Sdk
JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
No target specified, deploying to emulator
Error: No emulator images (avds) found.
1. Download desired System Image by running: /home/juanda/Android/Sdk/tools/android sdk
2. Create an AVD by running: /home/juanda/Android/Sdk/tools/android avd
HINT: For a faster emulator, use an Intel System Image and install the HAXM device driver
```

adb logcat para ver trazas de error:
```
06-10 23:53:59.258  2645  2645 D AndroidRuntime: >>>>>> START com.android.internal.os.RuntimeInit uid 0 <<<<<<
06-10 23:53:59.259  2645  2645 D AndroidRuntime: CheckJNI is ON
06-10 23:53:59.274  2645  2645 D ICU     : No timezone override file found: /data/misc/zoneinfo/current/icu/icu_tzdata.dat
06-10 23:53:59.290  2645  2645 E memtrack: Couldn't load memtrack module (No such file or directory)
06-10 23:53:59.290  2645  2645 E android.os.Debug: failed to load memtrack module: -2
06-10 23:53:59.291  2645  2645 I Radio-JNI: register_android_hardware_Radio DONE
06-10 23:53:59.298  2645  2645 D AndroidRuntime: Calling main entry com.android.commands.pm.Pm
06-10 23:53:59.305  2335  2347 D DefContainer: Copying /data/local/tmp/android-debug.apk to base.apk
```
Aumentamos la VM Heap a 512