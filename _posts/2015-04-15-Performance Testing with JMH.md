---
layout: post
title: Performance testing with JMH
---

[The previous post] (http://eleco.github.io/Monitoring%20metrics%20with%20Netflix%20Servo/) focused on adding new monitoring metrics using the Servo library. Before such a change goes into production it usually is a good idea to measure the performance impact of the library, especially so when it impacts code on the critical path of the application. 

To do this we need a java performance harness, and this is where [JMH] (http://openjdk.java.net/projects/code-tools/jmh/) the 
micro-benchmark framework for Java comes into play.

* The JMH benchmark file below defines two simple benchmark tests: one test for Servo's counter increment method and the other for the maxgauge update method. 
* The warmup phase, number of iterations and forks are all configurable via JMH Java's api. 
* A nice touch is the ability to specifiy a set of possible parameters directly in the code via the @Param annotation. JMH will cycle through the parameters and run all tests with each possible value: here both the counter and maxgauge will be tested twice, once with object registration turned on, and a second time with object registration turned off.

{% gist 4f7fe0b042efdd88fe95 %}



And the results:
    &nbsp;
<a href=""><img src="/images/jmh_run.png" align="middle"  ></a>


