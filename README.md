# "WebRTC Native Stack is considered as a single chain as close to the Hardware Abstraction Layer (HAL) as possible."


**Getting Started**
------
This repository involves a **Step by Step Guide to Build Android App based on WebRTC Native Stack.** As we all know, Android Programs run into Dalvik Virtual Machine. Native Development tool (NDK) allows users to execute some of the program using native code languages such as `C/C++`.

------
# NDK:

[NDK (Native Development Kit)](https://developer.android.com/ndk/guides) includes the following features such as;

- Tool and build files needed to generate a native code base from `C/C++`.
- Embed consistent native libraries in application packages files (.apk files) that can be deployed on Android devices.
- Supports a number of native system header files and libraries for the Android platform.

Here you can select & download the latest or lagecy NDK package for your development platform i.e. [NDK Download](https://developer.android.com/ndk/downloads)

------
# Why NDK?

NDk finds its best use to squeeze extra performance out to device, to achieve low latency or run computationally intensive applications on android platform. Here are some other reasons why we use NDK in our development;

- Easy to port libraries written in `C/C++` can be easily reused on other embedded platforms.
- Code protection, because the java code of apk can be easily decompiled, and the `C/C++` library is difficult to reverse.
- Call third-party `C/C++` libraries in the NDK, because most open source libraries are written in `C/C++` code,
such as WebRTC, TarsosDSP, Ffmpeg, OpenCV, and a lot of other machine learning stuff etc. 

------
# What is JNI?

[JNI (Java Native Interface)](https://docs.oracle.com/javase/8/docs/technotes/guides/jni/index.html) provides several APIs to implement the communication between Java and other languages (mainly `C/C++`). 

Drawback: There is one of the major side effect of JNI is, *The Program is no longer Cross-Platform*. To make your program Cross-Platform, you must recompile the native language part in different system environments. The program is no longer absolutely secure, and *improper* use of native code may cause the entire program to crash. As a general rule, you should focus your local methods on a few classes. This reduces the coupling between `JAVA` and `C`.

 In fact, Java and C/C++ are static type languages, the main reason that java and C cannot communicate is the problem of data types. JNI plays a role in data conversion. The corresponding relationship is shown in the following table:
 
 ![JNI Types and Data Sturctures](https://github.com/mail2chromium/Android-Native-Development-For-WebRTC/blob/master/types.png)

-----

 # NDK and JNI Workaround:
 
To put it simply, NDK is an extension toolkit developed by JNI. It uses NDK to compile corresponding local [static or shared libraries](https://stackoverflow.com/questions/2649334/difference-between-static-and-shared-libraries) that can be run for different mobile devices (`ARM, x86 ...`). In order to improve the sorting efficiency and use `C/C ++` in android, here are different steps for this process are: 

1. SDK development (write java code, write code containing native keywords to start JNI)([Native Methods](http://journals.ecs.soton.ac.uk/java/tutorial/native/index.html)) .

2. JNI development (according to the JNI coding specification, write a local interaction with java Code, the role is to talk about the `C/C++` data type conversion into Java can recognize).

3. `C/C++` development (write business logic, or call the local API or library provided by the NDK to complete the development of specific functions).

4. NDK compilation ( Write the .mk file, compile and debug, modify the .mk file, and optimize the compilation results for the specific platform (`ARM/X86`).

5. SDK compilation and packaging.

-----

# Installation and Configurations

Here we start with;

1. Download Source Code:

As we know that WebRTC implementation is done in `C/C++` languages. It needs to integrate with android application via Java Native Interface(JNI). WebRTC source available at [Github WebRTC Source Code](https://github.com/JumpingYang001/webrtc.git) as well as official WebRTC [download page](http://webrtc.github.io/webrtc-org/native-code/development/).

2. Setup Android NDK:

To integrate WebRTC code via JNI, first I needs setup android NDK. Download NDK from [here](https://developer.android.com/ndk/downloads) and extract it. Main thing to consider here is, make sure NDK path is being setup in environment variables in windows i.e. [see](https://subscription.packtpub.com/book/application_development/9781849691505/1/ch01lvl1sec09/setting-up-an-android-ndk-development-environment-in-windows). 

To test whether ndk-build is working or not, check these commands in the terminal like;

```
  ndk-stack
  ndk-build --help
```

**Example:**

Before digging into WebRTC Native Stack, If you don't have a basic understanding of NDK development, 
I must recommend you to follow this tutorial i.e [Hello-JNI](https://github.com/android/ndk-samples/tree/master/hello-jni).

-----

# WebRTC with Android:

Following are the steps that I have followed to integrate WebRTC source code with my android application. 

1. [Creating an Android Project](https://developer.android.com/training/basics/firstapp/creating-project)

2. Importing WebRTC Source to Android Project:

I have a seperated directory called `webrtc` inside the jni directory and added WebRTC source code for it. WebRTC source code can be cloned from [github](https://github.com/JumpingYang001/webrtc.git) or download via official [download page](http://webrtc.github.io/webrtc-org/native-code/development/).

![Android WebRTC Project Structure](https://github.com/mail2chromium/Android-Native-Development-For-WebRTC/blob/master/structure.png)

Make sure your project structure follow the same hierarchy as given above.

3. Write a Java class that uses native code of `C/C++`:

I have maintained and updated `Apm.java` in my Android Project as given here;

![Android WebRTC Project Structure](https://github.com/mail2chromium/Android-Native-Development-For-WebRTC/blob/master/apm.png)































