---
layout: post
title: "Run JUnit from Terminal on MacOS"
---

Download the latest version of JUnit from
[here](https://github.com/junit-team) and place the jar's in a sensible
location. I've gone with `~/java-junit/`.

Configure your environment variables to include the path to the location of the
JUnit jar's by adding the following to your shell's profile:

```bash
export JUNIT_HOME="$HOME/java-junit"
export PATH="$PATH:$JUNIT_HOME"
export CLASSPATH="$CLASSPATH:$JUNIT_HOME/junit-4.12.jar:$JUNIT_HOME/hamcrest-core-1.3.jar"

alias junit="java org.junit.runner.JUnitCore"
```

JUnit tests can now be executed using `junit JUnitTestClass`.