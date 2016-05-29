---
layout: post
title: "Working with legacy code"
date: 2016-05-28 10:30:00
---

The legacy code is a part of our daily job that we have to face them every hour. Sometimes we have to use them or build sometime new code block on them. Or even worse we have to refactor them and extract the part we needed in the new requirement. The well designed code should be easier to reuse and have a clearer logic. But most of the time the code we met is a mess.

Recently I just get a work for such situation and got a lot of problem to resolve. Here list some trap or tips that I met in my coding life.  

OK Let's kick start!

##Check the test coverage and the test case
Sometimes you just refactor a big block of your code and click the test button. All the test case are passed. A voice may be from your heart "My refactor works, what a magic!". But is it really ok? There may be some hidden issues come from your refactor. How to avoid this?

Before your refactor you need to check the test coverage for the block that you want to replace or extract. Make sure you already write the equivalent test case for your new code. But is the test coverage means everything? I am afraid not. You still need to check your test case. Sometimes the legacy test case not really fit the requirement, and they just could get passed.

##Limit your refactor scope
To make sure the effect that brought by your new code is small. You should limit your refactor scope. Do not just create a abstract class that replace all the same code you saw in those classes. Sometimes you could not know the scope that a abstract may affect. The current class maybe ok, but it may bring some new bugs in the follow process. Always check where those code should be placed. Once to create some value object make sure they should be create in some factory class rather in abstract class.

{% highlight java %}
//Do not create a abstract for a value object
class AliPayAccout extends AbstractAccount {
  //overwrite some field
}
class UnionPayAccount extends AbstractAccount {
  //overwrite some field
}
class ApplePayAccount extends AbstractAccount {
  //overwrite some field
}

//Use composite replace inheritance
class AliPayAccout {
  AccountInfo accountInfo = new AliPayAccountInfo();
  //... some other field
}
class UnionPayAccount {
  AccountInfo accountInfo = new UnionPayAccountInfo();
}
class ApplePayAccount {
  AccountInfo accountInfo = new ApplePayAccountInfo();
}
{% endhighlight %}

##The null-checking
The billion dollar mistake. We often saw some statements like `something != null` in our codes. Someone was thinking this is a good practice for programming, but it depends. For example the below code snip.

{% highlight java %}
AccountInfo accountInfo = getAccountInfo(context);
if (accountInfo == null) {
  //some code here
} else {
  //some code here
}
{% endhighlight %}

First you have to think if it is valid to get a null reference of `AccountInfo` here. When such kind of code could pass the former validation part. If here get a null account it makes no sense. The program should already fail in the former part rather that here. There are already lots of best practice for such problem such as [Null Object Pattern](https://en.wikipedia.org/wiki/Null_Object_pattern), [Optional in jdk8](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html), [Optional in guava for the java version less than jdk8](https://google.github.io/guava/releases/19.0/api/docs/com/google/common/base/Optional.html). The annotation `@Null` and `@NotNull` also great for using because some IDE such as [IntelliJ IDEA](https://www.jetbrains.com/idea/) could detected it and displayed in your workspace.

Someone like to separate the code to safe part(with null checking) and non-safe part(without null checking), it is also a great practice and easy for testing and simulation. But the code should be well encapsulated to prevent mistake. I really like the design in [Kotlin](https://kotlinlang.org/) that if you assign a null to the subclass of Any() and the code could not compile.

##Data object
If you working on the system which based on a data flow the data object could be seen everywhere. Lots of business logic come with those data objects. Someone like to use an interface to hidden the data object behind but it always bring some unnecessary fields and conditions. To work with legacy code, the [adaptor pattern](https://en.wikipedia.org/wiki/Adapter_pattern) sometimes is useful for data conversion. Better to create the new object with a [factory method pattern](https://en.wikipedia.org/wiki/Factory_method_pattern) or [static factory method](http://stackoverflow.com/questions/929021/what-are-static-factory-methods) to describe the new object.

{% highlight java %}
class AccountAdaptor {
  private AccountAdaptor(OldAccount account) {
    //some converter here
  }

  private NewAccount getAccount() {
    //return the new converted object
  }

  public static NewAccount createAccount(OldAccount oldAccount, OtherInfo otherInfo) {
    AccountAdaptor adaptor = new AccountAdaptor(oldAccount);
    //use other info
    return adaptor.getAccount();
  }
}
{% endhighlight %}

If you want to talk more about how to work with the legacy code, welcome to send me a email.
