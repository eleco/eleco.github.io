---
layout: post
title: Monitoring metrics with Netflix Servo
---

Developing a metrics monitoring component seems simple, but deceptively so. 

Adding a simple counter component is easy enough, however more advanced functionalities (polling, filtering, exporting the results... ) are somewhat trickier to code. Also since
the metrics must be read and written in parallel with the core logic, the code must be multithreaded, which add another challenge: [concurrency is hard.] (http://blog.nirav.name/2011/03/why-concurrency-is-hard.html)

So an in-house solution is doable, although it will probably take at least a few days to develop, and that's assuming it's bug free.

The alternative is to re-use existing libraries which neatly solve this problem by providing monitoring components such as counter, gauges, timers, and the ability to export the data via JMX. For instance:

* [Netflix servo] (https://github.com/Netflix/servo)
* [DropWizard metrics] (https://dropwizard.github.io/metrics/3.1.0/)


The simple app below calculates as many prime numbers as possible for a specified period of time, and uses servo's counter and peak rate counter to keep track of the total number of primes discovered, and the maximum rates of primes discovered per second.

{% gist 71c084207c0a3b121dfc %}


The metrics are automatically exposed via JMX so Java Mission Control can pick it up and chart the resulting data.

<a href=""><img src="/images/servo_charts.png"  ></a>

<a href=""><img src="/images/servo_mbeans.png"  ></a>










