---
published: false
categories: technique
tags: 'programming,java,javascript,mode'
---
尝试对编程做点小结

![developer-poster.png]({{site.baseurl}}/images/developer-poster.png)

一直以来，编程技能是我吃饭的家伙，而我却很少在朋友圈或者博客中提及，实在是愧对码农这个称号，原因其实很简单，一则是自己非科班出身，自信心不足。二则编程领域大牛如星辰，而我又算什么呢。 可是进来随着年龄的增长，突然发现自己周围都是些小朋友了，而自己也应该把自己积累的那点有限的或许有用的东西拿出来分享一下。

今天要聊的是编程模式，一直以来我自认为是个后端开发程序员，主要做的都是后台业务逻辑的设计和编码，当然也涉及到数据持久化，以及性能调优之类的。后来一个机缘巧合的机会下，做了一个前端项目，发现前端开发远不是我之前认为的就是些html,CSS加上一些javascript的奇技淫巧了，相反，和后端有了类似的庞大的生态圈，编程语言虽然还是html+javascript。可是模式完全不同，早期的前端js是完全的从属地位，而现在js是用来操纵dom的，html相反变成了配角。更不用说层出不穷的build工具如[npm](https://www.npmjs.com/)，单元测试工具[mocha](https://mochajs.org/)，各种编程框架如[react](https://reactjs.org/)，[angular](https://angular.io/)，更多的信息请参考[awesomeJS](https://github.com/sorrycc/awesome-javascript)。以至于现在[github](https://github.com/)上最流行的语言就是js也不能说是多让人惊讶的事情了（当然在[tiobe](https://www.tiobe.com/tiobe-index/)上面的官方排行榜还不是，至少说明在开源领域js之流行）。为什么会这样？ 我个人认为有以下三点原因：

## 移动开发的趋势

毫无疑问，移动开发是未来的发展趋势，就象之前的web开发的框架取代cgi一样。而移动开发的跨平台（主要就是Android和Apple）最好的办法就是复用浏览器，也就是web开发来取代原生的Android开发(基于Java或者Kotlin)和iOS(基于Object-C或者Swift)，而web开发最直接的就是采用方兴未艾的各种js框架。这其中比较强大的是[IONIC](https://github.com/ionic-team/ionic).

## Functional编程的趋势

自从C/Java统治编程领域近20年以来，最大的变化就是大家开始普遍拥抱functional programming了，从最开始的Lisp（当初受<[Hacker and Painter](http://www.paulgraham.com/hp.html)>的影响学习了点皮毛）到JVM平台上[Clojure](https://clojure.org/)。curring, fuction as first class, native closure等语言特性极大的提高了生产力。而被后端程序员鄙视来很久的js竟然具备N多functional编程的特性，使得它具备继续演化的基础，最近的演化成果就是[Typescript](https://www.typescriptlang.org/).

## 打通前后端编程模式的趋势

这个其实是我想说的重点，先来回顾一下早期Java web 编程的模式，基本上就是采用类似于Struts, Spring MVC, Webwork这种纯后端的框架来进行，也就是说所有的DOM的生成都是在后台发生的，前台浏览器只是把传说过来的html进行渲染而已，可以想象，如果需要某种灵活的UI响应，需要隔着一个DOM层把所有的输入（js模型）转换成后台Java平台上的模型来相应，再把结果传到前台，有点隔靴搔痒，有些特效实现起来极其繁琐甚至不可能。在Java范围内，怎么打通前后端呢？ 一般事先先实现一些UI的控件的浏览器插件，这些控件在java平台都有对应的模型存在，这样你可以使用Java语言来操纵这些直接在前台运行的UI模型，浏览器和服务器之间的沟通仅仅是控制信息的传递，这样前台模型的响应会方便很多，而且中间数据传输量大大减少。比较典型的框架一个是[wicket](https://wicket.apache.org/).一个就是[Vaadin](https://vaadin.com/docs/v10/flow/Overview.html),还有一个就是[GWT](http://www.gwtproject.org/)。

而JS很轻松地做到了这一点，当然前提是某人在某天发明了NodeJS，用js写了后端代码，前端js模型和后端的js模型竟然实现无缝共享，比起Java的方式不知轻便了多少。

## Java前后端打通的开发模式的未来

有一天我看到了一个天才少年[Li Haoyi](http://www.lihaoyi.com/)的这篇[文章](http://www.lihaoyi.com/hands-on-scala-js/)，使我豁然开朗，这应该是JVM平台上最优雅的实现了，后台采用Scala（大量采用Functional编程元素），前台就使用Scala-js(Scala在js平台上的实现)，完全实现了模型的共享，和JS的模型共享是异曲同工。这个小项目是一个小小的尝试，供参考： https://github.com/yuanqingfei/gdbscan-akka-d3js 

## 结语：

编程语言在不断发展，模式也是如此，前后台打通的模式应该是web编程领域的一个大趋势。