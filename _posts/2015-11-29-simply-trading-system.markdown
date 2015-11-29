---
layout: post
title:  "How to build a small FX trading system"
date:   2015-11-29 07:49:39
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

- Market Watching System

I use JAVA to build this system, the total system integrated by the [spring-framework](http://spring.io/). I recommend the spring-boot tools to build your system's prototype which really really fast to integrate the service you need. To receive the [ticks](http://www.investopedia.com/terms/t/tick.asp) from the exchange or the market you may need a websocket client service. If your exchange or market dose not provide a websocket feed. Then you need to build a socket server yourself. Using a 3rd party library can reduce the time you talk to native socket APIs. [Netty](http://netty.io/) would be helpful if you using JAVA.

- Algo System

After you set up your market watching system. Before you start you trading, you need to manage the market data. Data from the market are discrete, create a market data management system is necessary. Keep the market in your cache, if you got a database system, you can also put them in the database. From a period of market data. You can calculate some indicator that will trigger a [Singal](http://www.investopedia.com/terms/t/technicalanalysis.asp) to your main program.

- Order System

The order system used to execution an order which triggered by your algorithm engine. This system will send the order to the exchange and also your order book. You order book keeps all the order that generate from your algorithm. If it got the `ACK` from the exchange, the order system need to remove the order from the order book automatic. And the order will sync to your position system.

- Position System

The position system plays very import part in your trading system. It shows the current profit and lost in your trading system. It will trigger the take profit order or stop loss order. So the system need to integrate with your all your others system.  
