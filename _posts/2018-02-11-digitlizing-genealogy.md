---
published: true
categories: technique
tags: genealogy react svg pathjs
---
尝试数字化家谱。

自己由于做ＩＴ方面的工作，一直想把家谱数字化来着，这个周末花了两天，弄了个雏形，放在网上了，大家多提意见把。没有耐心的可以直接上了：　[http://yuanqingfei.me/familyTree/](http://yuanqingfei.me/familyTree/)

# 基本想法
家谱从算法的观点看其实就是一颗典型的树，所以打算从两方面入手，一个是树形图显示，这个主要方便查看，没啥好说的。另外一个就是家谱的数字化查询，基本的几个场景有：

* 任意两个人的最近一个共同祖先；
* 找出一个人到始祖的最短路线；
* 任意两个人是否在“五服”之内；

还可以做些有趣的查询：

* 家谱中那个人的儿子最多;
* 家谱中那个人的孙子最多;
* 家谱中那个除了始祖之外，那个人的后代最多;
* 给定任一代，找出后代最多的那个人；
* 家谱中没有生出男孩的有那些（也就是家谱中表示为“至”的）;
* 家谱中没有长大就死亡的（也就是家谱中表示为“夭”的）；
* 家谱中过继儿子的有多少;
* 家谱中人口增长曲线

如果在对每一个点创建一个基本的数据单元，还可以做相关的查询，比如：

* 家谱中那个人的老婆最多;
* 家谱中那个人的官最大，学位最高；
* 家谱中那个人最开始迁移；
* 家谱中那个人迁移的最远；

# 基本步骤

上面想法虽然很多，现在只能做第一步，就是做个简单的树形图展示，其他慢慢来把。这两天算是个开始。

* 由于现在[react](https://github.com/facebook/react)已经非常成熟，故采用react 16.0版本.
* 数据目前使用Json格式
* 由于家谱图往往很多人，所以要可以缩放，而且还不能影响图像质量，所以采用了[svg path](https://www.w3.org/TR/SVG/paths.html)，具体的参考框架就是两个：　[path-js](https://github.com/andreaferretti/paths-js)　和　[svg-pan-zoom](https://github.com/chrvadala/react-svg-pan-zoom).
* 创建项目使用 [create-react-app](https://github.com/facebook/create-react-app)
* 发布项目使用 gitpages，具体步骤请参考[这里](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#github-pages)。


步骤不是很复杂，下面做个简单的展示：
![jiapupage1.png]({{site.baseurl}}/images/jiapupage1.png)

如果需要看某个细部，可以使用右上角的手型符号来移动，同时滚动鼠标中键进行缩放。如下图
![jiapupage2.png]({{site.baseurl}}/images/jiapupage2.png)

好了，话不多说，有兴趣可以自己去尝试下，[http://yuanqingfei.me/familyTree/](http://yuanqingfei.me/familyTree/)

现在还比较粗糙，肯定有不完善支出，有意见可以在这个文章下面留言。谢谢。

# 下一步

* 要基于[d3-hierarchy](https://github.com/d3/d3-hierarchy)做些尝试，把基本的树算法都用上。
* 写个小工具来生成数据json文件。因为这个数据录入的力气活真不是人干的，我这次眼都花了。。。
* 基于[scala-js](https://github.com/scala-js/scala-js)来完成前后台统一开发。
