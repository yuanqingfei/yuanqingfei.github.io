---
published: true
categories: technique
tags: genealogy python php graphviz
---
自己瞎捣鼓了半天，现在把前人的工作大体看看。

基本上，自从上个世纪8,90年代开始就有人开始开发家谱软件，只不过当时都是单机版，到网络时代兴起，2000年以后开始有网络版的，大部分都是PHP和MYSQL。自从2010年后，随着新的前端技术发展，现在更多趋势是用js框架把上个世纪单机版的富客户端搬到网络上。

## 格式

> "GEDCOM is not perfect, and not perfectly supported either, but it is the only widely supported standard."

主流的家谱软件都是支持统一的数据格式[GEDCOM](https://en.wikipedia.org/wiki/GEDCOM),虽然它诞生于1984年，但是它已经是家谱软件的事实标准，最新版是发布于1996年的5.5版(已经20多年没有更新了)，大部分现在的家谱软件都是支持发布于1999年的[5.5.1草案](http://wiki-en.genealogy.net/Gedcom_5.5.1)。因为草案里引入对Unicode的支持,也就是多语言的支持。这篇文章对其做了非常好的[介绍](https://www.tamurajones.net/AGentleIntroductionToGEDCOM.xhtml)。

这个数据格式是同时支持父系和母系的，女儿和儿子一样也是都列入家谱的。下面例子中可以看出这一点。这个家谱数据是按照西方的家庭观点来看待的。

```
0 HEAD
1 SOUR PAF
2 NAME Personal Ancestral File
2 VERS 5.0
1 DATE 30 NOV 2000
1 GEDC
2 VERS 5.5
2 FORM LINEAGE-LINKED
1 CHAR ANSEL
1 SUBM @U1@
0 @I1@ INDI
1 NAME John /Smith/
1 SEX M
1 FAMS @F1@
0 @I2@ INDI
1 NAME Elizabeth /Stansfield/
1 SEX F
1 FAMS @F1@
0 @I3@ INDI
1 NAME James /Smith/
1 SEX M
1 FAMC @F1@
0 @F1@ FAM
1 HUSB @I1@
1 WIFE @I2@
1 MARR
1 CHIL @I3@
0 @U1@ SUBM
1 NAME Submitter
0 TRLR
```

## 几个开源家谱软件

### Gramps

[Gramps](https://github.com/gramps-project/gramps)是一个用Python写的单机版家谱软件，有很多很成熟的[特性](https://www.gramps-project.org/wiki/index.php?title=Features)。

![gramp_chart.png]({{site.baseurl}}/images/gramp_chart.png)

其他具体的请参考[它的手册](https://www.gramps-project.org/wiki/index.php?title=User_manual)。

### Webtrees

[Webtrees](https://github.com/fisharebest/webtrees)是一个使用PHP写的网络版家谱软件，也已经比较成熟。

![webtrees.png]({{site.baseurl}}/images/webtrees.png)

### Geneotree

[Geneotree](http://www.geneotree.com/)也是一个PHP写的网络版家谱软件，还在演化中。

![geneoTree.png]({{site.baseurl}}/images/geneoTree.png)

-----

其他更多开源或者收费家谱软件，请看[这里](https://en.wikipedia.org/wiki/Genealogy_software)


## GEDDOM 软件列表

github上面的开源列表在这里[Gedcom](https://github.com/todrobbins/awesome-gedcom)

### Gedcom

[https://github.com/FamilySearch/Gedcom](https://github.com/FamilySearch/Gedcom)

### gedcom4j

[https://github.com/frizbog/gedcom4j](https://github.com/frizbog/gedcom4j)



## 一点想法

* 遵循[GEDCOM](https://en.wikipedia.org/wiki/GEDCOM)，很重要的一点就是要把女的也要放上去。毕竟从科学的观点来看，父系传承的是Ｙ染色体，而母系传承的是线粒体，都是有继承根据的。从遗传学上来说，儿子的智商被母亲影响得更大呢。初步系想法是，妻子加入进来，但是只有一层。女儿也加入进来，但是只有配偶信息。毕竟如果男方家谱也遵循同样规则，不会造成大量信息重复。

![ideaTree.jpg]({{site.baseurl}}/images/ideaTree.jpg)

* Gramps是个已经很成熟的平台，只是它现在是个单机版。但是它所依赖的[Graphviz](http://www.graphviz.org/)技术已经被[js化](https://github.com/mdaines/viz.js)了，这为把它搬上网络打下了基础。已经有两个d3项目是基于它，一个是[graph-viz-d3-js](https://github.com/mstefaniuk/graph-viz-d3-js),另一个是[d3-graphviz](https://github.com/magjac/d3-graphviz). 以后打算尝试使用DOT语言来画svg图。DOT语言的好处就是可以用程序的方式把树形结构完全用DOT语言自动生成，这样就可以达到和d3-herarchy的stratify同样的效果了。

* 初步实验表明[d3-graphviz](https://github.com/magjac/d3-graphviz)仍然是模仿Graphviz的两层结构，结果在React编程时，viz作为web worker不能导入，暂时不能用React统一编程模型。但是可以作为普通js编程使用。

* [dagre](https://github.com/dagrejs/dagre)配合[dagre-d3](https://github.com/dagrejs/dagre-d3)也可以作为一个尝试，它也是纯client的layout框架，也支持DOT语言。
