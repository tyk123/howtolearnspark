# howtolearnspark
https://www.zhihu.com/question/26707124/answer/77249718
https://www.zhihu.com/question/39078198

 陈晓宇 算法工程师
35 人赞同
刚学习了一段时间Scala，给出我自己的学习线路：
首先我看了《Scala编程(中文版)》的前九章，作为初学者还是可以看懂的，看到第十章的时候就云里雾里了，后面的没有看。
对于 Inside 同学回答中的 Scala Tour，当我看到借贷模式就完全看不懂了，所以完全没有看这个。

这时你就可以开始看 Scala 课堂了，这个课堂的内容还是比较全的，但是对于每个知识点都讲的很少，不够全面，当你看不懂的时候就借助Google多搜索多看别人的帖子，你会发现很多写的很好的文章。

看完这些之后相信你已经有一些基础了，现在看看官方的 A Tour of Scala 巩固一下吧，上面按照每个知识点进行了讲解。

如果你喜欢看视频，这两个中文的视频还不错，有些东西我是看这个视频看懂的：Scala深入浅出实战初级入门经典视频课程（共41课时），Scala深入浅出实战中级进阶经典视频课程（共152课时）。你可以找自己需要看的内容看，因为内容比较多。

这个时候你就需要看看这个博客了：scala | 写点什么。我目前看了类型相关的部分，上面的内容写的非常好。

补充一个最近看到的一个Tutorial：Scala Tutorial.

最后，在学习的过程中，Scala for the Impatient 和官方的 Scala By Example 是你很好的参考，有时候你还要查阅 Scala 的 api：Scala Standard Library 2.10.4 以及 Scala 2.10.4 源码。并且后期的时候看看 Spark源码 会有很大的帮助。



 陈晓宇 算法工程师，业余创业者
61 人赞同
公司实习中，工作中写Spark代码，给点我自己的心得。只学了一个月左右，也只能算刚入门吧。

关于Hadoop，只了解配置相关，除了写过从hdfs读文件的代码，没有写过其他代码。

关于Spark，讲一下我从入门开始的学习过程：
我用了两个星期时间学习了Scala，先参考一下这个问题：如何学好Scala？请给出一条科学的时间线 - 陈晓宇的回答。

学完了Scala之后再学习一下Spark的RDD，据说这篇论文一定要看https://www.usenix.org/system/files/conference/nsdi12/nsdi12-final138.pdf。然后在网上多看看别人在Spark踩过的坑和Spark的使用经验，自己不要再跳就行。剩下的就是多写Spark代码了，在写代码的时候要多思考，有问题直接去 Stack Overflow 上问，提问之前先问一下自己这个问题我是不是真的找不到解决方法，我的这个问题是不是一个有价值的问题。

另外，写比较复杂的程序的时候，Spark的源码是要看的，你要看某个类提供了哪些方法可以调用，调用这个方法返回的是什么样的返回值等等。

在写代码的过程中会遇到很多坑，只有你自己慢慢去发现，慢慢积累了，所以没有什么捷径，实践是硬道理。比如说关于序列化，哪些变量需要用@transient声明不可序列化；zipWithUniqueId并不是从0开始连续计数；MLlib中RowMatrix并没有行号的概念，不关心矩阵中行的顺序，如果行号对你很重要你必须使用IndexedRowMatrix（具体参考这个问题 scala - Converting CoordinateMatrix to RowMatrix doesn't preserve row order）；打印CoordinateMatrix可以先toBlockMatrix然后再toLocalMatrix（一般情况下不把distributed的矩阵转为local矩阵，我是调试过程中输出矩阵的值才用到，具体参考这个问题 scala - Converting CoordinateMatrix to Array?）；还有一个连接MySQL中"No suitable driver found for jdbc"的问题（参考 mysql - No suitable driver found for jdbc in Spark）等等这些坑我都踩过。

遇到过的另一个问题：RDD transformations and actions can only be invoked by the driver, not inside of other transformations; for example, rdd1.map(x => rdd2.values.count() * x) is invalid because the values transformation and count action cannot be performed inside of the rdd1.map transformation. 简单的说，就是RDD的操作里面不允许再出现RDD的操作。An error about Dataset.filter in Spark SQL 这个问题也是因为该原因引起的。

关于你提的如何实践？那就自己找找可以用Spark写的小项目，MLlib中有很多example你可以看一下，MLlib - Spark 1.6.0 Documentation 里的很多算法可以让你练习很久了，如果没有大的数据量就自己构造数据，先写小实验开始入门。
