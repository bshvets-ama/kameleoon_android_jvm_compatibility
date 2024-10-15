# kameleoon_android_jvm_compatibility

This is a sample Flutter project that demonstrates the issue with the Kameleoon Flutter SDK on Android when using JDK 17.
Additional setup: Gradle 8.4, Android Kotlin plugin (org.jetbrains.kotlin.android) 1.9.23

## Issue
Android build fails with the following error:
```
FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':kameleoon_client_flutter:compileDebugKotlin'.
> Inconsistent JVM-target compatibility detected for tasks 'compileDebugJavaWithJavac' (1.8) and 'compileDebugKotlin' (17).

  Consider using JVM Toolchain: https://kotl.in/gradle/jvm/toolchain
  Learn more about JVM-target validation: https://kotl.in/gradle/jvm/target-validation 

* Try:
> Run with --stacktrace option to get the stack trace.
> Run with --info or --debug option to get more log output.
> Run with --scan to get full insights.
> Get more help at https://help.gradle.org.
```

The issue is mentioned in kotlinlang docs: https://kotlinlang.org/docs/gradle-configure-project.html#what-can-go-wrong-if-targets-are-incompatible:
> JVM target incompatibility occurs if you:
> * ...
> * Have a default configuration, and your JDK is not equal to 1.8.


## Solution

To fix the issue specify the kotlin `jvmTarget` in the `kameleoon_client_flutter/android/build.gradle` file:
```groovy
android {
    kotlinOptions {
        jvmTarget = '1.8'
    }
}
```

