# Spring Data Solr

## Lucene
是一个基于java的全文信息搜索工具包，对文本格式数据进行索引和搜索

## Solr
Solr基于Lucene。是一个可扩展，搜索/存储引擎,优化搜索大量以文本为中心的数据。

### 内置参数

* q 查询的关键字，默认为q=*:*，例如q=id:1
* fl 返回的结果包含哪些域，也就是返回哪些字段，可以指定多个，用逗号隔开。例如，fl=id,title,sort
* fq 过滤查询，提供一个可选的筛选器查询，例如：q=id:1&fq=sort:[1 TO 5]，查找id为1，并且sort是1到5之间的
* wt用于指定使用什么类型的格式来格式化查询结果，默认json

### Solr的检索运算符
“:”  指定字段查指定值，如返回所有值*:*

“?”  表示单个任意字符的通配

“*”  表示多个任意字符的通配（不能在检索的项开始使用*或者?符号）

“~”  表示模糊检索，如检索拼写类似于”roam”的项这样写：roam~将找到形如foam和roams的单词；roam~0.8，检索返回相似度在0.8以上的记录。

AND、||  布尔操作符

OR、&&  布尔操作符

NOT、!、-（排除操作符不能单独与项使用构成查询）

“+”  存在操作符，要求符号”+”后的项必须在文档相应的域中存在²

( )  用于构成子查询

[]  包含范围检索，如检索某时间段记录，包含头尾，date:[201507 TO 201510]

{}  不包含范围检索，如检索某时间段记录，不包含头尾date:{201507 TO 201510}

### 高亮
h1  是否高亮，hl=true，表示采用高亮

### 同类型技术 ElasticSearch
同样基于Lucene。是一个分布式、高扩展、高实时的搜索与数据分析引擎。

### Solr与ElasticSearch区别
Solr支持更多格式的数据，比如JSON、XML、CSV，而ElasticSearch仅支持json文件格式。Solr利用zookeeper进行管理，而ElasticSearch自带分布式协调管理功能，是分布式首选。
单纯对已有数据进行搜索时，solr更快，当建立实时索引时，Solr会产生io阻塞。随着数据量的增加，solr的搜索效率也会变得更低。

### core
core是solr的特有概念，每个core是一个查询数据、索引的集合体，可以把他想象成一个独立的数据库

### IK Analyzer 中文分析器
IK Analyzer是一个开源的，基于java语言开发的轻量级的中文分词工具包。

## Spring Data Solr
将solr的应用集成到spring中，通过solrTemplate使用

### 关键的几个类
SolrTemplate、Query、Criteria

Criteria 用于对条件的封装
query 把Criteria通过构造方法传入，可以设置开始索引、每页记录数

## solr的配置
1. 提前配置好Linux下的java环境
2. 下载solr的安装包，解压到相应目录
3. 进入解压文件的bin目录下启动solr
4. solr默认服务端口是8983，此时访问ip地址下的8983端口，就可以访问solr的控制面板
5. 创建core,名称为collection1
6. 配置中文分词器
7. 配置collection1目录下的conf目录下的schema.xml
8. 配置域、复制域、以及动态域等