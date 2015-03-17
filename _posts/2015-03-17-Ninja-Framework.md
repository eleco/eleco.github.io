---
layout: post
title: The Ninja Framework
---


The PlayFramework has long been my framework of choice. It stands out in the crwoded space of jvm web frameworks because:

- it is (relatively) lightweight

- with a short learning curve

- and a focus on ease of testing both at the unit and functional level.

So far so good. However. The core logic of the framework is mostly written in Scala, and it shows:

- view templates have to be scripted using Scala

- the build tooling uses SBT instead of the Maven/Gradle alternatives favored by the majority of Java projects

- a Scala/SBT plugin is required to compile the code in Intellij and Eclipse. Can be fidly to setup.

- long build times curtesy of the Scala compiler
- 

These little annoyances are not deal breaking but they do add up, so much so that at times this negates the productivity bonuses brought on by the framework.

The Ninja framework is heavily inspired by Play, with the same focus on simplicity and performance, the same functionality (at a basic level at least i.e both frameworks provide routers, controllers,filters...). The API is also very familiar. 

Above all this is a pure Java (no Scala) framework so it removes all of the concerns highlighted above. Plus it has a cool name. So all in all  it's an easy tradeoff.


Finally migrating from Play to Ninja is fairly simple (largely due to the near identical API). Amongst the salient point:
   * create a pom.xml with Ninja framework dependencies at the root of your Play project (examples available on the NinjaFramework website)
   * setup your project as a Maven project. In Intellij this is done with a right-click on the pom above and select "Add as a Maven project"
   * replace all of the play.* imports by their equivalents ninja.*
   * create a Java class to host the route configuration (this is a property file in Play)
   * some of the properties in the application.conf may differ from Play to Ninja - no shortcut here they have to be analysed on a case by case basis.
   * (the best part) remove the scala plugin delete Build.scala, plugins.sbt. Watch your compilation time plummet.

Enjoy.

