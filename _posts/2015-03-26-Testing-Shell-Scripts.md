---
layout: post
title: Testing shell scripts
---

This [story] (https://bugzilla.redhat.com/show_bug.cgi?id=1202858) highlights the potential dire consequences of undefined variables in Shell scripts.
In a nutshell this command: 
{% highlight %}
rm -rf "$VAR/ * 
{% endhighlight %}
when executed with $VAR left undefined, then becomes 
{% highlight %} rm -rf * {% endhighlight %}

, and will delete all files in the current directory and subdirectories. oops.


It's somewhat paradoxical that Shell scripts are frequently used to drive mission-critical activities such as starting/stopping processes,
copying, moving and deleting files... and yet these scripts are error-prone, often hard to read and always hard to test.

<a href=""><img src="/images/slipperyslope.jpg" align="middle" height="258" width="348" ></a>


Mitigations

Being at the mercy of a buggy shell script is not fun. Thanksfully there are ways to prevent disaster from happening.

- **Add "set -eu" to the script.**

 "-e" causes the script to terminate if any command fails.
 "-u" causes the script to terminate when it encounters an unbound variable.
One additional line of code which will save lot of trouble... should be mandatory on top of every script.

- **Check if the variables are set before use**

   `[[ "$VAR" ]] && rm -rf "$VAR/*"`

   It's not foolproof though as it wont prevent failure due to typos in the variable name.
 
- **Use a unit test framework**

 Yes shell scripts have their unit-test frameworks too, see [Roundup] (http://bmizerany.github.io/roundup/)
 or [ShUnit] (https://code.google.com/p/shunit2/). 

- **Use a (real) programming language**

  Drop the shell interpreter bash/zsh... and replace with Python, or Perl, or Groovy. Programming languages have much better support for functions,
  variable scoping, conditionals, string handling ...etc. compared to a shell script. 
  The idea is to avoid shell scripts save for the simplest tasks, and use a programming language to handle any kind of elaborate control
  logic (anything less complex than a pair of if/else statements).




 
 
 
 
