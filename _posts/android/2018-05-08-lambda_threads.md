---
header:
   image_fullwidth: "wallebanner.jpg"
layout: page
title:  "Lambda Threads in Android"
teaser: "More elegant multithreading."
breadcrumb: true
categories:
    - android
tags:
    - blog
    - content
    - post
      
---
<!--more-->

You'll need to <a href="/android/installing_retrolambda/">install Retrolambda</a> in Android Studio to use lambdas.
<br>
<h5>Example: without a lambda</h5>
```java
new Thread(new Runnable() {
    public void run() {
        Log.d("THREAD", "Hello World\n");
    }
}).start();
```

<h5>Example: with a lambda</h5>
```java
new Thread(() -> {
    Log.d("THREAD", "Hello World\n");
}).start();
```

I love creating and running threads "in-line" with just two lines of code.<br>It's more readable than defining a `Runnable` in one place and inserting it into a `Thread` elsewhere.

<h5>For example,</h5>
```java
public void sendHello() {

    doSomething();
    doMoreSomethings();

    new Thread(() -> {
        try {
            mOutputStream.write("Hello World!".getBytes());
            mOutputStream.flush();
        } catch (IOException e) {}
    }).start();

    doSomethingElse();
    doMoreSomethingElses();
}
```
