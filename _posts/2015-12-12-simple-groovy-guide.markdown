---
layout: post
title: "Groovy, please try!"
date: 2015-12-12 12:30:00
---

For a java programmer sometimes need to write some POC program. The program changed often, sometimes you feel tired to move a lot of interfaces, factories, builders and services. Refactor takes a lot of time and also may create more structure class in your program. Under such situation you may want some dynamic feature for Java, but it is impossible. [Groovy](http://www.groovy-lang.org/) was birth for this. I really recommend you to try such programming language.

# How to install

For window, you can visit [groovy download page](http://www.groovy-lang.org/download.html) to download. For Mac OSX, Linux  user better to use [SDKMAN](http://sdkman.io/) to download and configure any Groovy version of your choice. You may also need to install [Grails](https://grails.org/index.html) for web development, SDKMAN can also help you to handle it.

{% highlight bash %}
$curl -s get.sdkman.io | bash
#You need reopen a session
$sdk install groovy
#Check if you successful installed it
$groovy -version
{% endhighlight %}

# Your first program

Please open your favorite editor to input below code and save as `MyGroovyScript.groovy`

{% highlight groovy %}
println 'Hello Groovy!'
{% endhighlight %}

Then in your command type

{% highlight bash %}
groovy MyGroovyScript.groovy
{% endhighlight %}

You will see your screen prints `Hello Groovy!`

# Some String magic

In groovy single quoted strings are plain `java.lang.String` object. You can simple use `==` to compare two string's value are equal. No need to use the `String.equals()` method.
{% highlight groovy %}
def value = 'a string'
assert 'a string' == value
{% endhighlight %}
Please try to modified the `==` to `!=`, you can see a more powerful assert in Groovy which I love the most. As you see there's no semicolon at the end of the line. This becomes not necessary in Groovy.

Any Groovy expression can be interpolated in all string literals, apart from single and triple single quoted strings. This is a little bit like [Perl](https://www.perl.org/) and very useful when you process some text;
{% highlight groovy %}
def name = 'Rex'
def greeting = "Hello ${name}"
assert greeting.toString() == 'Hello Rex'
{% endhighlight %}

# Collections
Groovy also uses some Java collections. Groovy lists are plain JDK `java.util.List` the default implementation are `java.util.ArrayList`. It can also changed by using `as`.
{% highlight groovy %}
def numbers = [1, 2, 3]
assert numbers instanceof List
def linkedList = [2, 3, 4] as linkedList
assert linkedList instanceof java.util.LinkedList
{% endhighlight %}
You can fast access a element in a list by its index. If use a negative index, it will count from the backend. Btw also can use a rang to access a list which really readable.
{% highlight groovy %}
def numbers = [1, 2, 3]
assert number[0] == 1
assert number[-1] == 3
assert number[0..1] == [1, 2]
{% endhighlight %}

Groovy creates maps are instances of `java.util.LinkedHashMap` which a little like Spring map injection.
{% highlight groovy %}
def info = [name: 'Rex', age: 50]
assert info['name'] == 'Rex'
assert info.age == 50
// Insert a element
info['gender'] = 'male'
assert info.gender == 'male'
{% endhighlight %}

# Closures
A closure in Groovy is an anonymous, block of code that can pass in arguments and return a value. A little complex? Haha, let's learn it from coding.
{% highlight groovy %}
// Syntax
{ [param -> ] statements}
// Try some simple
// Convert to upper case
def convertToUpperCase = {
  str -> str.toUpperCase()
}
assert convertToUpperCase('rex') == 'REX'
// With 2 params
def sum = {
  a, b -> a + b
}
assert sum(1,2) == 3
// Varargs
def concatString = {
  String... args -> args.join('-')
}
assert concatString('I','Love','Groovy') == 'I-Love-Groovy'
{% endhighlight %}

With closure we can try functional programming in Groovy.
{% highlight groovy %}
//This is an example for calculate the Fibonacci
def fib //Need to define first or will throw MissingMethodException
fib = {
  long n -> n<2?n:fib(n-1) + fib(n-2)
}
assert fib(20) == 6765
// To make it execute fast can cache the former result by memoize()
fib = {
  long n -> n<2?n:fib(n-1) + fib(n-2)
}.memoize()
{% endhighlight %}

# The nuclear boom: Domain-Specific Language
The most powerful feature in Groovy should be the [DSL(Domain-Specific Language)](https://en.wikipedia.org/wiki/Domain-specific_language) support. Some modern building tools such as [Gradle](http://gradle.org/) are base on this. With this you can try to build your own language parser. The blow example comes from the official document from [groovy-lang](http://www.groovy-lang.org/dsls.html), you can find more details from there.

Now we create a DSL with the following structure
{% highlight groovy %}
email {
  from 'dsl-guru@mycompany.com'
  to 'john.doe@waitaminute.com'
  subject 'The pope has resigned!'
  body {
    p 'Really, the pope has resigned!'
  }
}
{% endhighlight%}

Then implementing such a builder is usually done the following way:
{% highlight groovy %}
def email(Closure cl) {
  def email = new EmailSpec()
  def code = cl.rehydrate(email, this, this)
  code.resolveStrategy = Closure.DELEGATE_ONLY
  code()
}
{% endhighlight%}

We also need to build the spec for a DSL and pass to the builder to execute
{% highlight groovy %}
class EmailSpec {
  void from(String from) { println "From: $from"}
  void to(String... to) { println "To: $to"}
  void subject(String subject) { println "Subject: $subject"}
  void body(Closure body) {
    def bodySpec = new BodySpec()
    def code = body.rehydrate(bodySpec, this, this)
    code.resolveStrategy = Closure.DELEGATE_ONLY
    code()
  }
}
{% endhighlight%}

Then the type checker will know if an `email` method accepting a Closure.
{% highlight groovy %}
@groovy.transform.TypeChecked
void sendEmail() {
  from 'dsl-guru@mycompany.com'
  to 'john.doe@waitaminute.com'
  subject 'The pope has resigned!'
  body {
    p 'Really, the pope has resigned!'
  }
}
{% endhighlight%}
It is magic right?

# Some other useful tools
There are some useful tools build on Groovy. Let me take a short tour.

#### Gradle
[Gradle](https://gradle.org) is a modern building tools. Now is the official recommend building tool for Android Developer. Gradle build on Groovy DSL, which is a better solution for construct building steps. To compare with Maven, with a Java plugin in Gradle, the build script can be like this:
{% highlight groovy %}
apply plugin: 'java'
repositories {
  mavenCentral()
}
dependencies {
  compile group: 'commons-collections', name: 'commons-collections', version: '3.2'
  testCompile group: 'junit', name: 'junit', version: '4.+'  
}
sourceCompatibility = 1.5
version = '1.0'
jar {
  manifest {
    attributes 'Implementation-Title': 'Gradle Project',
               'implementation-Version': version
  }
}
{% endhighlight%}

#### Grails
[Grails](https://grails.org/index.html) is a powerful web framework which including integrated ORM, Domain-specific  Language, runtime and compile-time meta-programming and Asynchronous programming. If you want to develop a web application don't forget to take a try with this.
