---
title: "Downgrade java version in MacOS"
author: "Othmane Rifki"
date: 2020-04-12T14:41:32+02:00
description: ""
type: technical_note
draft: false
---

## Downgrade java version
Sometimes you need to run applications that require a lower java version.

* First check which version you are running: `java --version`
``` bash
openjdk 16.0.1 2021-04-20
OpenJDK Runtime Environment Homebrew (build 16.0.1+0)
OpenJDK 64-Bit Server VM Homebrew (build 16.0.1+0, mixed mode, sharing)
```
* Download the java version you want from http://jdk.java.net/
* Follow the installation instructions
* Check which versions are installed: `/usr/libexec/java_home -V`
``` bash
Matching Java Virtual Machines (2):
    16.0.1 (x86_64) "Homebrew" - "OpenJDK 16.0.1" /usr/local/Cellar/openjdk/16.0.1/libexec/openjdk.jdk/Contents/Home
    14.0.2 (x86_64) "Oracle Corporation" - "Java SE 14.0.2" /Library/Java/JavaVirtualMachines/jdk-14.0.2.jdk/Contents/Home
/usr/local/Cellar/openjdk/16.0.1/libexec/openjdk.jdk/Contents/Home
```
* For example, i would like to set Java14: `export JAVA_HOME=`/usr/libexec/java_home -v 14.0.2`
* Add it to my .zsh_aliases: `echo "export JAVA_HOME=`/usr/libexec/java_home -v 14.0.2`" >>  ~/.zsh_aliases`
* Checking the java version installed: 
```bash 
java 14.0.2 2020-07-14
Java(TM) SE Runtime Environment (build 14.0.2+12-46)
Java HotSpot(TM) 64-Bit Server VM (build 14.0.2+12-46, mixed mode, sharing)
```