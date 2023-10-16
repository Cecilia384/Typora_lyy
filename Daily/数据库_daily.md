### 9.11

SQL Vs MySQL

SQL是一种语言，而MySQL是基于这种语言的软件之一。实际上，MySQL、SQL Server、Oracle和PostgreSQL都是基于SQL语言的软件。由于它们来自不同的厂商，所以它们的部分语法会有一定的差别，不过大部分语法都是相同的(https://zhuanlan.zhihu.com/p/609117553

MySQL是一个开源的关系型数据库管理系统，它支持多用户、多线程和多表等特性。MySQL可以运行在各种操作系统上，包括Windows、Linux和Mac OS X等](https://blog.csdn.net/weixin_31354669/article/details/113130118)

SQL是一种标准化的语言，用于管理关系型数据库。它可以用来执行各种任务，例如查询数据、插入数据、更新数据和删除数据等](https://zhuanlan.zhihu.com/p/130768469)

因此，可以说MySQL是SQL的一种实现方式。它使用SQL语言来进行操作，并提供了许多其他功能和特性，例如事务处理、存储过程和触发器等](https://blog.csdn.net/weixin_31354669/article/details/113130118



### 10.11

[db-tutorial](https://github.com/dunwu/db-tutorial)



[youtube1_4h_SQL](https://www.youtube.com/watch?v=HXV3zeQKqGY)



- [x] [Learn SQL In 60 Minutes](https://www.youtube.com/watch?v=p3qvj9hO_Bo)



#### CMU_01-RelationalModel

- **DATA MODELS** 

  - Relational 

  - Key/Value 

  - Graph

  -  ==Document / XML / Object== (Leading Alternative)

  - Wide-Column / Column-family 

  - Array / Matrix / ==Vectors==( Current Hotness)

  -  Hierarchical 

  - Network 

  - Multi-Value

- **DOCUMENT DATA MODEL**

  > 文档数据模型 : 包含已命名字段/值对层次结构的记录文档集合。
  >  →字段的值可以是标量类型、值数组或其他文档。
  > →现代实现使用 JSON。旧系统使用 XML 或自定义对象表示法。通过将对象与数据库紧密耦合，避免 "关系对象阻抗失配"。

![img](%E6%95%B0%E6%8D%AE%E5%BA%93_daily.assets/%60F$F%5BFZ3UCLJM9OP@%25ZBQX1.png)

![img](%E6%95%B0%E6%8D%AE%E5%BA%93_daily.assets/P%7BEBTJ66R78R%60KL7LZJ3P8V.png)





**VECTOR DATA MODEL**

> 矢量数据模型
>  用于最近邻搜索（精确或近似）的一维数组。
> →用于对由 ML 训练的转换器模型（如 ChatGPT）生成的嵌入进行语义搜索。
> →与现代 ML 工具和 API（如 LangChain、OpenAI）的原生集成。这些系统的核心是使用专门的索引来快速执行 NN 搜索。

![img](%E6%95%B0%E6%8D%AE%E5%BA%93_daily.assets/8%5DU%60%5B58@G1BSFB6DIH%5B%5B4FJ.png)

 

![img](file:///C:\Users\08042x'l\AppData\Roaming\Tencent\Users\2260215531\QQ\WinTemp\RichOle\7WS~IC9N[]1H$55ZCFBTV$V.png)

