---
layout: post
title: Migrating from Play to the Ninja Framework
---


[The PlayFramework](https://www.playframework.com/) has long been my framework of choice. It stands out in the crowded space of jvm web frameworks in particular because it is (relatively) lightweight, with a short learning curve, and a focus on ease of testing both at the unit and functional level.

So far so good. However. The core logic of the framework is mostly written in Scala, and it shows:

- view templates have to be scripted using Scala
- the build tooling uses SBT instead of the Maven/Gradle alternatives favored by the majority of Java projects
- a Scala/SBT plugin is required to compile the code in Intellij and Eclipse. Can be fidly to setup and fragile to run.
- long build times, curtesy of the Scala compiler

In other words the Scala roots of the framework are leaking in user space...These are little annoyances, from the standpoint of a Java programmer which is not particularly in writing Scala code, and are not deal-breaking but they do add up, so much so that at times this negates the productivity bonus brought on by the framework.


The Ninja Framework
-------------------

<a href=""><img src="/images/Ninja_The_Last_Thing_You_See.jpg" align="middle" height="258" width="348" ></a>


[The Ninja framework](www.ninjaframework.org/) is heavily inspired by Play, with the same focus on simplicity and performance, the same functionality (at a basic level at least i.e both frameworks provide routers, controllers,filters...). The API is also very familiar. 

Above all this is a pure Java (no Scala) framework so it removes all of the concerns highlighted above. Plus it has a cool name. So all in all  it's an easy tradeoff.


Migrating from Play to Ninja 
----------------------------

This is fairly easy, largely due to the near identical API. Amongst the salient points:

1. create a pom.xml with Ninja framework dependencies at the root of your Play project (examples available on the NinjaFramework website)

2. setup your project as a Maven project. In Intellij this is done with a right-click on the pom above and select "Add as a Maven project"

3. replace all of the play.* imports by their equivalents ninja.

4. create a Java class to host the route configuration (this is a property file in Play)

5. some of the properties in the application.conf may differ from Play to Ninja - no shortcut here they have to be analysed on a case by case basis.

6. (the best part) remove the scala cruft: scala plugin, delete Build.scala, plugins.sbt. 

7. Watch your compilation time plummet. Enjoy.


