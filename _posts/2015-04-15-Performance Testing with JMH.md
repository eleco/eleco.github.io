
[The previous post] (http://eleco.github.io/Monitoring%20metrics%20with%20Netflix%20Servo/) focused on adding new monitoring metrics using the Servo library. 

It usually is a good idea to measure the performance impact of the project libraries, especially so when it impacts code on the critical
path of the application. 

To do this we need a java performance harness, and this is where the [JMH] (http://openjdk.java.net/projects/code-tools/jmh/) the 
micro-benchmark framework for Java comes into play.


The JMH benchmark file below tests Servo's counter increment and maxgauge updates operations. The warmup phase, number of iterations 
and forks are all configurable via JMH Java's api. A nice touch is the ability to specifiy a set of possible parameters directly in the code via the @Param annotation. JMH will cycle 
through the parameters and run all tests with each possible value.

{% gist 4f7fe0b042efdd88fe95 %}



And results:
[snapshot perf test]


