---
header:
   image_fullwidth: "wallebanner.jpg"
layout: page
title:  "Installing Retrolambda in Android Studio"
teaser: "De-uglify your Android code."
breadcrumb: true
categories:
    - android
tags:
    - blog
    - content
    - post
      
---
<!--more-->
Retrolambda lets you use <a href="/android/lambda_threads/">lambdas</a> in Android Studio!

In `build.gradle (Project: YourProj)`, you'll need to add the line
```python
classpath 'me.tatarka:gradle-retrolambda:3.7.0'
```
to `dependencies {}.` For example:

```python
...
buildscript {
    repositories {
        google()
        jcenter()
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.1.2'
        classpath 'me.tatarka:gradle-retrolambda:3.7.0'
    }
}
...
```

At the end of the same file, add the line
```python
apply plugin: 'me.tatarka.retrolambda'
```

Then, to `"build.gradle (Module: app)"` you'll need to add the lines:
```python
compileOptions {
    sourceCompatibility JavaVersion.VERSION_1_8
    targetCompatibility JavaVersion.VERSION_1_8
}
```
to `android {}.` For example:

```python
android {
    ...
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('...'), '...'
        }
    }
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
    ...
}
									
```

Awesome! Now sync your gradle files and test things by pasting this into your code:
```java
new Thread(() -> {
    Log.d("THREAD", "Hello World\n");
}).start();
```

<a href="https://github.com/evant/gradle-retrolambda">Check the Github page</a> if you have problems.