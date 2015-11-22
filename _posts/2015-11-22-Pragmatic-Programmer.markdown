---
layout: post
title:  "Pragmatic Programmer"
date:   2015-11-22 18:49:39
---

This article for those people who want to be more pragmatic in their daily life.
Most of the aspect mentioned below come from the real problem I meat in work. Those
just about some basic skill that a programmer should have, if you want more need
to find them yourself.

### An Editor
This is most important part in your daily working. You need to write your code,
process text, analysis the log and write the documents. Someone prefer to use an
IDE to write their code. That's a really good habit for collaborate working. You can
easily import you coding standard configuration make sure all of your partner writing
code follow the same guideline.

- [IntelliJ IDEA](https://www.jetbrains.com/idea/) One of the most powerful IDE. Great
designed for code refactor, code inception and lots of useful plugin.

- [Atom](https://atom.io) A text editor developed by [GitHub](https://github.com/). It
has thousands of open source packages, and you can also hacked it yourself.

- [Visual Studio Code](https://code.visualstudio.com/) A light weight font-end text editor
 developed by Microsoft. Now it just supports Javascript and ASP.NET maybe more feature in the future version.

- [Vim](www.vim.org) A must well used editor for back-end developer. It is hard to learn, but easy to use.

After you picked up your favorite editor, there are several steps need to concern.

- Setup your favorite color theme, coding and font. Because you may need to type for a long time.
- Setup your coding standard and plugin, make sure all of your environment follow the same guideline.
- Be familiar with your editor's keybindings. Don't make your hand break your mind. You can easily add
 a line, drop a line, replace some code and so on.
- Some editor well integrated with [Git](http://www.git-scm.com/), make sure you know the meaning.

### Version Control System
The [VCS](https://en.wikipedia.org/wiki/Version_control) not only for your code, also for your documents. Then you can
easily roll back to the former version or compare with the different version. Some of the documents type
such as word and excel are not suit for the VCS to compare, try the [markdown](http://daringfireball.net/projects/markdown/) file. Some of the above editors already support
the preview of the markdown file which are really great feature.

I recommend [GIT](http://www.git-scm.com/) as the default VCS. If you do not know how to use it
[this online guide](http://try.github.com/) can give you a short view on git. If you already a git
master [this free book](http://www.git-scm.com/book/en/v2) can also give you more info about it.

### The Programming Language
It is necessary to master a language in your work. Make sure you know the language feature in different version.
If it is a [object-oriented](https://en.wikipedia.org/wiki/Object-oriented_programming) language, you also need
to know some OOP design principle. Here's a check list please make sure you already take in charge of it.

- The language standard library(Data structure, File, Network, Thread model).
- The language memory model(GC or manual allocated).
- The common used third-party library(reduce the common mistake for build wheel.
- The common used data structure of the language(collections, hashtable).
- The I/O library(Also the network).
- The common used algo that already contains in the standard library(Binary search, sorting).
- The [design pattern](http://www.oodesign.com/) used for the language.
- Try to make it reactive(http://www.reactivemanifesto.org/).
- Having a toolkit that you can fast build a system from zero([Spring-Boot](http://projects.spring.io/spring-boot/)).
- The testing framework(*really import*).

#### A second language for your daily job.
Sometimes we need to process some data in a very short time or to build up a tiny
system to do some testing job. Then we need a language that can solve the problem very quickly.
[Python](https://www.python.org/), [Ruby](http://rubyonrails.org/) and [Node](https://nodejs.org/) have some
magic to help you do those things. Then you need to know:

- How to build a web server.
- How to build a RESTful services.
- How to manipulate and export data from database.
- How to process CSV file.
- How to process XML file.
- How to process JSON data file.
- How to process your log file.
- How to simulate network request and response for testing.
- How to fetch data from internet or web page.
- Regular Expression(*It is ok to put it here?*).

### The Operation System
No matter what operation system(Windows, Linux, Unix, Mac OS) you are using. Better to know some basic knowledge
 about it. Make sure you can handle some problem yourself. Such as setup your account, install and remove software.
 Know some benchmark of your system such as memory usage, CPU usage, network I/O usage. There's a must know list below:

- A shell for your OS([Power shell](https://technet.microsoft.com/en-us/library/bb978526.aspx) for Windows. [Bash](https://en.wikipedia.org/wiki/Bash_%28Unix_shell%29) for \*nix).
- System diagnosis command(`top`,`ifconig`,`netstat`,`df`...).
- File and directory manipulating command(`rm`,`mkdir`,`chmod`...).
- File watching command(`more`, `less`, `tail`...).
- File process command(`sed`, `awk`).

All of the above skill just make sure you have basic knowledge for being a programmer. But you still need
to do more to make you outstanding.

### What's Next
I know, some of you already good at all the mentioned above. You still want more right? Ok I will show you more
about what I think necessary for a pragmatic programmer should have.

- A Web developing framework from front to back-end. This will help to build some useful tools for yourself. Now web is
not just a website, it more like a app. You can also use it in your mobile device by responsive design. I recommend [Django](https://www.djangoproject.com/) for python, [Rails](http://rubyonrails.org/) for ruby, [Express](http://expressjs.com/) for node, [Spring-MVC](http://spring.io/) for java. Just use it and improve it. Do not hate it.
- A [continuous integration](https://en.wikipedia.org/wiki/Continuous_integration) system. Most of the time a programmer need to work with others. So the collaboration is really import. To make your software need to make it earlier integrate and earlier test. A CI system will really help you to do that job. [TeamCity](https://www.jetbrains.com/teamcity/) and [Travis CI](https://travis-ci.org/) are really good at it.
- Software developing method. No matter you are using waterfall or agile. You need know how to run them unless you are the single soldier.

To be a pragmatic programmer is a very hard road. You need to practice every day and try many different ways. If you have more advice for it. An email is welcome. Hope you enjoy this article. :)
