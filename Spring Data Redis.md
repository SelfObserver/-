# Spring Data Redis
## Redis
redis是一款开源的键值对数据库，企业开发通常采用Redis实现缓存
## Jedis
Jedis是Redis官方推出的一款面向java的客户端，提供了很多接口供java语言使用
## Spring data redis
Spring data redis，提供了在spring应用中通过简单的配置访问redis服务，RedisTemplate提供了redis各种操作、异常处理及序列化，支持发布订阅。

## 针对jedis提供了如下功能
1. 连接池自动管理，高度封装的RedisTemplate类
2. 针对jedis客户端中大量的api进行了归类封装，将同一类型操作封装为operation接口
   
   ValueOperations 简单的键值对

   SetOperations  无序集合

   ZSetOperations 有序集合

   HashOperations map类型
   
   ListOperations 列表

3. 提供了对key的bound（绑定）便捷化操作API，进行一系列操作不用再次指定Key，即BoundKeyOperations
   
   BoundValueOperations
   
   BoundSetOperations
   
   BoundListOperations
   
   BoundSetOperations
   
   BoundHashOperations