基于python的中文分词项目。

第一个版本实现了基于的[MMSEG中文分词算法](http://technology.chtsai.org/mmseg/)Python实现。MMSEG实际上是一个正向最大匹配+多个规则的分词算法。链接给出的几个网站写的很清楚了。在开发过程中我增加了一个规则来处理原来的算法中有可能出现的冲突问题。当所有的规则都无法唯一的确定一个chunk时，优先选择后面比较长的词。开发过程中参照了[MMSEG的Java实现](http://www.solol.org/projects/mmseg/)和[ruby实现](http://rmmseg.rubyforge.org/)。并且对性能进行了初步的优化。

目前的性能数据：在Pentium D 2.8G的CPU下处理2.9MB的文本数据，全切分的复杂算法不开启pysco的情况下104s，开启pysco的情况下90s，能达到32KB/s。简单算法可以达到64KB/s。经测试速度能达到Java版本MMSEG的1/3，未来如果要进一步优化速度的话应该是把关键的算法的实现移植到c语言中。

实现了简单的余弦相似度计算的算法。

TODO:

  * 实现[NLTK](http://nltk.sourceforge.net/index.php)兼容的接口。(目前已经增加了tokenizer接口)
  * C语言级别的优化 （测试中，增加了is\_basic\_latin的c实现，考虑字典用c语言优化）
  * 实现其他算法，目前考虑一个[ICTCLAS](https://groups.google.com/group/ictclas)的python实现，要看有没有时间。
  * 支持停用词，支持unicode的字母数字检测等。

与分词有关的其他想法
  * 研究一下ferret/cferret，能否实现一个python binding并且结合进去。（研究发现ferret的实现非常复杂，ruby绑定的接口部分的c代码都有上万行，放弃了，还是用[solr](http://lucene.apache.org/solr/)吧）
  * 与nlp/datamining的进一步结合