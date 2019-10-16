# Spark-Python
## 一 Spark 概述
Spark是一个通用的分布式数据处理框架  
提供了用于大规模操作数据、内存数据缓存和跨计算重用的函数API  
它在分区数据上应用组粗粒度转换，并在失败时依赖于大数据的沿袭来重新计算任务  
Spark支持大多数数据格式，与各种存储系统集成，可以在Mesos或YARN上执行  

##一.1案例
两个函数，一个备份，一个恢复。  
![image](https://github.com/402test/Spark-Python/blob/master/img/1571210326.jpg)  
  
对不同数据存储中的数据进行差异分析  
![image](https://github.com/402test/Spark-Python/blob/master/img/1571210429(1).jpg) 

## 二 结构
![image](https://github.com/402test/Spark-Python/blob/master/img/1571210466(1).jpg)  
用户通过 SparkContext ，进行连接和操作，交互。创建RDDs并执行一系列转换以实现最终结果。然后将这些RDDs的转换转换为DAG并提交给调度程序，以便在一组工作节点上执行。  

## 三 RDD
可以将RDD视为具有故障恢复可能性的不可变并行数据结构  
它为数据的各种转换和物化以及控制元素的缓存和分区以优化数据布局提供了API  
可以从外部存储创建RDD，也可以从另一个RDD创建RDD，并存储关于其父RDD的信息，以优化执行(通过操作管道)，并在出现故障时重新计算分区。  
从开发人员的角度来看，RDD表示分布式不可变数据(分区数据+迭代器)和延迟计算操作(转换)  
RDD有如下五大特性  
1有一个分片列表，就是能被切分，和Hadoop一样，能够切分的数据才能并行计算  
2由一个函数计算每一个分片，这里指的是下面会提到的compute函数  
3对其他RDD的依赖列表，依赖还具体分为宽依赖和窄依赖，但并不是所有的RDD都有依赖  
4可选：key-value型的RDD是根据哈希来分区的，类似于mapreduce当中的paritioner接口，控制Key分到哪个reduce。  
5可选：每一分片的优先计算位置，比如HDFS的block的所在位置应该是优先计算的位置。
https://blog.csdn.net/zhousenshan/article/details/79513895  
