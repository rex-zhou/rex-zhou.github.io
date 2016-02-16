---
layout: post
title: "To design a better API"
date: 2016-02-16 10:30:00
---

Recently just finished a small project from API design to the whole progress processing. The API part built on the legacy system and followed by the guide of the original design. All the function included in the API module just to build an complex value object and pass to our system by the transport layer. The transport layer provides socket and MOM([Message Oriented Middleware](https://en.wikipedia.org/wiki/Message-oriented_middleware)) 2 communication ways. To reduce the cost of development between different team it is necessary to design a good API.

#API is the language you talk with others
Other system will access your system by calling your API. So the API should be easy to use and avoid to misuse even without documentation. It always plays as a contract to make agreement. The API user will understand what they could do and how to do thing in the right way.

Here's some characteristics of a good API. Some of them are from the [Effective API design](http://www.infoq.com/presentations/effective-api-design).

- Easy to learn and use
- Easy to read and maintain
- Easy to extend
- Self explanation
- Avoid misuse
- Provide necessary feedback for the caller

#General design principles
The API always implement as a prototype as write often with the spec growth. Make sure all of your codes published with an using example and unit tests in every iteration. Make your method a good name that can well explain the functionality.

####API design to abstraction rather than implementation
If your API provides an interface as the standard of the function. Make sure all the implementation take zero impact to the API. Please do not add some additional step in the same methods. If really need to do some calculation or value assignment, put them in a special step. Remember API should do one thing and do it well.

####Minimize the accessibility
Make sure the classes and members as private as possible. Better to build an immutable object if you use a builder. If a class is public, limit the necessary access function. Do not use a setter method to init a variable.

####Self explanation
There's some annotation could be detected by some IDE could also provide function as documentation. Try to use the `@Nullable` and `@NotNull` to mark a variable or a method. Then the user could do some check to avoid the `NullPointerException`

To make the method calling much safer in concurrent environment. We advice you to use the concurrent annotation like below.

{% highlight java %}
@ThreadSafe
public class Queue<E> implements java.util.Queue<E> {
  private ConcurrentLinkedQueue readWriteLock;

  @GuaredBy{ value="readWriteLock" }
  public boolean offer(E element) {
    return queue.offer(elemnt);
  }
}
{% endhighlight %}

####Using appropriate parameter and return types
Prefer interface types to classes for input. And also use most specific possible input parameter type.
For example if you provide a assign method with the `List` parameter as blow.
{% highlight java %}
public void setNameList(List<String> nameList) {
  //some code here
}
{% endhighlight %}

If you assign the nameList with the implementation of `com.google.common.collect.ImmutableList` which server side not contains. It will throw an exception of class not found.

####Avoid long parameter list
Do not provide interface like below, it will bring mistake and confuse the user. If there's no javadoc, user do not know how to input the params.
{% highlight java %}
public String queryIdBy(String arg1, String arg2, String arg3, String arg4, String arg5) {
  //some code here
}
{% endhighlight %}

API design is really a challenge job, if you have better idea welcome to discuss with me:)
