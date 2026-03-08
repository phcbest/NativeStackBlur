# NativeStackBlur
Android StackBlur with gradle support (only for the native method) https://github.com/kikoso/android-stackblur

As you may see, kikoso has not yet provided a way to add StackBlur as a gradle dependency easily. This library is an attempt to make the NativeBlurProcess availible through gradle without the need to import any modules or do any other configuration.

[![](https://jitpack.io/v/Commit451/NativeStackBlur.svg)](https://jitpack.io/#Commit451/NativeStackBlur)

# Gradle Dependency

Add this in your root `build.gradle` file (**not** your module `build.gradle` file):

```gradle
allprojects {
	repositories {
		...
		maven { url "https://jitpack.io" }
	}
}
```

Then, add the library to your project `build.gradle`
```gradle
dependencies {
    implementation("com.github.Commit451:NativeStackBlur:latest.version.here")
}
```

This library is provided as a "fat" aar with native binaries for all available architectures. To
reduce your APK size, use the ABI filtering/splitting techniques in the Android plugin:
http://tools.android.com/tech-docs/new-build-system/user-guide/apk-splits

# Usage
Usage is similar to StackBlur, but also more streamlined:

```
Bitmap bm = NativeStackBlur.process(source, blurRadius);
```

# Compiling
This project now builds `libblur.so` from source via CMake (`nativestackblur/src/main/cpp`).
Native binaries are generated during normal Gradle builds.

To build the library module directly:

```bash
./gradlew :nativestackblur:assemble
```

The native linker is configured with `-Wl,-z,max-page-size=16384`, so generated binaries are compatible with both 4KB and 16KB page-size Android devices.

License
--------

    Copyright 2022 Commit 451

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
