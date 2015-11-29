---
layout: post
title: "How to build a small FX trading system"
date: 2015-11-29 20:30:00
---

Last month just finished a trading game in my corp. From zero to one to build a trading system is a great experience. This post just a brief to make a trading system from zero to one. If you want to talk more, please contact me at the below link.

### What is a trading system
From [investopedia](http://www.investopedia.com/university/tradingsystems/tradingsytems1.asp) we can conclude that a trading system is a simply a group of specific rules, or parameters, that determine entry and exit point for a given equity. So we can infer that there are several point for a trading system.

- Trading rules(the algorithm)
- Signal
- Execution system.

So your trading system need to be designed base on those above rules. You need watching the market data, analysis the data if it matches your algorithm, send the order to the exchange system and wait for the execution result and hold your position.

### Some basic info for FX trading
Before you setup your system, there are some basic terminology you should know.

- The [currency pair](http://www.investopedia.com/terms/c/currencypair.asp). This is the quotation and pricing structure of the currencies traded in the forex market. For example USD/CHF, the first currency of a currency pair is called the "base currency", and the second currency is called the "quote currency".
- The [position](http://www.investopedia.com/terms/p/position.asp). The amount of a symbol(such as USD/CHF) either owned(long position) or borrowed(short position).
- The [take profit order](http://www.investopedia.com/terms/t/take-profitorder.asp). An order to close out current position for a profit.
- The [stop loss order](http://www.investopedia.com/terms/s/stop-lossorder.asp). An order to limit the current position in a security.

### Pick up your tech stack and write your program
First of all, choose an environment to host your program. Because the game hold in my crop are based on the cloud platform [CloudFoundry](https://www.cloudfoundry.org/). So my program was built on this [PaaS](https://en.wikipedia.org/wiki/Platform_as_a_service) platform. Make sure your hosting support the programming language you choose, if you got your own virtual server that you can build the runtime you like.

I use JAVA to build my system, the total system integrated by the [spring-framework](http://spring.io/). I recommend the spring-boot tools to build your system's prototype which really really fast to integrate the service you need. To receive the [ticks](http://www.investopedia.com/terms/t/tick.asp) from the exchange or the market you may need a websocket client service. It is very easy to add the websocket dependency in your system by add the following code in your pom.xml.

{% highlight xml %}
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-websocket</artifactId>
</dependency>
{% endhighlight %}
