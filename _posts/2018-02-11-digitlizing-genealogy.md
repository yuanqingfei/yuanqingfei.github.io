---
published: true
categories: technique
tags: genealogy react svg pathjs
---
尝试数字化家谱。

自己由于做IT方面的工作，一直想把家谱数字化来着，这个周末花了两天，弄了个雏形，放在网上了，大家多提意见把。没有耐心的可以直接上了：　[http://yuanqingfei.me/familyTree/](http://yuanqingfei.me/familyTree/)

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
![jiapupage2.png]({{site.baseurl}}/images/jiapupage2.png)

好了，话不多说，有兴趣可以自己去尝试下，[http://yuanqingfei.me/familyTree/](http://yuanqingfei.me/familyTree/)

现在还比较粗糙，肯定有不完善支出，有意见可以在这个文章下面留言。谢谢。

# 下一步

* ~~要基于[d3-hierarchy](https://github.com/d3/d3-hierarchy)做些尝试，把基本的树算法都用上。~~
* ~~写个小工具来生成数据json文件。因为这个数据录入的力气活真不是人干的，我这次眼都花了。。。~~
* 基于[scala-js](https://github.com/scala-js/scala-js)来完成前后台统一开发。

# 20180220更新

* 使用d3-hierarchy中的工具[stratify](https://github.com/d3/d3-hierarchy#stratify)来解析dsv,从而自动生成树。也就是把如下的csv数据自动构造成能满足树形图需要的json.

```csv
id|name|parent|description
00001|清||全,仲七
00002|仲|00001|
00003|玘|00002|
00004|洪|00003|配辛,吴氏
00005|河|00003|
```

```javascript
    dsv("|", yuanCsv, function (d) {
      return {
        id: d.id,
        name: d.name,
        parent: d.parent,
        description: d.description
      };
    }).then(function (data) {
      var myRoot = stratify()
        .id(function (d) { return d.id; })
        .parentId(function (d) { return d.parent; })(data);

    });
```
* 用d3-hierarchy来生成树（[tidy tree](https://github.com/d3/d3-hierarchy/blob/master/src/tree.js)）,通过对比可以看出他们的区别. pathJs算法更有效利用空间，但是d3Hierarchy是更清楚些。相同点是每一代都在同一竖线上，很好分辨，下一步打算在此基础上加上班辈和世代。
![pathjs.png]({{site.baseurl}}/images/pathjs.png)
![tidyTree.png]({{site.baseurl}}/images/tidyTree.png)

# 20180303更新

* 使用[d3-graphviz](https://github.com/magjac/d3-graphviz)来渲染这棵家族树，算法果然又不一样，可以参考下面的结果。
![dotFmailiyTree.png]({{site.baseurl}}/images/dotFmailiyTree.png)

* 在把女性计入家谱的情况下，由于会出现表亲结婚的情况下，所以就会变成DAG(有向无环图)，可参考[下面描述](https://en.wikipedia.org/wiki/Directed_acyclic_graph#Genealogy_and_version_history):

>> Family trees may be seen as directed acyclic graphs, with a vertex for each family member and an edge for each parent-child relationship.[44] Despite the name, these graphs are not necessarily trees because of the possibility of marriages between relatives (so a child has a common ancestor on both the mother's and father's side) causing pedigree collapse.[45] The graphs of matrilineal descent ("mother" relationships between women) and patrilineal descent ("father" relationships between men) are trees within this graph. Because no one can become their own ancestor, family trees are acyclic.

* dot语言描述DAG可以参考[这里](https://stackoverflow.com/questions/2271704/family-tree-layout-with-dot-graphviz)

* 具体的画图形式需要遵循家族图的[格式](https://en.wikipedia.org/wiki/Genogram)。

* 还是要借鉴[Gramps](https://en.wikipedia.org/wiki/Gramps)。
