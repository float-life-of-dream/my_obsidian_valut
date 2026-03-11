[TOC]

 # redis

## 基础篇

### 初识redis

#### 认识NoSQL

|          | SQL                  | NoSQL    |
| -------- | -------------------- | -------- |
| 数据结构 | 结构化（Structured） | 非结构化 |
| 数据关联 | 关联的（Relational） | 无关联的 |
| 查询方式 | SQL查询              | 非SQL    |
| 事务特性 | ACID                 | BASE     |
| 存储方式 | 磁盘                 | 内存     |
| 拓展性   | 垂直                 | 水平     |

#### 认识Redis

Redis诞生于2009年全称是Remote Dictionary Server， 远程词典服务器，是一个基于内存键值型NoSQL数据库

**特征：**

- 键值（key-value）型：value支持多种不同数据结构
- 单线程，每个命令具有原子性
- 低延迟，速度快（基于内存、IO多路复用、良好的编码）
- 支持数据持久化
- 支持主从集群、分片集群
- 支持多语言客户端

#### 安装Redis

**docker部署**

``` shell
# 下载镜像
docker pull redis

# 检查当前所有Docker下载的镜像
docker images

## 创建目录
mkdir -p /opt/redis/conf
mkdir -p /opt/redis/data

## 创建文件
touch /opt/redis/conf/redis.conf

# Docker 创建 Redis 容器命令
docker run \
--restart=always \
--log-opt max-size=100m \
--log-opt max-file=2 \
-p 6379:6379 \
--name redis \
-v /opt/redis/conf/redis.conf:/etc/redis/redis.conf  \
-v /opt/redis/data:/data \
-d redis redis-server /etc/redis/redis.conf \
--appendonly yes \
--requirepass 123456 

# 修改 /opt/redis/conf/redis.conf
protected-mode no
bind 0.0.0.0

# 重启redis服务
docker restart redis
```

1. 获取Redis镜像

2. 下载Redis镜像

3. 创建redis配置文件

   1. 启动前需要先创建Redis外部挂载的配置文件 （ /home/redis/conf/redis.conf ）
   2. 之所以要先创建 , 是因为Redis本身容器只存在 /etc/redis 目录 , 本身就不创建 redis.conf 文件
   3. 当服务器和容器都不存在 redis.conf 文件时, 执行启动命令的时候 docker 会将 redis.conf 作为目录创建 , 这并不是我们想要的结果 。

4. 创建Redis容器并启动
  | 命令                                                         | 功能                                                         |
   | ------------------------------------------------------------ | ------------------------------------------------------------ |
   | docker run                                                   | 这是 Docker 用来创建并运行一个新的容器的命令                 |
   | --restart=always                                             | 如果容器退出，这个选项会使得它自动重启                       |
   | --log-opt max-size=100m                                      | 这是对容器日志的设置，最大大小为 100MB                       |
   | --log-opt max-file=2                                         | 这是对容器日志文件的设置，最多可以有2个日志文件              |
   | -p 6379:6379                                                 | 这是端口映射的设置，将宿主机的6379端口映射到容器的6379端口   |
   | --name redis                                                 | 这是给新创建的容器命名的选项，名字是 "redis"                 |
   | -v /opt/myredis/redis.conf:/etc/redis/redis.conf             | 这是对容器内的文件系统的挂载设置，将宿主机上的 /opt/myredis/redis.conf 文件挂载到容器内的 /etc/redis/redis.conf 位置 |
   | -v /opt/myredis/data:/data                                   | 这是另一个文件系统的挂载选项，将宿主机上的 /opt/myredis/data 目录挂载到容器内的 /data目录 |
   | -d                                                           | 这是 Docker 的分离模式，新创建的进程将会在后台运行           |
   | redis redis-server /etc/redis/redis.conf --appendonly yes --requirepass 123456 | 这是容器内要运行的命令，启动 Redis 服务，使用 /etc/redis/redis.conf 配置文件，设置追加写入(appendonly)为 yes，设置密码为 "123456" |
5. Redis配置文件修改

 | 命令              | 功能                                                         |
   | ----------------- | ------------------------------------------------------------ |
   | protected-mode no | 关闭protected-mode模式，此时外部网络可以直接访问 (docker貌似自动开启了) |
   | bind 0.0.0.0      | 设置所有IP都可以访问 (docker貌似自动开启了)                  |

6. RDM 远程连接

#### Redis命令客户端

Redis安装完成后自带命令行客户端：Redis-cli

~~~sh
redis-cli [option] [commonds]
~~~

其中常见的options有：

- -h 127.0.0.1：指定要连接的Redis节点的IP地址，默认是127.0.0.1
- -p 6379       ：指定要连接Redis节点的端口，默认是6379
- -a 123321   ：指定Redis的访问密码

其中commands就是Redis的操作命令，例如:

- ping            ：与Redis服务端做心跳测试

不指定commond时，会进入redis-cli交互控制台

#### Redis图形化客户端

Redis Desktop Manager又名RDM，它是一款用于Windows，Linux和MacOS的快速开源Redis数据库管理应用程序，能够为用户提供一系列功能选择以及操作设定，以便于用户直接对需要管理的Redis数据库进行建设性操作，以树形的方式来罗列出密匙以及CRUD密钥，可节约用户的很多宝贵时间，此工具支持识别shell命令，管理员能够根据自己的需要添加shell，以此让程序系统执行对应的命令操作；

### Redis常见命令

#### Redis数据结构介绍

Redis是一个key-value的数据库，key一般是string类型，不过value的类型多种多样

| 类型 | 例如 |
| ---- | ---- |
|String     |hello world      |
|Hash|{name:"Jack",age:21}|
|List|{A  -> B -> C -> C}|
|Set|{A,B,C}|
|SortedSet|{A:1,B:2,C:3}|
|GEO|{A:(120.3, 30.5)}|
|BitMap|0110110101110101011|
|HyperLog|0110110101110101011|

 在官网（https://redis.io/commands）可以查看到不同命令的帮助文档

或者在命令行中输入

```bash
help @组别
```

#### Redis通用命令

通用指令是部分数据类型，都可以使用的指令，常见的有：

- KEYS : 查看符合模板的所有key,不建议在生产环境设备上使用
- DEL： 删除指定的Key
- EXITS：判断一个KEY是否存在
- EXPIRE：给一个key设置有效期有效期到期时key会被自动删除
- TTL：查看一个key的剩余有效期

#### String类型

String类型，也就是字符串类型，时Redis最简单的存储类型。

其value是字符串，不过根据字符串的格式不同，又可以分为3类

- string：普通字符串
- int：整数类型，可以做自增、自减操作
- float：浮点类型，可以做自增、自减操作  

不管以哪种形式，底层都是以字节数组i形式存储，只不过编码方式不同，字符串类型的最大空间不能超过512m

String的常见命令有：

- SET：添加或者修改已经存在的一个String类型键值对
- GET：根据key获取String类型的键值对
- MSET：批量添加多个String类型的value
- MGET：根据多个key获取多个String类型的value
- INCR：让一个整型的key自增1
- INCRBY：让一个整形key自增并指定步长，例如：incrby num 2让num值自增2
- INCRBYFLOAT：让一个浮点类型的数字自增并指定步长
- SETNX：添加一个String类型的键值对，前提是这个key不存在，否则不执行
- SETEX：添加一个String类型的键值对，并且指定有效期

key的机构

Redis的key允许有多个单词形成层级结构，多个单词用":"隔开，格式如下：

``` 
项目名：业务名：类型：id
```

#### Hash类型

Hash类型，也叫散列，其value是一个无序字典，类似于java的HashMap结构

Hash结构可以将每个字段独立存储，可以针对单个字段做CRUD

Hash类型常见命令有：

- HSET key field value ：修改或者修改hash类型key的field的类型值
- HGET key filed：获取一个hash类型key的field的值
- HMSET：批量添加多个hash类型key的field的值
- HMGET：批量获得多个hash类型key的field的值
- HGETALL：获取一个hash类型的key所有的field和value
- HKEYS：获取一个hash类型的key中所有的field
- HVALS：获取一个hash类型的key中所有的value
- HINCRBY：让一个hash类型key字段值自增并指定步长
- HSETNX：添加一个hash类型可以的filed的值，前提是这个field不存在，否则不执行

#### List类型

Redis中的List类型与java中的LinkedList类似，可以看作一个双向链表的结构。既可以支持正向检索也可以支持反向检索。

特征业余LinkedList类似：

- 有序
- 元素可以重复
- 插入和删除快
- 查询速度一般

常用来存储一个有序数据

List类型常见命令：

- LPUSH key element……：向列表左侧插入一个或多个元素
- LPOP key：移除并返回列表左侧的第一个元素，没有则返回nil
- RPUSH key element……：向列表右侧插入一个或多个元素
- RPOP key：移除并返回列表右侧的第一个元素，没有则返回nil
- LRANGE key star end：返回一段角标范围内的所有元素
- BLPOP和BRPOP：与LPOP和RPOP类似，只不过在没有元素时等待；指定时间而不是直接返回nil

模拟栈

- 入口与出口在同一侧

模拟队列

- 入口和出口在不同边

模拟阻塞队列

- 入口和出口在不同边
- 出队时采用BLOPOP或BRPOP

#### Set类型

Redis的set结构与java中的HashSet类似，可以看作一个value为null的HashMap。因此也是一个Hash表，因此具备与HashSet类似的特征

- 无序
- 元素不可重复
- 查找快
- 支持交集、并集、差集等功能

Set类型常见命令有：

- SADD key member ……：向set添加一个或多个元素
- SREM key member ……：移除set中指定元素
- SCARD key：返回set中元素个数
- SISMEMBER key member：判断一个元素是否在set中
- SMMEMBERS：获取set中的所有元素‘
- SINTER key1 key2……：求key1与key2的交集
- SDIFF key1 key2……：求key1与key2的差集
- SUNION key1 key2……：求key1和key2的并集

#### SortedSet类型

Redis的SortedSet是一个可排序的set集合，与java中TreeSet有些类似，但底层数据结构却差别很大。SortedSet中每一个元素都带有一个score属性，可以基于score属性对元素排序，底层实现是一个跳表（SkipList）加hash表

SortedSet具备下列特性：

- 可排序
- 元素不可重复
- 查询速度快

因为Sortedset的可排序特性经常用来实现排行榜这样的功能

Sortedset的常见命令有：

- ZADD key score member：添加一个或多个元素到sorted set，如果已存在则更新score值
- ZREM key member：删除Sortedset中的一个指定元素
- ZSCORE key member ：获取Sortedset中的指定元素的score值
- ZRANK key member：获取Sortedset中指定元素的排名
- ZCARD key：获取Sortedset中的元素个数
- ZCOUNT key min max：统计score的值在给定范围的所有元素的个数
- ZINCRBY key increment member：让Sortedset中指定元素自增，步长为指定大的increment值
- ZRANGE key minmax：按照score排序后，获取指定score范围内的元素
- ZDIFF、ZINTER、ZUNION：求差集、交集、并集

注意：所有的排名默认都是升序，如果要降序则在命令Z后添加REV即可

### Redis的Java客户端

#### 客户端对比

- Jedis

  - 以Redis命令作为方法名称，学习成本低，简单实用
  - 但是Jedis实例是线程不安全的，多线程环境下需要基于连接池来使用
- lettuce

  - lettuce是基于Netty实现的，基于同步、异步、和响应式编程方式，并且是线程安全的。

  - 支持Redis和哨兵模式、集群模式和管道模式
- Redission
  - Redisson是一个基于Redis实现的分布式、可伸缩的Java数据集合。包含了诸如Map、Queue、Lock、Semaphore、AtomicLong等强大功能
- Spring Data Redis
  - 集成了Jedis和lettuce


#### Jedis

Jedis的官网网址：https://github.com/redis/jedis，快速入门

1. 引入依赖

   ~~~java
   <dependcy>
       <groupId>redis.clidents</groupId>
       <artifactId>jedis</artifactId>
       <version>3.7.0</version>
   </dependcy>
   ~~~

2. 建立连接

```java
private Jedis jedis:

@BeforeEach
void setUp(){
	//建立连接
    jedis= new Jedis("服务器ip",6379);
    //设置密码
   	jedis.authentic("密码");
    //选择库
    jedis.select(0);
}
```

3. 测试string

   ~~~java
   @Test
   void testString(){
       //插入数据，方法名称就是redis命令名称
       String result = jedis.set("name","张三");
       System.out.println("result="+result);
       //获取数据
       String name = jedis.get("name");
       System.out.println("name="+name);
           
   }
   ~~~

4. 释放资源

   ~~~java
   @AfterEach
   void tearDown(){
       //释放资源
       if(jedis != null){
           jedis.close();
       }
   }
   ~~~

#### Jedis连接池

jedis本身是线程不安全的，并且频繁的的创建和销毁连接会有性能损耗，因此我们推荐大家使用jedis连接池代替Jedis直连方式

~~~java
public class JedisConnectionFactory{
    private static final JedisPool JedisPool;
    
    static{
        JedisPoolConfig JedisPoolConfig = new JedisPoolConfig();
        //最大连接
        jedisPoolConfig.setMaxTotal(8);
        //最大空闲连接
        jedisPoolConfig.setMaxIdle(8);
        //最小空闲连接
        jedisPoolConfig.setMinIdle(0);
        //设置最长等待时间， ms
        jedisPoolConfig.setMaxWaitMillis(200);
        jedisPool = new JedisPool(jedisPoolConfig,"虚拟机ip",6379,1000,"密码");
    }
    //获取Jedis对象
    public static Jedis getJedis(){
        return jedisPool.getResoure();
    }
}
~~~

#### SpringDataRedis

SpringData是Spring中数据操作的模块，包含对各种数据库的集成，其中对Redis的集成模块就叫做SpringDataRedis，官网地址：https://spring.io/projects/spring-data-redis

- 提供了对不同Redis客户端的整合(lettuce和Jedis)
- 提供了RedisTemplate来统一API来操作Redis
- 支持Redis的发布订阅模型
- 支持Redis哨兵和Redis集群
- 支持基于Lettuce的响应式编程
- 支持基于JDK、JSON、字符串、Spring对象的数据结构序列化和反序列化
- 支持基于Redis的JDKCollection实现

##### SpringDataRedis快速入门

SpringDataRedis中提供了RedisTemplate工具类，其中封装了对Redis的各种操作。并且将不同数据类型的操作API封装到不同类型

| API  | 返回值类型 | 说明 |
| ---- | ---------- | ---- |
|RedisTemplate.opsForValue()      |ValueOperations            |操作String类型数据      |
|RedisTemplate.opsForHash()      |HashOperations            |操作Hash类型数据      |
|RedisTemplate.opsForList()      |ListOperations            |操作List类型数据      |
|RedisTemplate.opsForSet()      |SetOperations            |操作Set类型数据      |
|RedisTemplate.opsForZSet()      |ZSetOperations            |操作Sortedset类型数据      |
|RedisTemplate      |            |通用的命令     |

Springboot易筋经提供了对SpringDataRedis的支持，使用非常简单

1. 引入依赖

   ~~~java
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artfactId>spring-boot-starter-data-redis</artifactId>
   </dependency>
   <dependency>
       <groupId>org.apache.commons</groupId>
       <artfactId>common-pool</artifactId>
   </dependency>
   
   ~~~

2. spring

	```yaml
	spring:
		redis:
			host: 虚拟机ip
			port: 6379
			password: 123321
			lettuce:
				pool:
					max-active: 8 # 最大连接
					max-idle: 8 # 最大空闲连接
					min-idle: 0 #最小空闲连接
					max-wait: 100 # 连接等待时间
	```
	
3. 注入RedisTemplate

  ```java
  @Autowired
  private ReidsTemplate reidsTemplate;
  ```

4. 编写测试

  ~~~java
  @SpringBootTest
  public class RedisTest{
      @Autowired
  	private ReidsTemplate reidsTemplate;
   	@Test
      void testString(){
          //插入一条string类型的数据
          redisTemplate.opsForValue().set("name","李四");
          //读取一条string类型的数据
          Obiect name = redisTemplate.opsForValue().get("name");
          System.out.println("name="+name);
      }
  }
  ~~~

SpringDataRedis的使用步骤：

1. 引入spring-boot-starter-data-redis依赖
2. 在application.yml配置Redis信息
3. 注入RedisTemplate

##### SpringDataRedis的序列化方式

RedisTemplate可以接受任意Object作为值写入Redis，只不过写入前会把Object序列华为字节形式，默认采取JDK序列化

缺点：

- 可读性差
- 内存占用较大

我们可以自定义RedisTemplate的序列化方式

```java
@Bean
public RedisTemplate<String,Object> redisTemplate(RedisConnectionFactory redisConnecttionFactory) throws UnknownHostException{
    //创建Template
    RedisTemplate<String,Object> redisTemplate = new RedisTemplate<>();
    //设置连接工厂
    redisTemplate.setConnectionFactory(redisConnectionFactory);
    //设置序列化工具
    GenericJackson2JsonRedisSerializer jsonRedisSerializer = 
        								new GenericJackson2JsonRedisSerializer();
    //key和hashkey采用string序列化
    redisTemplate.setKeySerializer(RedisSerializer.string());
    redisTemplate.setHashKeySerializer(RedisSerializer.string());
    //value和hashValue采用JSON序列化
    redisTemplate.setValueSerializer(jsonRedisSerializer);
    redisTemplate.setHashValueSerializer(jsonRedisSerializer);
    return redisTemplate
}
```

##### StringRedisTemplate

json序列化，为了在反序列化时知道对象的类型，json序列化器会将类的class类型写入json结果中，存入Redis，会带来额外的缓存开销

为了节省内存空间，我们并不会使用JSON序列化器处理value，而是统一使用String序列化器，要求只能存储String类型的key和value。当需要存储java对象时，手动完成对象的序列化与反序列化。

Spring默认提供了一个StringRedisTemplate类，它的key和value的序列化方法默认就是String方式。省去了我们定义RedisTemplate

```java
@Autowired
private StringRedisTemplate stringRedisTemplate;
//JSON工具
private static final ObjectMapper mapper = new ObjectMapper();
@Test
void testStringTemplate() throws JsonProcessingException{
    //准备对象
    User user = new User("虎哥",18);
    //手动序列化
    String json = mapper.writeValueAsString(user);
    //写入一条数据到redis
    stringRedisTemplate.opsForValue().set("user:200",json);
    
    //读取数据
    String val = stringRedisTemplate.opsForValue().get("user:200");
    //反序列化
    User user1 = mapper.readValue(val, User.class);
    System.out.println("user="+user1);
}
```

## 实战篇

![image-20251001192428400](images/image-20251001192428400.png)

### 短信登录

#### 导入黑马点评项目

![image-20251001192744233](images/image-20251001192744233.png)

后端

不要忘了修改appication.yaml文件中的mysql、redis

前端

在nginx所在目录打开CMD，输入命令

```
start niginx.exe
```

打开chrome浏览器，打开开发者模式

#### 基于session实现登录

![image-20251001194036595](images/image-20251001194036595.png)

![image-20251001195330564](images/image-20251001195330564.png)



#### 集群的session共享问题

多台Tomcat并不共享session存储空间，当请求切换到不同tomcat服务时丢失数据的问题

session替代方案应该满足：

- 数据共享
- 内存存储
- key、value结构

![image-20251001201523530](images/image-20251001201523530.png)

#### 基于redis实现共享session登录

![image-20251001202148392](images/image-20251001202148392.png)

##### 登陆拦截器的优化

![image-20251001203710535](images/image-20251001203710535.png)

### 用户查询缓存

#### 什么是缓存

缓存就是数据交流的缓冲区(称作Cache)，是存储数据的临时地方，一般读写性能较高

![image-20251001211226905](images/image-20251001211226905.png)

![image-20251001211307992](images/image-20251001211307992.png) 

#### 添加redis缓存

![image-20251001212832293](images/image-20251001212832293.png)

#### 缓存更新策略

|          | 内存淘汰                                                     | 超时剔除                                                     | 主动更新                                   |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------ |
| 说明     | 不用自己维护，利用redis的内存淘汰机制，当内存不足时自动淘汰部分数据。下次查询时自动更新缓存 | 给缓存数据添加TTL时间，到期后自动删除缓存，下次查询时更新缓存 | 编写业务逻辑，在修改数据库的同时，更新缓存 |
| 一致性   | 差                                                           | 一般                                                         | 好                                         |
| 维护成本 | 无                                                           | 低                                                           | 高                                         |

业务场景：

- 低一致性需求：使用内存淘汰机制，例如店铺类型的查询缓存
- 高一致性需求：主动更新，并以超市提出作为兜底方案。例如店铺详情查询的缓存

##### 主动更新策略

1. Cache Aside Pattern
    有缓存的数据，在更新数据库的时候同时也更新缓存
2. Read/write Through Pattern
    缓存与数据库整合为一个服务，有服务来维护一致性。调用者调用该服务，无需关心缓存一致性问题
3. Write Behind caching Pattern
    调用者只操作缓存，有其他线程异步将缓存数据持久化到数据库最终保持一致

Cache Aside Pattern

删除缓存：更新数据库时，让缓存失效，查询时在更新缓存

保证缓存与数据库的操作是同时成功或失败

- 单体系统，将缓存与数据库操作放在一个事务
- 分布式系统，利用TCC等分布式服务方案

先删除缓存，再操作数据库

先操作数据库，在删除缓存
![image-20251001215128200](images/image-20251001215128200.png)

读操作：

- 缓存命中直接返回
- 缓存未命中则查询数据库，并写入缓存，设定超时时间

写操作：

- 先写数据库，然后在删除缓存
- 要确保数据库与缓存操作的原子性

#### 缓存穿透

缓存穿透是指客户端请求数据再缓存中和数据库中都不存在，这样的缓存永远不会生效，这些请求都会打到数据库

常见两种解决方案：

- 缓存空对象

    - 优点：实现简单，维护方便
    - 缺点：
        - 额外的内存消耗
        - 可能造成短期的不一致

    ![image-20251001220437987](images/image-20251001220437987.png)

- 布隆过滤

    - 优点内存占用较少，没有多余key
    - 缺点：
        - 实现复杂
        - 存在误判可能

    ![image-20251001220519396](images/image-20251001220519396.png)

- 增强id的复杂度，避免被猜测id规律

- 做好数据的基础格式校验

- 加强用户权限校验

- 做好热点数据限流

#### 缓存雪崩

缓存雪崩指的是同一时间段缓存大量的key同时失效或者Redis服务宕机，导致大量请求到达数据库，带来巨大压力

解决方案

- 给不同的Key添加TTL添加随机值
- 利用Redis集群提高高可用的可用性
- 给缓存业务添加降级限流策略
- 给业务添加多级缓存

![image-20251002101051647](images/image-20251002101051647.png)

#### 缓存击穿

缓存击穿问题也叫热点key问题，就是高并发访问并且缓存重建业务较复杂的key突然失效，无数的请求访问会在瞬间给数据库带来巨大冲击

![image-20251002101606414](images/image-20251002101606414.png)

常见解决方案由两种

- 互斥锁
- 逻辑过期

![image-20251002101847752](images/image-20251002101847752.png)

| 解决方案 | 优点                                           | 缺点                                           |
| -------- | ---------------------------------------------- | ---------------------------------------------- |
| 互斥锁   | 没有额外内存消耗<br />保证一致性<br />实现简单 | 线程需要等待，性能受影响                       |
| 逻辑过期 | 线程无需等待，性能较好                         | 不保证一致性<br />有额外内存消耗<br />实现复杂 |

互斥锁

![image-20251002104357414](images/image-20251002104357414.png)

逻辑过期

![image-20251002104555347](images/image-20251002104555347.png)

#### 缓存工具封装

### 优惠卷秒杀

#### 全局唯一ID

订单表使用数据库自增ID就存在一些问题

- id规律太明显
- 受单表数据量的限制

全局ID生成器，是一种在分布式系统下用来生成唯一ID的工具，一般满足以下特性

- 高可用
- 唯一性
- 高性能
- 安全性
- 递增性

为了增强ID的安全性，我们可以不直接使用redis自增的数值，而是拼接一些其他的信息

![image-20251002113810005](images/image-20251002113810005.png)

ID的组成部分：

符号位：1bit，永远为0

时间戳：31bit，一秒为单位可以用69年

序列号：32bit，秒内的计数器，支持每秒产生$2^{32}$个不同ID

全局唯一ID生成策略：

- UUID
- Redis自增
- snowflake算法
- 数据库自增

Redis自增Id策略：

- 每天一个key，方便统计订单量
- ID构造是时间戳+计数器

#### 实现优惠卷秒杀下单

每个店铺都可以发布优惠卷，分为平价卷和特价卷，平价卷可以随时购买，而特价卷需要秒杀抢购
表关系如下：

- tb_voucher:优惠卷的基本信息、优惠金额、使用规则等
- tb_seckill_vocher:优惠卷的库存，开始抢购的时间、结束抢购的时间。特价优惠店需要填写以下信息

在VoucherController中提供了一个接口，可以添加秒杀优惠卷：

```java
@RestController
@RequestMapping("/voucher")
public class VoucherController{
    
    @Resource
    private IVoucherService voucherService;
    
    /**
    *新增秒杀卷
    *@param voucher 优惠卷信息，包含秒杀信息
    *@return 优惠卷id
    */
    @PostMapping("seckill")
    public Result addSeckillVoucher(@RequestBody Voucher voucher){
        VoucherService.addSeckillVoucher(voucher);
        return Result.ok(voucher.getId())
    }

}
```

下单时需要判断两点：

- 秒杀是否开始或结束，如果尚未开始或已经结束无法下单
- 库存是否充足，不足则无法下单

![image-20251002212704068](images/image-20251002212704068.png)

#### 超卖问题

![image-20251002213553896](images/image-20251002213553896.png)

超卖问题时典型的多安全问题，针对这一问题的常见解决方案是加锁

悲观锁：认为线程安全问题一定发生，因此在操作数据是先获取锁，确保线程串行执行

- 例如Synchronized、lock都属于悲观锁

乐观锁：认为线程安全问题不一定会发生，因此不加锁，只是在更新数据去判断有没有其他线程对数据做了修改

- 如果没有数据修改则认为是安全的，自己才更新数据
- 如果已经被其他线程修改说明发生了安全问题，此时可以重试或异常

乐观锁的关键是判断之前查询得到的数据是否修改过，常见方式有两种：

- 版本号法

    | id   | stock | version |
    | ---- | ----- | ------- |
    | 10   | 1     | 1       |

    ![image-20251002214830283](images/image-20251002214830283.png)

- CAS法

    | id   | stock |
    | ---- | ----- |
    | 10   | 1     |

    ![image-20251002215021563](images/image-20251002215021563.png)

    优点：性能好

    缺点：成功率低

#### 一人一单

![image-20251002215909905](images/image-20251002215909905.png)

#####  并发安全问题

通过加锁可以解决单机情况下一人一单安全问题，但在集群模式下就不行了

1. 我们将服务启动两份，端口为8081和8082
2. 然后修改nginx的conf目录下的nginx.conf文件，配置反向代理和负载均衡

现在，用户请求会在这两个节点负载均衡，再次测试下是否存在线程安全问题

![image-20251002221514855](images/image-20251002221514855.png)

#### 分布式锁

![image-20251003100700474](images/image-20251003100700474.png)

分布式锁：满足分布式系统或集群模式下多进程可见并且互斥锁

![image-20251003100827598](images/image-20251003100827598.png)

分布式锁的核心是实现多线程之间互斥，而满足这一点的方式有很多，常见有三种：

|        | MySQL                     | Redis                    | ZooKeeper                  |
| ------ | ------------------------- | ------------------------ | -------------------------- |
| 互斥   | 利用mysql本身的互斥锁机制 | 利用setnx这样的互斥命令  | 利用节点唯一性和有序性互斥 |
| 高可用 | 好                        | 好                       | 好                         |
| 高性能 | 一般                      | 好                       | 一般                       |
| 安全性 | 断开连接，自动释放锁      | 利用锁超时时间，到期释放 | 临时节点，断开连接自动释放 |

##### 实现redis锁时需要实现的两个基本方法

- 获取锁：

    - 互斥：确保只有一个线程能获得锁

    - 非阻塞：尝试一次，成功返回true，失败返回false

        ```redis
        #添加锁，利用setnx的互斥特性
        SETNX lock thread1
        #添加所得过期时间，避免服务宕机引起的死锁
        EXPIRE lock 10
        ```

        ```redis
        #添加锁，NX是互斥，EX是设置超时时间
        SET lock thread1 NX EX 10
        ```

        

- 释放锁：

    - 手动释放

    - 超时释放：获取锁时添加一个超时时间

        ```redis
        # 释放锁，删除即可
        DEL key
        ```

    ![image-20251003103153304](images/image-20251003103153304.png)

    

##### 基于redis实现分布式锁初级版本

    需求定义一个类，实现以下接口。利用Redis实现分布式锁功能
    
    ```java
    public interface Ilovk{
        /**
        *尝试获取锁
        *@param timeoutSec 锁持有的超时时间，过期后自动释放
        *@return true 代表获取锁成功，false代表获取锁失败
        */
        
        boolean tryLock(long timeoutSec);
        
        /**
        *释放锁
        */
        void unlock();
    }
    ```


​     
​    
​    ```java
​    public class SimpleRedisLock implements ILock{
​        private String name;
​        private StringRedisTemplate stringRedisTemplate;
​        
​        public SimpleRedisLock(String name,StringRedisTemplate stringRedisTemplate) {
​    		this.name=name;
​           	this.stringRedisTemplate = stringRedisTemplate;
​        }
​        
​        private static final  String KEY_PREFIX = "lock:";
​        @Override
​        public boolean trylock(long timeoutSec){
​            long threaId = Thread.currentThread().getID();
​            Boolean success = stringRedisTemplate.opsForValue().setIfAbsent(Key_PREFIX+name,threadId+"",timeoutSec,TimeUnit.SECONDS);
​            return Boolean.TRUE.equals(success);
​        }
​        
​        public void unlock(){
​            stringRedisTemplate.delete(KEY_PREFIX+name);
​        }
​    }
​        
​    ```

##### 分布式锁误删

![image-20251003111714128](images/image-20251003111714128.png)
改进Redis分布式锁实现，满足：

1. 在获取锁的时候存入线程表示(可以用UUID表示)
2. 在释放锁时先获取锁中的线程标示，判断与当前线程表示一致
    - 如果一致则释放锁
    - 如果不一致则不释放锁   

```java
 public class SimpleRedisLock implements ILock{
        private String name;
        private StringRedisTemplate stringRedisTemplate;
        public SimpleRedisLock(String name,StringRedisTemplate stringRedisTemplate) {
	this.name=name;
   	this.stringRedisTemplate = stringRedisTemplate;
}

	private static final  String KEY_PREFIX = "lock:";
	@Override
	public boolean trylock(long timeoutSec){
    	long threaId = Thread.currentThread().getID();
    	Boolean success = stringRedisTemplate.opsForValue().setIfAbsent(Key_PREFIX+name,threadId+"",timeoutSec,TimeUnit.SECONDS);
    	return Boolean.TRUE.equals(success);
}

	public void unlock(){
        String threaId = Thread.currentThread().getID();
        String id = stringRedisTemplate.opsForValue().get(Key_PREFIX+name);
        if(threaID.equals(if)){
    	stringRedisTemplate.delete(KEY_PREFIX+name);
		}
    }
}
```


##### 分布式锁的原子性

![image-20251003114826186](images/image-20251003114826186.png)

##### Redis的Lua脚本

Redis提供了Lua脚本的功能，在一个Redis脚本编写多条命令，确保多条命令执行时的原子性。Lua是一种编程语言

Redis提供的调用函数

```lua
#执行redis命令
redis.call('命令名称','key','其他参数',...)
```

写好脚本以后使用redis命令调用脚本，调用脚本常见命令如下：

```redis
EVAL script numkeys key [key...] arg [arg ...]
```

scripts脚本内容

numkeys需要传参的个数

如果脚本中的key、value不想写 死，可以作为参数传递。key类型参数会放入KEYS数组，其他参数会放入ARGV数组，在脚本中可以从KEYS和ARGV数组获取这些参数

释放锁的业务流程：

1. 获取锁中的线程表示
2. 判断是否与指定表示(与当前线程表示)
3. 如果一致则释放锁
4. 如果不一致，则什么也不做

```lua
--锁的kety
local key = KEYS[1]
--当前线程表示
local threadId = ARGV[1]

--获取锁中的线程表示 get key
local id = redis.call('get',key)
--比较线程表示与锁的表示是否一致
if(id == threaId) then
    --释放锁 del key
    return redis.call('del',key)
end
return 0
```

```lua
--比较线程表示与锁的表示是否一致
if(redis.call('get',KEYS[1])==ARGV[1]) then
    --释放锁
    return redis.call('del',KEYS[1])
end
return 0
```

特性：

- 利用set nx满足互斥性
- 利用set ex保证故障时锁依然能释放，避免死锁，提高安全性
- 利用Redis集群保证高可用和高并发特性

##### 再次改进redis分布式锁

需求：基于lua脚本实现分布式锁的逻辑

提示：RedisTemplate调用lua脚本的API如下

```java
class redis{
    @override
    public <T> T excute(RedisScipt<T> script,List<K> keys, Object... args){
        return scriptExecutor.execute(script,keys,args)
    }
}
```

##### 基于redis的分布式锁优化

基于setnx实现的分布式锁存在下面问题：

1. 不可重入
    同一个线程无法多次获取同一把锁
2. 不可重试
    获取锁只尝试一次就返回false
3. 超时释放
    锁超时释放虽然可以避免死锁，但是业务执行耗时较长，也会导致锁释放，存在安全隐患
4. 主从一致性
    如果redis提供了主从集群，主从同步存在延迟，当主宕机时，如果从并同步主中的所数据，则会出现锁实现

##### Redssion

Redssion是一个在redis基础上实现的java驻内存数据网络(In-Memory Data Grid)。它不仅提供了一系列分布式的Javachangu对象，还提供了许多分布式的服务，其中就包含了各种分布式锁的实现

![image-20251003204947493](images/image-20251003204947493.png)

1. 引入依赖

    ```xml
    <depency>
    	<groupId>org.redisson</groupId>
    	<artifactId>redission</artifactId>
    	<version>3.13.6<version>
    </depency>
    ```

2. 配置Redssion客户端

    ```java
    @configuration
    public class RedisConfig{
    	@Bean
    	public RedssionCilent redissonClient(){
            //配置类
            Config config = new Config();
            //添加redis地址，这里添加了单点地址,也可以使用config.useClusterServers()添加集群地址
            config.useSingleServer().setAddress("redis://IP:6379").setPassword("password");
            //创建客户端
            return Redisson.create(config);
        }
    ```

3. 使用Redission的分布式锁

    ```java
    @resource
    private RedissonCilent redissonCilent;
    @Test
    void testRedisson() throws InterruptedException{
        //获取锁(可重入)，指定所得名称
        Rlock lock = redissionCilent.getclock("anyLock");
        //尝试获取锁，参数分别是：获取锁的最大等待时间（期间会重试,锁自动释放的时间，时间单位
        boolean isLock = Lock.tryLock(1,10,TimeUnit.SECONDS);
        //尝试判断获取成功
        if(isLock){
            try{
                System.out.println("执行业务");
            }finally{
                lock.unlock();
            }
        }
    }
    ```

##### Redis可重入锁的原理

![image-20251003211842251](images/image-20251003211842251.png)

```lua
local key = KEYS[1];--锁的key
local threadId = ARGV[1];--线程唯一标识
local releaseTime = AGRV[2]; -- 锁的自动释放时间
--判断所是否还是被自己持有
if(redis.call('HEXISTS',key,threadId)==0) then
    return nil; -- 如果不是自己的则直接返回
end;
--是自己的锁，则重入次数-1
local count = redis.call('HINCRBY',key,threadId,-1);
--判断是否重入次数已经为0
if(count>0) then
    --大于0，说明不能释放锁吧，重置有效期然后返回
    redis.call('EXPIRE',key,releaseTime);
    return nil;
else --等于-，说明可以释放锁，直接删除
    redis.call('DEL'，key);
    return nil;
end;
    
```

![image-20251003215046973](images/image-20251003215046973.png)

Redisson分布式锁原理

- 可重入：利用hash结果记录线程id和冲入次数
- 可重试：利用信号量和PubSub功能实现等待、唤醒、获取锁失败的重试机制 

##### Redission分布式锁主从一致性问题

原理：多个独立的redis节点，必须所有解放点都获取重入锁，才算获取锁成功

缺陷：运维成本高、实现复杂

![image-20251003220209174](images/image-20251003220209174.png)

#### Redis优化秒杀

![image-20251004093429136](images/image-20251004093429136.png)

![image-20251004093702244](images/image-20251004093702244.png)

需求：

1. 新增秒杀优惠卷的同时，将优惠卷的信息保存到redis中
2. 基于lua脚本、判断秒杀库存、一人一单、决定用户是否抢购成功
3. 如果抢购成功，将优惠卷id和用户id封装后存入阻塞队列
4. 开启线程任务，不断从阻塞队列中获取消息，实现异步下单功能

```lua
--1.参数列表
--1.1优惠卷id
local vocherId = ARGV[1]
--1.2用户id
local userId = ARGV[2]

--2.数据key
--2.1 库存key
local stockKey = 'seckill:stock' .. voucherId
--2.2 订单key
local orderKey = 'seckill:order' .. voucherId

--3.脚本业务
--3.1判断脚本是否充足
if(tonumber(redis.call('get',stockKey))<=0) then
    --3.2库存不足,返回1
    return 1
end
--3.2判断用户是否下单SISMEMBER
if(redis.call('sismember',orderKey,useId)==1) then
	--3.3存在，说明是重复下单，返回2
    return 2
end
--3.4扣库存 incrby,stockKey -1
redis.call('incrby',stockKey,-1)
--3.5下单(保存用户)
redis.call('sadd',orderKey,useId)
```

基于阻塞队列的异步秒杀问题

- 内存限制问题
- 数据安全问题  

#### Redis消息队列实现异步秒杀 

消息队列(Message Queue)，字面意思是存放消息的队列。最简单的消息队列包含三个角色：

- 消息队列：存储和管理消息，也被称为消息代理(Message Broker)
- 生产者：发送消息到消息队列
- 消费者：从消息队列获取消息并处理消息

![image-20251004103221828](images/image-20251004103221828.png)

Redis提供了三种不同的方式来实现消息队列

- list结构：基于List结构模拟消息队列
- PubSub：基本的点对点消息模型
- Stream：比较完善的消息队列

##### 基于List结构模拟消息队列

消息队列(Message Queue)，字面意思是存放消息的队列。而redis的list结构是一个双向链表很容易模仿出队列的效果

队列的入口和出口不在一边，，因此我们可以利用：LRUSH结合RPOP、或者RPUSH结合LPOP来实现

不过要注意的是，队列中没有消息时RPOP和LPOP操作会返回null，并不像JVM阻塞队列那样会阻塞并等待消息

因此这里应该使用BRPOP或者BLPOP来实现阻塞效果

![image-20251004104537823](images/image-20251004104537823.png)

优点：

- 利用redis存储，不受限于JVM内存上限
- 基于redis的持久化机制，数据安全性有保证
- 可以满足消息有序性

缺点：

- 无法避免消息丢失
- 支支持单消费者

##### 基于PubSub的消息队列

PubSub(发布订阅)是Redis2.0版本引进的消息传递模型。顾名思义，消费者可以订阅一个或多个channel，生产者，相对应的channel发送消息后，所有订阅者都能收到相关消息

- SUBSCRIBE channel [channel]：订阅一个或多个频道
- PUBLISH channel msg：向一个频道发送信息
- PSUBSCRIBE pattern[pattern]：订阅与pattern格式匹配的所有频道

![image-20251004105417811](images/image-20251004105417811.png) 

优点：

- 采用发布订阅模型，支持多生产、多消费

缺点：

- 不支持数据持久化
- 无法避免消息丢失
- 消息堆积有上限，超出时数据丢失

##### 基于Stream的消息队列

Stream是redis5.0引入的一种新的数据类型，可以实现一个功能非常完整的消息队列

![image-20251004110406452](images/image-20251004110406452.png)

![image-20251004110451809](images/image-20251004110451809.png)

XREAD阻塞方式
![image-20251004111932798](images/image-20251004111932798.png)

XREAD阻塞方式，读取最新消息：

![image-20251004112043542](images/image-20251004112043542.png)

在业务开发中，我们呢可以循环调用XREAD阻塞方式来查询最新的信息，从而实现持续监听队列的效果，伪代码如下：

```java
while(true){
	//尝试获取队列中的消息，最多阻塞2秒
	Object msg = redis.excute("XREAD COUNT 1 BLOCK 2000 STREAMS users $");
	if(msg == null){
		continue;
	}
	
	//处理消息
	handleMessage(msg);
}
```

注意：

当我们指定起始ID为$是，代表读取最新消息，如果我们处理一条信息的过程中，又有超过一条以上的消息到达队列，则下次获取时也只能获取到最新的一条，会出现漏读消息的情况

##### 基于Sream的消息队列-消费者组

消费者组（Consumer Group）：将多个消费者划分到一个组内，监听同一个队列。具备以下特点

1. 消息分流
    队列中的消息会分流给组内的不同的消费者，而不是重复消费，从而加快消息处理的速度
2. 消息标示
    消费者会维护一个标示，记录最后一个被处理的消息，哪怕消费者宕机重启，还会从标示中读取消息。确保每一个消息都消费
3. 消息确认
    消费者获取消息之后，消息处于一个pending状态，并存入pending-list，当处理完成后需要通过XACK来确认消息，标记消息为已处理，才会从pending-list移除

创建消费者组

```redis
XGROUP CREATE key groupName ID [MKSTREAM]
```

- key：队列名称
- groupName：消费者组名称
- ID：起始ID表识，$代表队列中最后一个消息,0代表队列中第一个消息
- MKSTREAM：队列不存在时自动创建队列

其他常见命令

![image-20251004114328915](images/image-20251004114328915.png)

从消费者组读取消息

```
XREADGROUP GROUP group consumer [COUNT cpunt] [BLOCK milliseconds] [NOACK] STREAMS key[key...] ID[ID...]
```

- group：消费组名称
- consumer：消费者名称，如果消费者不存在，会自动创建一个消费者
- count：本次查询的最大数量
- BLOCK milliseconds：当没有消息时最长等待时间
- NOACK：无需手动确认ACK，获取消息后自动确认
- STREAM key：指定队列名称
- ID：获取消息的起始ID：
    - ">"：从下一个未消费的的消息开始
    - 其他：根据指定id从pending-list中获取以消费但未确认的消息，例如0，是从pending-list中的第一个消息开始

```java
while(true){
	//尝试获取队列中的消息，最多阻塞2秒
	Object msg = redis.excute("XREAD COUNT 1 BLOCK 2000 STREAMS users $");
	if(msg == null){
		continue;
	}
	try{
	//处理消息，完成ACK
	handleMessage(msg);
	}catch(Exexption e){
        while(true){
            Object msg = redis.call("SREADGROUP GROUP g1 c1 COUNT 1 STREAMS s1 0");
            if(msg==null){
                break;
            }
            try{
                //如果有异常消息，再次处理
                handleMessage(msg);
            } catch(Exception e){
                //再次出现异常，记录日志，继续循环
                continue;
            }
        }
    }
}
```

XREADGROUP命令特点：

- 消息可回溯
- 可以多消费者争抢信息，加快消费速度
- 可以阻塞读取
- 没有消息漏读的风险
- 有消息确认机制，保证消息至少被消费一次

|              | List                                     | PubSub             | Stream                                                 |
| ------------ | ---------------------------------------- | ------------------ | ------------------------------------------------------ |
| 消息持久化   | 支持                                     | 不支持             | 支持                                                   |
| 阻塞读取     | 支持                                     | 支持               | 支持                                                   |
| 消息堆积处理 | 受限于内存空间，可以利用多消费者加速处理 | 受限于消费者缓冲区 | 受限于队列长度，可以利用笑得这组提高消费速度，减少堆积 |
| 消息确认机制 | 不支持                                   | 不支持             | 支持                                                   |
| 消息回溯     | 不支持                                   | 不支持             | 支持                                                   |

##### 基于Redis的Stream结构作为消息队列，实现异步秒杀下单

需求：

1. 创建一个Stream类型的消息队列，名为Stream.orders
2. 修改之前的lua脚本，在认定有抢购资格后，直接向stream.orders中添加信息，内容包含voucherld，userId，orderIs
3. 项目启动时，开启一个线程任务，尝试获取Stream.orders中的信息，完成下单

### 达人探店

#### 发布探店笔记

探店笔记类似点评网站的评价，往往时图文结合。对应的表有两个

- tb_blog：探店笔记表，包含笔记中的标题、文字、图片等
- tb_blog_comments：其他用户对探店笔记的评价

![image-20251004192220955](images/image-20251004192220955.png)

需求：点击首页的探店笔记，会进入详情界面，实现该界面的查询接口
![image-20251004192625521](images/image-20251004192625521.png)

#### 点赞

完善点赞功能

需求：

- 同一个用户只能点赞一次，再次点击则取消点赞
- 如果当前用户已经点赞，则点赞按钮高亮显示(前端以实现，判断字段Blog类的islike属性)

实现步骤：

1. 给Blog类中添加一个isLike，表示是否被当前用户点赞 
2. 修改点赞功能，利用Redis的set集合判断是否是否点赞过，未点赞过的则点赞数+1，以点赞过则点赞数-1
3. 修改根据id查询Blog的业务，判断当前登录的用户是否点赞过，赋值给isLike字段
4. 修改分页查询的Blog业务，判断当前登录用户是否点赞过，赋值给isLike字段

![image-20251004194151809](images/image-20251004194151809.png)

数据更新成功才更新redis，做法拷贝if(isSuccess)

#### 点赞排行榜

在探店笔记的详情页应该把给该笔记点赞的人显示出来，比如最早点赞的TOP5，形成点赞排行榜

![image-20251004194704500](images/image-20251004194704500.png)

|          | List                       | Set          | SortedSet       |
| -------- | -------------------------- | ------------ | --------------- |
| 排序方式 | 按添加顺序排序             | 无法排序     | 根据score值排序 |
| 唯一性   | 不唯一                     | 唯一         | 唯一            |
| 查找方式 | 按索引查找<br />或首尾查找 | 根据元素查找 | 根据元素查找    |

### 好友关注

#### 关注和取关

需求：基于该表的数据结构，实现两个接口

1. 关注和取关接口
2. 判断是否关注接口

关注是User之间的关系，是博主与粉丝的关系，数据库中有一张表tb_follow表来表示：

注意：这里需要把主键修改尾自增长，简化开发

#### 共同关注

![image-20251004203324039](images/image-20251004203324039.png)

#### 关注推送

关注推送也叫Feed流，自己已尾投喂。为用户提供"沉浸式"的体验，通过无限下拉获取新的信息

![image-20251004204320546](images/image-20251004204320546.png)

Feed流实现由两种常见的方式

- Timeline：不做内容的筛选，简单的按照内容发布时间排序，常用于好友或关注。例如朋友圈
    - 优点：信息全面，不会由缺失，并且实现，相对简单
    - 缺点：信息噪音较多，用户不一定感兴趣，内容获取效率较低
- 智能排序：利用智能算法频闭掉违规的、用户不敢兴趣的内容。推送用户感兴趣信息，用户黏度很高，容易沉迷
    - 优点：投喂用户感兴趣信息，用户黏度很高，容易沉迷
    - 缺点：如果算法不精准，很可能起反作用

基于关注好友来做Feed流，因此采用TimeLine的模式，

- 拉模式
    也叫读扩散
    ![image-20251004205136777](images/image-20251004205136777.png)

    

- 推模式
    也叫写扩散
    ![image-20251004205249389](images/image-20251004205249389.png)

- 拉推结合
    也叫做读写结合，兼具推和拉两种模式的优点
    ![image-20251004205451411](images/image-20251004205451411.png)

|              | 推模式   | 拉模式            | 推拉结合            |
| ------------ | -------- | ----------------- | ------------------- |
| 写比例       | 低       | 高                | 中                  |
| 读比例       | 高       | 低                | 中                  |
| 用户读取延迟 | 高       | 低                | 低                  |
| 实现难度     | 复杂     | 简单              | 很复杂              |
| 使用场景     | 很少使用 | 用户量少，没有大V | 过千万粉丝量，有大V |

##### 基于推模式实现关注推送功能

需求：

1. 修改新增探店业务，在保存blog到数据库的同时，推送到粉丝的收件箱
2. 收件箱满足可以根据时间戳排序，必须使用Redis的数据结构实现
3. 查询收件箱数据时，可以实现分页查询

```java
@pastMapping
public Result saveBlog(@RequestBody Blog blog){
    //获取登录用户
    UserDTO user = UserHolder.getUser();
    blog.setUserId(user.getId());
    //保存探店笔记
    blogService.save(blog);
    return Result.ok();
}
```

Feed流中的数据会不断更新，所以数据的角标也在变化，因此不能使用传统的分页模式

![image-20251004210726376](images/image-20251004210726376.png)

##### 实现关注推送页的分页查询

![image-20251004211631513](images/image-20251004211631513.png)

### 附近商户

#### GEO数据结构

GEO就是Geolocation的简写形式，代表地理坐标，Redis在3.2版本中加入了对GEO的支持，允许存储地理坐标信息，帮助我们根据经纬度检索数据。常见的命令有：

GEOADD：添加一个地理位置信息，包含：经度，纬度，值

GEODIST：计算指定两个点之间的距离并返回

GEOHASH：将指定member的坐标转化为hash字符串的形式并返回

GEOPOS：返回member坐标

GEORADIUS：指定圆心、半径，找到该圆内所有的member，并按照与圆心之间的距离排序后返回。6.2以弃用

GEOSEARCH：在指定范围内搜索member，并按照与指定点之间的距离排序后返回。范围可以是圆形或矩形。6.2新功能

GEOSEARCHSTORE：与GEOSEARCH功能一致，不过可以把结果存储到一个指定的key。6.2新功能

#### 附近商户搜索 

按照商户类型做分类，类型相同的商户作为同一组，以typeld为key存入同一个GEO集合中即可 	

![image-20251004215017783](images/image-20251004215017783.png)

SpringDataRedis的2.3.9版本并不支持Redis6.2提供的GEOSEARCH命令，因此我么提示需要修改该版本，修改自己的POM文件

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.data</groupId>
            <artifactId>spring-data-redis</artifactId>
        </exclusion>
        <exclusion>
            <artifactId>lettuce-core</artifactId>
            <groupId>io.lettuce</groupId>
        </exclusion>
    </exclusions>
</dependency>
<dependency>
    <groupId>org.springframework.data</groupId>
    <artifactId>spring-data-redis</artifactId>
    <version>2.6.2</version>
</dependency>
<dependency>
    <artifactId>lettuce-core</artifactId>
    <groupId>io.lettuce</groupId>
    <version>6.1.6.RELEASE</version>
</dependency>
```

### 用户签到

加入我们用一张表来存储用户信息，其结构应该如下

```sql
CREATE TABLE'tb_sign'(
'id'bigint(2O）unsigned NOT NULL AUTO_INCREMENT COMMENT'主键',
'user_id'bigint(20）unsigned NOT NULL COMMENT'用户id',
'year'year（4）NOTNULLCOMMENT'签到的年',
'month'tinyint（2）NOTNULLCOMMENT'签到的月',
'date'dateNOTNULLCOMMENT'签到的日期',
'is_backup'tinyint（1）unsigned DEFAULT NULL COMMENT'是否补签',
PRIMARY KEY（'id'）
)ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
```

#### BitMap

我们按月来统计用户的签到信息，签到记录为1，未签到记录为0
![image-20251005104954485](images/image-20251005104954485.png)

把每一个bit位对应当月的每一天，形成了映射关系。用0或1表示业务状态。用0和1表示业务状态，这种思路称为位图(BitMap)

Redis中是利用string类型数据结构实现BitMap，因此最大上限是512M，转化为bit则是$2^{32}$个bit位

BitMap的操作命令有：

SETBIT：向指定位置(offset)存入一个0或1

GETBIT：获取指定位置(offset)的bit值

BITCOUNT：统计BitMap中值为1的bit位的数量 

BITFIELD：操作（查询，修改，自增）BitMap中bit数组中的指定位置指定位置(offset)的值

BITFILELD_RO：获取BitMap中bit数组，并以十进制形式返回

BITOP：将多个BitMap的结果做位运算(与、或、异或)

BITPOS:查找bit数组中指定范围内第一个0或1出现的位置

#### 签到功能

![image-20251005112921708](images/image-20251005112921708.png)

#### 签到统计

连续签到天数

从最后一次签到开始向前统计，直到遇到第一次未签到为止，计算总的签到次数，就是连续签到天数

本月到今天的所有签到数据

BITFIELD key GET u[dayOfMonth] 0

如何从后往前遍历每个bit位

与1做位运算，就能得到最后一个bitwei

随后右移1位，下一个bit位就成为了最后一个bit位

![image-20251005113908061](images/image-20251005113908061.png)

### UV统计

- UV
    全称Unique Visitor，也叫独立访客量，是指通过互联网访问，浏览这个网页的自然人，1天内同一个用户多此访问该网站，只记录一次
- PV
    全称Page View，也叫做页面访问量或点击量，用户每访问网站的一个界面，记录一次PV，用户多此打开页面，则记录多此PV，往往用来衡量网站的流量

#### HyperLoglog用法

HyperLoglog(HLL)是从Loglog算法派生出的概率算法，用于确定非常大的集合的基数，而不需要存储其所有值

Redis中的HLL是基于string结构实现的，单个HLL的内存永远小于16kb，内存占用地的发指，作为代价其测量结果是概率性，有小雨0.81%概率的误差，不过对于UV统计来说，完全可以忽略

```
PFADD key element [element ...]

PFCOUNT key[key ...]

PFMERGE destkey sourcekey [sourcekey ...]
```

#### 实现UV统计

查看内存占用和统计效果

```java
@Test
void testHyperLogLog() {
    //准备数组，装用户数据
    String[] users = new String[1000];
    //数组角标
    int index = 0;
    for （int i = 1;i <= 1000000; i++）{
        //赋值
        users[index++] = "user_"+i;
        //每1000条发送一次
        if （i % 1000 == 0） {
        index = 0;
        stringRedisTemplate.opsForHyperLogLog() .add("hlli", users) ;
        }
    }
    //统计数量
    Long Size = stringRedisTemplate.opsForHyperLogLog().size("hlli") ;
    System.out.println("size = " + size) ;
}
```

## 高级篇

### 分布式缓存

#### 单点redis的问题

单点Redis的问题

数据丢失问题

实现Redis数据持久化

并发能力问题

搭建主从集群，实现读写分离

故障恢复问题

利用Redis哨兵，实现健康检测，及自动恢复

存储能力问题

搭建分片集群，利用插槽机制实现动态扩容

#### Redis持久化

##### RDB

RDB全称是Redis Database Backup file(Redis数据备份文件)，也叫做Redis数据快照。简单来说就是把内存中的所有数据都记录在磁盘中。当Redis实例故障重启后，从磁盘读取快照文件，恢复数据

快照文件称为RDB文件，默认是保存在当前运行目录

```
save
#由Redis主进程来执行RDB，会阻塞所有命令
bgsave
#开启子进程执行RDB，避免主进程受到影响
```

Redis内部有触发RDB机制，可以在redis.conf文件中找到，格式如下

```c
#900秒内，如果至少有1个key被修改，则执行bgsave，如果是save ""在表示禁用RDB
save 900 1
save 300 10
save 60 10000
```

RDB的其他配置也可以在redis.conf文件中设置

```c
#是否压缩，建议不开启，压缩也会消耗cpu，磁盘的话不值钱
rdbcompression yes
    
#RDB 文件名称
dbfilename dump.rdb

#文件保存的路径目录
dir ./
```

brsqve开始时会fork主进程得到子进程，子进程共享主进程的内存数据，完成fork后读取内存数据并写入RDB文件

fork采用的是copy-on-write技术：

- 当主进程执行读操作，访问共享内存
- 当主进程执行写操作是，则会拷贝一份数据，执行写操作

![image-20251005152429162](images/image-20251005152429162.png)

##### AOF

AOF全称位Append Only File(追加文件)。Redis处理的每一个写命令都会记录在AOF文件，可以看作是命令日志文件
![image-20251005153013203](images/image-20251005153013203.png)

AOF默认是关闭的，需要修改redis.conf配置文件来开启AOF

```json
#是否开启AOF功能，默认是no
appendonly yes
#AOF文件的名称
appendfilename "appendonly.aof"
```

AOF的命令记录的频率也可以通过redis.conf文件来配

```json
#表示每执行一次写命令，立即记录到AOF文件
appendfsync  always
#写命令执行完先放入AOF的缓冲区，然后每隔一秒将缓冲区的数据写到AOF文件，是默认方案
appendfsync everysec
#写命令执行完先放入AOF缓冲区，由操作系统决定何时将缓冲区内容写回磁盘
appendfsync no
```

| 配置项   | 刷盘时机     | 优点                   | 缺点                       |
| -------- | ------------ | ---------------------- | -------------------------- |
| Always   | 同步刷盘     | 可靠性高，几乎不丢数据 | 性能影响大                 |
| everysec | 每秒刷盘     | 性能始终               | 最多丢失1秒数据            |
| no       | 操作系统配置 | 性能最好               | 可靠性差，可能丢失大量数据 |

因为是记录命令，AOF文件回避RDB文件大的多。而且AOF记录对同一个key的多次写操作，但只有最后一次写操作才有意义。通过执行bgrewriteof命令，可以让AOF文件执行重写功能，用最少的命令达到相同的效果

![image-20251005154747288](images/image-20251005154747288.png)

Redis也会在触发阈值随时自动去重写AOF文件。阈值也可以在Redis.conf中配置

```json
#AOF文件比上次文件增长超过多少百分比则触发重写
auto-aof-rewrite-percentage 100
#AOF文件体积最小多大以上才触发重写
auto-aof-rewrite-min-size 64mb
```

RDB和AOF各有自己的优缺点，但如果对数据的安全性要求较高，实际开发中往往会结合两者使用

|                | RDB                                          | AOF                                                        |
| -------------- | -------------------------------------------- | ---------------------------------------------------------- |
| 持久化方式     | 定时对整个内存做快照                         | 记录每一次执行的命令                                       |
| 数据完整性     | 不完整，两次备份之间会丢失                   | 相对完整，取决于刷盘策略                                   |
| 文件大小       | 会有压缩，文件体积小                         | 记录命令，文件体积很大                                     |
| 宕机恢复速度   | 很快                                         | 慢                                                         |
| 数据恢复优先级 | 低，完整性不如AOF                            | 高。因为数据完整性更高                                     |
| 系统资源占用   | 高，大量CPU和内存的消耗                      | 低，主要是磁盘IO资源<br />但AOF重写时占用大量CPU和内存资源 |
| 使用场景       | 可以容忍数分钟的数据丢失，追求更快的启动速度 | 对数据安全性要求较高，常见                                 |

#### Redis主从  

##### 搭建主从架构 

单节点Redis的并发能力是有上限的，要进一步提高Redis的并发能力，就需要搭建主从集群，实现读写分离
![image-20251005155935510](images/image-20251005155935510.png) 

1. 在工作目录，创建目录 

    ```sh
    mkdir 7001 7002 7003
    ```

2. 恢复原始配置
    开启RDB，关闭AOF

3. 拷贝配置文件到每个目录
    将redis.conf文件拷贝到三个目录中(/tmp目录下)

    ```sh
    echo 7001 7002 7003 |xargs -t -n 1 cp redis-version/reids.conf
    ```

4. 修改每个文件夹内的配置文件

    ```sh
    sed -i -e 's/6379/7001/g' -e 's/dir .\//dir \/tmp\/7001//g' 7001/redis.conf
    ```

5. 修改实例中的IP
    redis.cong文件中指定每一个实例绑定的IP信息，格式如下

    ```
    replica-announce-ip IP
    ```

    ```sh
    sed -i 'la replica -ip IP' port/redis.conf
    ```

6. 开启主从关系

    - 修改配置文件(永久生效)

        - 在reids.conf中添加一行配置:

            ```
            slaveof <masterip> <masterport>
            ```

    - 使用redis-cli客户端连接到redis服务，执行slaveof命令(重启后失效)：

        - ```
            slaveof <masterip> <masterport>
            ```

    注：在5.0以后新增命令replicaof 与slaveof效果一致

##### 主从数据同步原理

###### 全量同步

主从第一次同步时全量同步：

![image-20251005161909393](images/image-20251005161909393.png)

Repliaction Id:简称replid，是数据集的标记，id一致则说明是同一数据集。每一个master都有唯一的replid，slave则会继承master节点的replid

offset：偏移量，随着记录在repl_baklog中的数据增多而逐渐增大，slave完成同步时会记录当前同步的offset，如果slave的offset小于master的offset，说明slave数据落后master需要更新

因此slave作数据同步，必须向master声明自己的replication id和offset，master才可以判断到底需要同步那些数据

###### 增量同步

如果slave重启后同步，则进行增量同步

![image-20251005163526696](images/image-20251005163526696.png)

注意：repl_baklog大小有上限，写满后会覆盖最早的数据。如果slave断开时间太久，导致尚未备份的数据被覆盖，则无法基于log作增量同步，只能再次全量同步

优化主从集群

- 在master配置repl-diskless-sync yes启用五磁盘赋值，避免全量同步时的磁盘IO
- Redis单节点上的内存不要占用太大，较少RDB导致的过多磁盘IO
- 适当提高repl_baklog的大小，发现slave宕机时尽快实现故障恢复，尽可能避免全量同步
- 限制一个节点上的slave节点数量，如果实在太多slave，则可以采用主-从-从链式结构，减少master的压力

#### Redis哨兵

##### 哨兵的作用和原理

Redis提供了哨兵(Sentinel)机制来实现主从集群的自动故障恢复。哨兵的结构和作用如下：

- 监控：Sentinel会不断检查您的master和slave是否按预期工作
- 自动故障恢复：如果master故障，Sentinel会将一个slave提升为master。当实例恢复后也以新的master为主
- 通知：Sentinel充当Redis服务端发现来源，当集群发生故障转移时，会将最新信息推送给Redis客户端

![image-20251005164754398](images/image-20251005164754398.png)

Sentinel基于心跳监测服务状态，每隔一秒向集群中的每一个实例发送ping命令：

- 主观下线：如果某sentinel节点发现某实例未在规定时间响应，则认为该实例主观下线

- 客观下线：若超过指定数量(quorom)的sentinel都认为该实例主观下线，则该实例客观下线。quorum值最好超过Sebtinel实例数量的一半

    ![image-20251005174939116](images/image-20251005174939116.png)

    一旦发现master故障，sentinel需要在salve中选择一个作为新的master，选择依据是这样的：

    - 首先会判断slave与master节点断开时间的长短，如果超过指定值(down-after-milliseconds*10)则会排除该salve节点
    - 然后判断slave节点的slave-priority值，越小优先级越高，如果是0则永不参与选举
    - 如果slave-priority一样，则判断slave节点的offset值，越大说明数据越新，优先级越高
    - 最后是判断判断slave节点的运行id大小，越小优先级越高

    当选中了其中一个slave位新的master后(例如slave1)，故障转移的步骤如下：

    - sentinel给备选slave1节点发送slaveof no one命令，让该节点称为master
    - sentinel给其他所有slave发送slaveof IP port  ，让这些slave称为新master的从节点，开始从新的master上同步数据
    - 最后，sentienl将故障节点标记为slave，当故障系欸但恢复后会自动成为新的master的salve节点

##### 搭建哨兵集群
1. 在工作目录，创建目录 

    ```sh
    mkdir s1 s2 s3
    ```

2. 

  ```yaml
  port 27001
  sentinel announce-ip 192.168.150.101
  sentinel monitor mymaster 192.168.150.101 7001 2
  sentinel down-after-milliseconds mymaster 5000
  sentinel failover-timeout mymaster 60000
  dir"/tmp/s1
  ```

sentinel.conf

port：是当前的端口

sentinel monitor mymaster 192.168.150.101 7001 2：指主节点的信息

- mymaster:主节点名称，自定义，随便写
- IP Port：主节点的ip和端口
- 2：选举master时的quonum值

3. 拷贝配置文件到每个目录
    将redis.conf文件拷贝到三个目录中(/tmp目录下)

    ```sh
    echo s2 s3  |xargs -t -n 1 cp s1/sentinel.conf
    ```

4. 修改每个文件夹内的端口

    ```sh
    sed -i -e 's/27001/27002/g' -e 's/s1/s2/g' 27002/sentinel.conf
    sed -i -e 's/27001/27003/g' -e 's/s1/s2/g' 27003/sentinel.conf
    ```

##### RedisTemplate的哨兵模式

在Sentinel集群监管下的Redis主从集群，其节点会因为自动故障转移而发生变化，Redis客户端必须感知这种变化，即使连接信息，Spring的RedisTemplate底层一样lettuce实现了节点的感知与自动切换

1. 在pom文件中引入redis的starter依赖

    ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-redis</artifactId>
    </dependency>
    ```

2. 然后再配置文件application.yml中指定sentinel相关信息

    ```spring
    spring:
        redis:
            sentinel:
                master：mymaster # 指定master名称
                nodes：#指定redis-sentinel集群信息
                -192.168.150.101:27001
                -192.168.150.101:27002
                -192.168.150.101:27003
    ```

3. 配置主从读写分离

    ```java
    @Bean
    public LettuceClientConfigurationBuilderCustomizer configurationBuilderCustomizer(){
        return configBuilder -> configBuilder.readFrom(ReadFrom.REPLICA_PREFERRED) ;
    }
    ```

    这里的ReadFrom是配置Redis的读取策略，是一个枚举，包括以下选择：

    - MASTER：从主节点读取
    - MASTER_PREFERRED：优先从master节点读取，master不可用才读取replica
    - REPLICA：从salve(replica)节点读取
    - REPLICA_PREFERRED：优先从slave(replica)系欸但读取，所有的slave都不可哦那个才读取master

#### Redis分片集群

##### 搭建分片集群

主从和哨兵可以解决高可用、高并发的读的问题，但是依然有两个问题没有解决：

- 海量数据的存储问题
- 高并发写的问题

使用分片集群可以解决上述的问题，分片集群的特征：

- 集群中有多个master，每个master保存不同的数据
- 每个master都可以有多个slave节点
- master之间可以通过ping监测彼此监控状态
- 客户端请求可以访问集群任意节点，最终都会被转发到正确节点

![image-20251005200520154](images/image-20251005200520154.png)



1. 在工作目录，创建目录 

    ```sh
    mkdir 7001 7002 7003 7004 7005 7006
    ```

2. 更改配置文件redis.conf
   
    ```yaml
    port 6379
    #开启集群功能
    cluster-enabled yes
    #集群的配置文件名称，不需要我们创建，由redis自已维护
    cluster-config-file/tmp/6379/nodes.conf
    #节点心跳失败的超时时间
    cluster-node-timeout 5000
    #持久化文件存放目录
    dir/tmp/6379
    #绑定地址
    bind0.0.0.0
    #让redis后台运行
    daemonize yes
    #注册的实例p
    replica-announce-ip 192.168.150.101
    #保护模式
    protected-mode no
    #数据库数量
    databases 1
    #日志
    logfile /tmp/6379/run.log
    ```
    
3. 启动

    ```sh
    #进入/tmp目录
    cd/tmp
    #修改配置文件
    printf '%s\n' 7001 7002 7003 8001 8002 8003 | xargs -I{} -t sed -i 's/6379/{}/g'
    ```

    关闭所有进程

    ```shell
    ps -ef|grep redis| awk'{print $2}'|xargs kill
    ```

    或者

    ```sh
    printf'%s\n'7001 7002 7003 8001 8002 8003|xargs -I{} -t redis-cli -p {} shutdown
    ```

    

5. 创建集群
    我们使用的是Redis6.2.4版本，集群管理集成到了redis-cli中

    ```sh
    redis-cli --cluster create --cluster-replicas 1192.168.150.101:7001
    192.168.150.101:7002 192.168.150.101:7003 192.168.150.101:8001 192.168.150.101:8002
    192.168.150.101:8003
    ```
    
    - redis-cli --cluster 代表集群操作命令
    - create 代表是创建集群
    - --replicas 1：指定集群中每个master副本个数为1，此时节点总数/(replicas+1)得到的就是master的数量。因此节点列表中的前n个就是master，其他节点都是slave系欸但那，随机分配到不同的master
    
    ```sh
    redis -cli -p 7001 cluster nodes
    ```
    
    查看集群状态

##### 散列插槽

Redis会把每一个Master节点映射到0~16383共16384个插槽(hash slot)上慢查询集群信息是就能看到
![image-20251005202728414](images/image-20251005202728414.png)

- key中包含"{}"，且"{}"至少包含1个字符，"{}"中的部分是有效部分
- key中不包含"{}",整个key都是有效部分

例如：key是num，那么根据num计算，如果是{itcast}num，则根据itcast计算。计算方式是利用CRC16算法得到一个hash值，然后对16384取余，得到的结果就是slot值   

![image-20251005202919212](images/image-20251005202919212.png)

同一类数据保存在同一个redis实例

将一类数据使用相同有效部分例如key都已{typeld}为前缀

##### 集群伸缩

Redis-cli --cluster提供了很多操作集群的命令，可以通过help查看

添加节点命令：

```sh
add-node 	new_host:new_port existing_host:existing_port
```

##### 故障转移

当集群中有一个master主机宕机后会发生

1. 首先是该实例与其他实例失去连接
2. 然后是疑似宕机
3. 最后是确定下线，自动提升一个slave作为一个新的master

利用cluster failover命令可以手动让集群中的某个master宕机，切换到执行cluster failover命令的这个slave节点，实现无感知的数据迁移。其流程如下：

手动的Failover支持三种不同的模式

- 缺省：默认流程，如图1~6步
- force：省略了对offset的一致性检验
- takeover：直接执行第五步，忽略数据一致性、忽略master状态和其他master的意见

![image-20251005210645919](images/image-20251005210645919.png)

##### RedisTemplate访问分片集群

RedisTemplate底层同样基于lecttuce实现了分片集群的支持，而是用的步骤与哨兵模式基本一致：

1. 引入redis的starter依赖
2. 配置分片集群地址
3. 配置读写分离

与哨兵模式相比，其中只有分片集群的配置方式略有差异，如下：

```spring
spring:
    redis:
        cluster:
            nodes：#指定分片集群的每一个节点信息
                - 192.168.150.101:7001
                - 192.168.150.101:7002
                - 192.168.150.101:7003
                - 192.168.150.101:8001
                - 192.168.150.101:8002
                - 192.168.150.101:8003
```



### 多级缓存

传统的缓存策略一般是请求到达Tomcat后，先查询Redis，如果未命中则查询数据库，存在下面的问题

- 请求要经过Tomcat处理，Tomcat的性能会成为整个系统瓶颈
- Redis缓存失效时，会对数据库产生冲击

![image-20251006110008251](images/image-20251006110008251.png)

多级缓存就是充分利用请求的每个环节，分别添加缓存，减去tomcat压力，提升服务性能

用作缓存的是业务Nginx，需要部署为集群，再用专门的Nginx作反向代理

![image-20251006110552659](images/image-20251006110552659.png)

#### JVM进程缓存

#####  导入商品案例

1. 安装Mysql

    1. 准备目录
        准本两个目录，用来该镇在容器数据和配置文件目录

        ```shell
        #进入/tmp目录
        cd/tmp
        #创建文件夹
        mkdir mysql
        #进入mysql目录
        cd mysql
        ```

    2. 运行命令

        ```shell
        docker run\
        -p 3306:3306\
        -name mysql\
        -v $PWD/conf:/etc/mysql/conf.d\
        -v $PWD/logs:/logs\
        -v $PWD/data:/var/lib/mysql\
        -e MYSQL_R00T_PASSWORD=123\
        --privileged\
        -d\
        mysql:5.7.25
        ```

    3. 修改配置文件
        /tmp/mysql/conf目录添加一个my.cnf文件，作为MySQL的配置文件

        ```shell
        #创建文件
        touch/tmp/mysql/conf/my.cnf
        ```

        文件内容如下

        ```ini
        [mysqld]
        skip-name-resolve
        character_set_server=utf8
        datadir=/var/lib/mysql
        server-id=1000
        ```

    4. 重启
        配置修改后必须重启容器

        ```shell
        docker restart mysql
        ```

    5. 导入sql，将sql文件拖入sql远程连接客户端

2. 运行Nginx服务

    1. 将Nginx拷贝到一个非中文目录下，运行这个nginx服务

        ```shell
        start nginx.exe
        ```

    2. 配置Nginx集群
        ![image-20251006135651870](images/image-20251006135651870.png)

    

##### 初识Caffine

缓存在日常开发中起到至关重要的作用，由于是存储在内存中，数据的读取速度是非常快的，能大量减少对数据库的访问，减少数据库的压力，我们把缓存分为两类：

- 分布式缓存，例如Redis：
    - 优点：存储容量更大，可靠性更好、可以在集群件共享
    - 缺点：访问缓存有网络开销
    - 场景：缓存数据量较大，可靠性要求较高、需要在集群间共享
- 进程本地缓存：例如HashMap、GuavaCache
    - 优点：读取本地内存，没有网络开销，速度更快
    - 缺点：存储容量有限、可靠性较低、无法共享
    - 场景：性能要求较高，缓存数据量较小

Caffine是一个基于java8开发的，提供了近乎高性能的本地缓存库，目前Spring内部的缓存使用的就是Caffine。
![image-20251006141151134](images/image-20251006141151134.png)

测试

```java
@Test
void testBasicOps(） {
    //创建缓存对象
    Cache<String, String> cache = Caffeine.newBuilder().build();
    //存数据
    cache.put("gf"，"迪丽热巴"）;
    //取数据，不存在则返回null
    String gf = cache.getIfPresent("gf");
    System.out.println("gf = " + gf);
    //取数据，不存在则去数据库查询
    String defaultGF = cache.get("defaultGF", key -> {
    //这里可以去数据库根据key查询value
    return"柳岩";
    });
System.out.println("defaultGF = " + defaultGF);
}
```

Caffine提供了三种缓存驱逐策略：

- 基于容量：设置缓存的数量上限

    ```java
    //创建缓存对象
    Cache<String,String> cache = Caffie.newBuilder()
        .maximumSize(1) //设置缓存大小上限为1
        .build();
    ```

- 基于时间：设置缓存的有效时间

    ```java
    //创建缓存对象
    Cache<String,String> cache = Caffine.newBuilder().
        expireAfterWrite(Duration.ofSeconds(10)) //设置缓存有效期为10秒。总最后一次写入开始计时
        .build();
    ```

- 基于引用：设置缓存为软引用或弱引用时，利用GC来回收缓存数据。性能较差，不建议使用

在默认情况下，当一个缓存元素过期时候，Caffine不会自动立即将其清理和驱逐，而是在一次读或写的操作后，或者在空闲时间完成对失效元素的驱逐

##### 实现进程缓存

利用Caffine实现下列请求：

- 根据id查询商品的业务添加缓存，缓存未命中时查询数据库
- 给根据id查询商品库存的业务添加缓存，缓存未命中时查询数据库
- 缓存的初始大小为100
- 缓存上限为10000

#### Lua语法入门

##### 初始Lua

Lua是一种轻量小巧的脚本语言，用标准C语言编写并且源代码形式开发，其设计的目的时为了嵌入应用程序中，从而为应用程序提供灵活的拓展和定制功能(https://www/lua.org/)
![image-20251006143107681](images/image-20251006143107681.png)

###### hello world

1. 在linux虚拟机任意目录下，新建一个hello.lua文件

    ```shell
    touch hello.lua
    ```

2. 添加下面的内容

    ```lua
    print("Hello World")
    ```

3. 运行

    ```shell
    lua hello.lua
    ```

##### 变量与循环

###### 数据类型

| 数据类型 | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| nil      | 这个嘴贱但，只有值nil属于该类，表示一个无效值                |
| boolean  | 包含两个值：false和true                                      |
| number   | 表示双精度类型的实浮点数                                     |
| string   | 字符串由一对双引号或单引号来表示                             |
| function | 由C或Lua编写的函数                                           |
| table    | Lua表中(table)其实是一个"关联数组"(associative arrays),数组的索引可以是数字、字符串或表类型。在Lua里，table的创建时通过"构造表达式"来完成的，最简单构造表达式{}，用来创建一个空表 |

可以使用type函数测试给定变量或者值的类型

```lua
type("Hello World")
```

lua声明变量的时候，不需要指定数据类型

```lua
--声明字符串
local str = 'hello'
--声明数字
local num = 21
--声明布尔类型
local flag = true
--声明数组key为索引的table
local arr = {'java', 'python','lua'}
--声明table，类似java的map
local map ={name='Jack', age=21}
```

访问table

```lua
--访问数组，lua数组的角标从1开始
print(arr[1])
--访问table
print(map['name'])
print(map.name)
```

###### 循环

数组、table都可以利用for循环来遍历

- 遍历数组

    ```lua
    --声明数组key为索引的table
    local arr = {'java', 'python', 'lua'}
    --遍历数组
    for inde,value in ipairs(arr) do
    	print(index, value)
    end
    ```

- 遍历table

    ```lua
    --声明map，也就是table
    local map = {name='Jack', age=21}
    --遍历table
    for key,value in pairs(map) do
    print(key, value)
    end
    ```

##### 条件控制、函数

###### 函数

定义函数的语法：

```lua
function 函数名( argumentl，argument2..·，argumentn)
	--函数体
	return 返回值
end
```

例如，定义一个函数，用来打印数组

```lua
function printArr(arr)
	for index, value n ipairs(arr) do
		print(value)
	end
end
```

###### 条件控制

类似java中的条件控制，例如if，else语法

```lua
if(布尔表达式)
then
	--[布尔表达式为true时执行该语句块--]
else
	--[布尔表达式为false时执行该语句块--］
end
```

与Java不同，布尔表达式中的逻辑运算是基于英文单词

| 操作符 | 描述                                                         | 实例                  |
| ------ | ------------------------------------------------------------ | --------------------- |
| and    | 逻辑与操作符。若A为false，则返回A，否则返回B                 | (A and B)为 false     |
| or     | 逻辑或操作符。若A为true，则返回A，否则返回B                  | (A or B)为true        |
| not    | 逻辑非操作符。与逻辑运算结果相反，如果条件为 true，逻辑非为 false | not (A and B) 为 true |

#### 实现多级缓存

##### 安装OpenResty

OpenResty是一个基于Nginx的高性能web平台，用于方便的搭建能够处理超高并发、拓展性极高的动态web应用、Web服务和动态网关。具备以下特点：

- 具备Nginx的完整功能
- 基于Lua语言进行拓展，集成了大量精良的Lua库，第三方模块
- 允许使用Lua自定义业务逻辑、自定义库

官方网站：https://openresty.org/cn/

1. 安装

    1. 安装开发库
        首先安装PoenResty的依赖开发库，执行命令：

        ```shell
        yum install -y pcre-devel openssl-devel gcc --skip-broken
        ```

    2. 安装OpenResty仓库
        添加openresty仓库，便于未来安装或更新我们的软件包，通过(yum check-update)

        ```shell
        yum-config-manager--add-repo https://openresty.org/package/centos/openresty.repo
        ```

        如果命令不存在，则运行：

        ```shell
        yum install -y yum-utils
        ```

        然后重复上述命令

    3. 安装OpenResty

        ```shell
        yum install -y openresty
        ```

    4. 安装opm工具
        opm是OpenResty的一个管理工具，可以帮助我们安装一个第三方的Lua模块
        如果你想安装命令行工具opm，那么可以向下面这样安装openresty-opm包：

        ```shell
        yum -install -y openresty-opm
        ```

    5. 目录结构
        默认情况下，OpenResty安装的目录是:/usr/local/openresty

        Openresty就是在Nginx基础上集成了一些lua模块

    6. 配置nginx的环境变量
        打开配置文件

        ```shell
        vi/etc/profile
        ```

        在最下面加入两行：

        ```shell
        export NGINX_HOME=/usr/local/openresty/nginx
        export PATH=${NGINX_HOME}/sbin:$PATH
        ```

        NGINX_HOME:后面是OpenResty安装目录下的nginx目录

        然后让配置生效

        ```shell
        source /etc/profile
        ```

2. 启动和运行
    OpenResty底层是基于Nginx的，查看OpenResty目录的Nginx目录，结构与Windows中安装的nginx基本一致

    ```shell
    #启动nginx
    nginx
    #重新加载配置
    nginx -s reload
    #停止
    nginx -s stop
    ```

3. nginx的默认配置文件注释太多，影响我们后续编辑，这里将nginx.conf中的注释部分删除，保留有效部分
    修改/usr/local/openresty/nginx/conf/nginx.conf文件

##### OpenResty快速入门

 需求：

![image-20251006152501147](images/image-20251006152501147.png)

1. 修改niginx.conf文件

    1. 在nginx.conf的http下，添加对OpenResty的lua模块的加载

        ```yaml
        #加载lua模块
        lua_package_path "/usr/local/openresty/lualib/?.lua;;";
        #加载c模块
        lua_package_cpath "/usr/local/openresty/lualib/?.so;;";
        ```

    2. 在nginx.conf的server下面，添加对/api/item这个路径监听：

        ```yaml
        location /api/item_{
            #响应类型，这里返回json
            default_type application/json;
            #响应数据由Lua/item.Lua这个文件来决定
            content_by_lua_file lua/item.lua;
        }
        ```
    
2. 编写item.lua文件
   
   1. 在nignx目录下创建文件夹 lua
   
       ```shell
       mkdir lua
       ```
   
   2. 在lua文件夹下，新建文件：item.lua
   
       ```shell
       touch lua/item.lua
       ```
   
   3. 内容如下：
   
       ```lua
       --返回假数据，这里的ngx.say（）函数，就是写数据到Response中
       ngx.Say('{"id":10001,"name":"SALSA AIR}')
       ```
   
   4. 重新加载配置
   
       ```shell
       nginx -s reload
       ```

##### 请求参数处理

OpenResty提供了各种API获取不同类型的请求参数

| 参数格式     | 参数示例    | 参数解析代码示例                                             |
| ------------ | ----------- | ------------------------------------------------------------ |
| 路径占位符   | /item/1001  | #1.正则表达式匹配：<br/>location ~ /item/(\d+) {<br />content_by_lua_file lua/item.lua;<br />}<br />--2.匹配到的参数会存入ngx.var数组中，<br />--可以用角标获取<br/>local id = ngx.var[1] |
| 请求头       | id:1001     | --获取请求头，返回值是table类型<br/>local headers = ngx.req.get_headers() |
| Get请求参数  | ?id=1001    | --获取GET请求参数，返回值是table类型<br/>local getParams = ngx.req.get_uri_args() |
| Post表单参数 | id=1001     | --读取请求体<br/>ngx.req.read_body()<br/>--获取POST表单参数，返回值是table类型<br/>local postParams = ngx.req.get_post_args() |
| JSON参数     | {"id":1001} | --读取请求体<br/>ngx.req.read_body()<br/>--获取body中的json参数，返回值是string类型<br/>local jsonBody = ngx.req.get_body_data() |

获取商品请求的路径信息，拼接到json结果后返回

![image-20251006154920818](images/image-20251006154920818.png)	

需求：在OpenResty中接受这个请求，并获取路径的id信息，拼接到结果的json字符串中返回

##### 查询Tomcat

获取请求路径中的id信息，根据id向Tomcat查询商品信息

这里要修改item.lua，满足下面的需求

1. 获取请求参数的id
2. 根据id向Tomcat服务发送请求，查询商品信息
3. 根据id向Tomcat服务发送请求，查询库存信息
4. 组装商品信息、库存信息、序列化为JSON格式并返回

###### nginx内部发送Http请求

nginx提供了内部API用以发送http请求：

```lua
local resp = ngx.location.capture("/path",{
    method = ngx.HTTP_GET,	--请求方式
    args = {a=i,b=2},	--get方式传参数
    body = "c=3&d=4" -- post方式传参数
})
```

反回的响应内容包括：

- resp.status:响应状态码

- resp.header：响应头，是一个table

- resp.body:响应体，就是响应数据

    

注意：这里的path是路径，并不包含IP和端口，这个请求会被nginx内部的server监听并处理。但是我们希望这个请求发送到Tomcat服务器，所以还需要编写一个server来对这个路径做反向代理

```yaml
location &path {
    #这里是windows电脑的ip和Java服务端口，需要确保windows防火墙处于关闭状态
    proxy_pass http://192.168.150.1:8081;
}
```

封装http查询的函数

我们可以把http查询的请求封装为一个函数，放到OpenResty函数库中，方便后期使用

1. 在/usr/local/openresty/lualib目录下创建common.lua文件：

    ```shell
    vi /usr/local/openresty/lualib/common.lua
    ```

2. 在common.lua中封装http函数

    ```lua
    --封装函数，发送http请求，并解析响应
    local function read_http(path, params)
        local resp = ngx.location.capture(path,{
            method = ngx.HTTP_GET,
            args = params,
        })
        if not resp then
        	--记录错误信息，返回404
            ngx.log(ngx.ERR, "http not found, path: ", path ,", args: ", args)
            ngx.exit(404)
    	end
    	return resp.body
    end
    --将方法导出
    local _M = {	
    	read_http = read_http
    }
    return M
    ```

    ```lua
    --导入common函数库
    local common = require('common')
    local read_http = common.read_http
    --导入cjson库
    local cjson = require('cjson')
    
    --获取路径参数
    local id = ngx.var[1]
    
    --查询商品信息
    local itemJSON=read_http("/item/"..id,nil)
    --查询库存信息
    local stockJsoN = read_http("/item/stock/".. id,nil)
    
    --JSON转化为lua的table
    local item = cjson.decode(itemJSON)
    local stock = cjson.decode(stockJsoN)
    --组合数据
    item.stock =stock.stock
    item.sold = stock.sold
    
    --把item序列化为json返回结果
    ngx.say(cjson.encode(item))
    ```

JSON结果的处理

OpenResty提供了一个cjson的模块用来处理JSON的序列化和反序列化
官方地址：http://github.com/openresty/lua-cjson/

- 引入cjson模块：

  ```lua
  local cjson = require "cjson"
  ```
  
- 序列化
  
  ```lua
  local obj = {
      name = 'jack',
      age=21
  }
  local json = cjson.encode(obj)
  ```
  
- 反序列化
  
  ```lua
  /local json = '{"name": "jack", "age": 21}'
  --反序列化
  local obj = cjson.decode(json) ;
  print(obj.name)
  ```
  

负载均衡

![image-20251006162855307](images/image-20251006162855307.png)

```yaml
#反向代理配置,将item路径的请求代理到tomcat集群
location /item {
	proxy_pass http://tomcat-cluster;
}

#tomcat集群配置

upstream tomcat-cluster{
	
	server 192.168.150.1:8081;
	server 192.168.150.1:8082;
}
```

##### Redis缓存预热

冷启动与缓存预热

冷启动:服务刚刚启动时,Redis中并没有缓存,如果所有商品数据都在第一次查询时添加缓存,可能会给数据库代理较大压力

缓存预热:在实际开发中,我们可以利用大数据统计用户访问的热点数据,在项目启动时将这些热点数据提前查询并保存在Redis

我们的数据量较少,可以将所有数据都放入缓存中

###### 缓存预热

1. 利用docker安装Redis

    ```shell
    docker run --name redis -p 6379:6379 -d redis redis-serverr --appendonly yes
    ```

2. 在item-service服务中引入Redis依赖

    ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-redis</artifactId>
    </dependency>
    ```

3. 配置Redis地址

    ```yaml
    spring:
    	redis:
    		host: 192.168.150.101
    ```

4. 编写初始化类

    ```java
    @Component
    public class RedisHandler implements InitializingBean {
        @Autowired
        private StringRedisTemplate redisTemplate;
        @override
        public void afterPropertiesSet(） throws Exception {// 初始化缓存...}
    }
    ```

测试

```java
@Component
public class RedisHandler implements InitializingBean {
    @Autowired
    private StringRedisTemplate redisTemplate;
    @Autowired
    private IItemService itemService;
    @Autowired
    private IItemStockService stockservice;
    private static final ObjectMapper MAPPER = new ObjectMapper();
    @override
    public void afterPropertiesSet() throws Exception{
    //初始化缓存
    // 1.查询商品信息
    List<Item> itemList = itemService.list();
    //2.放入缓存
    for (Item item : itemList) {
        //2.1.item序列化为JsoN
        String json = MAPPER.writeValueAsString(item);
        //2.2.存入redis
        redisTemplate.opsForValue().set("item:id:" + item.getId(), json) ;
    }
    //3.查询商品库存信息
    List<ItemStock> stockList = stockService.list();
    //4.放入缓存
    for (ItemStock stock : stockList) {
        //2.1.item序列化为JsoN
        String json = MAPPER.writeValueAsString(stock);
        //2.2存入redis
        redisTemplate.opsForValue().set("item:stock:id:" + stock.getId(),json);
    }
```



##### 查询Redis缓存

需求:

- 修改item.lua,封装一个函数read_data,实现先查询Redis,如果未命中,再查询Tomcat
- 修改item.lua查询商品和库存数都调用read_data这个函数

```lua
--封装函数，先查询redis，再查询http
local function read_data(key, path, params)
    --查询redis
    local resp = read_redis("127.0.0.1", 6379, key)
    --判断redis是否命中R
    if not resp then
    	--Redis查询失败，查询http
    	resp = read_http(path, params)
    end
    return resp
end
```

###### OpenResty的Redis模块

OpenResty提供了操作Redis模块,我们只要引用该模块就可以直接使用:

- 引入Redis模块,并初始化Redis对象

    ```lua
    --引入redis模块
    local redis = require("resty.redis")
    --初始化Redis对象
    local red = redis:new()
    --设置Redis超时时间
    red:set_timeouts(1000, 1000, 1000)
    ```

- 封装函数,用来释放Redis连接,其实是放入连接池

    ```lua
    --关闭redis连接的工具方法，其实是放入连接池
    local function close_redis(red)
        local pool_max_idle_time = 10000--连接的空闲时间，单位是毫秒
        local pool_size=100--连接池大小
        local ok, err = red:set_keepalive(pool_max_idle_time, pool_size)
    	if not ok then
    		ngx.log(ngx.ERR，"放入Redis连接池失败："，err)
    	end
    end
    ```

- 封装函数,从Redis中读数据返回

    ```lua
    --查询redis的方法ip和port是redis地址，key是查询的key
    local function read_redis(ip, port, key)
        --获取一个连接
        local ok, err = red:connect(ip, port)
        if not ok then
            ngx.log(ngx.ERR，"连接redis失败："，err)
            return nil
        end
        --查询redis
        local resp, err = red:get(key)
        --查询失败处理
        if not resp then
        	ngx.log(ngx.ERR，"查询Redis失败："，err，"，key ="，key)
        end
        --得到的数据为空处理
        if resp == ngx.null then
        	resp = nil
        	ngx.log(ngx.ERR，"查询Redis数据为空，key="，key)
        end
        close_redis(red)
        return resp
    end
    ```

##### Nginx本地缓存

OpenResty为Nginx提供了shard dict的功能,可以在多个nginx的多个worker之间共享数据,实现缓存共享功能

- 开启共享词典,再nginx.conf的http下添加配置

    ```yaml
    #共享字典，也就是本地缓存，名称叫做：item_cache，大小150m
    lua_shared_dict item_cache 150m;
    ```

- 操作共享字典

    ```lua
    --获取本地缓存对象
    local item_cache = ngx.shared.item_cache
    --存储，指定key、value、过期时间，单位s，默认为o代表永不过期
    item_cache:set('key'， 'value'， 1000)
    --读取
    local val = item_cache:get('key')
    ```

查询商品时,优先查询OpenResty的本地缓存

需求:

- 修改item.lua中的read_data函数,优先查询本地缓存,未命中时再查询Redis、Tomcat
- 查询Redis或Tomcat成功后，将数据写入本地缓存，并设置有效期
- 商品基本信息，有效期30分钟
- 库存信息,有效期一分钟

修改后的查询逻辑:

```lua
--封装函数，先查询本地缓存，再查询redis，再查询http
local function read_data(key, expire, path, params)
    --读取本地缓存
    local val = item_cache:get(key)
    if not val then
        --缓存未命中，记录日志
        ngx.log(ngx.ERR，"本地缓存查询失败，key："，key，"，尝试redis查询")
        --查询redis
        val = read_redis("127.0.0.1", 6379, key)
        --判断redis是否命中
        if not val then
        	ngx.log(ngx.ERR，"Redis缓存查询失败，key："，key，"，尝试http查询")-Redis查询失败，查询http
        	edis查询失败，查询http
            val = read_http(path, params)
        	end
        end
        --写入本地缓存
        item_cache:set(key, val, expire)
        return val
end
--根据id查询商品
local itemJsoN = read_data('item:id:'.. id, 1800,"/item/"..id,nil)
--根据id查询商品库存
local itemStockJsONread = read_data('item:stock:id' .. id, 60 ,"/item/stock" .. id ,nil)
```



#### 缓存同步

##### 缓存同步策略

缓存数据同步的方式常见有三种

- 设置有效期：给缓存设置有效期，到期后自动删除。再次查询时更新

    - 优势：简单、方便
    - 缺点：时效性差，缓存过期前可能不一致
    - 场景：更新频率较低，时效性要求低的业务

- 同步双写：在修改数据库的同时，直接修改缓存

    - 优势：时效性强，缓存与数据库强一致
    - 缺点：有代码侵入，耦合度高
    - 场景：对一致性、时效性要求较高的缓存数据

- 异步通知：修改数据库时发送时间通知，相关服务监听到通知后修改数据

    - 优点：低耦合，可以同时通知多个缓存业务
    - 缺点：时效性一半，可能存在中间不一致的状态
    - 场景：时效性要求一半，有多个服务需要同步

    基于MQ的异步通知

    ![image-20251006171450042](images/image-20251006171450042.png)

    基于Cancal的异步通知
    ![image-20251006171520832](images/image-20251006171520832.png)

##### 安装Canal

Cancal，意为水道/管道/沟渠，cancal是阿里巴巴旗下的一款一款开源项目，基于java开发。基于数据库增量日志解析，提供增量数据订阅&消费.GitHub地址:https://github.com/alibaba/canal

Cancal是基于mysql的主从同步来实现的，MySQL的主从同步的原理如下：

- MySQL master将数据变更写入二进制日志(binary log),其中记录的数据叫做binary log events
- MySQL slave 将master 的 binary log events拷贝到它的中继日志(replay log)
- MySQL slave重放 replay log中的事件，将数据变更反映它自己的数据

![image-20251006172541558](images/image-20251006172541558.png)

Cancal就是把自己伪装成MySQL的一个slave节点，从而监听master的binary log变化。在得到的变化消息通知给Cancal的客户端，进而完成对其他数据库的同步

![image-20251006172730845](images/image-20251006172730845.png)

1. 开启MySQL的主从

    1. 打开mysql容器挂载的日志文件，我在/tmp/mysql/conf目录

        ```shell
        vi /tmp/mysql/conf/mt.cnf
        ```

        添加内容：

        ```yaml
        log-bin=/var/lib/mysql/mysql-bin
        binlog-do-db=heima
        ```

        `log-bin=/var/lib/mysql/mysql-bin`：设置binarylog文件的存放地址和文件名，叫做mysql-bin
        `binlog-do-db=heima`：指定对哪个database记录binary log events，这里记录heima这个库

        最终效果

        ```mysql
        [mysqld]
        skip-name-resolve
        character_set_server=utf8
        datadir=/var/lib/mysql
        server-id=1000
        log-bin=/var/lib/mysqlfmysql-bin
        binlog-do-db=heima
        ```

    2. 设置用户权限
        接下来添加一个仅用于数据同步的账户，处于安全考虑，仅提供对heima这个库的操作权限

        ```mysql
        create user cancal @'%' IDENTIFIED by 'cancal';
        GRANT SELECT,REPLICATION SLAVE,REPLICATION CLIENT,SUPER ON *.* TO'canaL'@'%' identified by 'canal';
        FLUSH PRIVILEGES;
        ```

        重启mysql容器即可

        ```sh
        docker restart mysql
        ```

        测试是否成功

        ```mysql
        show master status;
        ```

2. 安装Cancal

    1. 创建网络
        我们需要创建一个网络将MySQL，Cancal，MQ放到同一个Docker网络：

        ```sh
        docker network create heima
        ```

        让mysql加入这个网络

        ```sh
        docker network connect heima mysql
        ```

    2. 安装Cancal

        将镜像上传到压缩机，通过命令导入

        ```sh
        docker load -i canal.tar
        ```

        然后通过命令创建Canal容器

        ```sh
        docker run -p 11111:11111--name canal\
        -edanal.destinations=heima\
        -e canal.instance.master.address=mysql:3306
        -e canal.instance.dbusername=canal
        -e canal.instance.dbPassword=canal
        -e canal.instance.connectionCharset=UTF-8\
        -e canal.instance.tsdb.enable=true\
        -e canal.instance.gtidon=false
        -e canal.instance.filter.regex=heima\\..*\
        --network heima\
        -d canal/canal-server:vl.1.5
        ```

        说明：

        `-p11111:11111`：这是canal的默认监听端口
        `-e canal.instance.master.address=mysql:3306`：数据库地址和端口，如果不知道mysql容器地
        址，可以通过过dockerinspect容器id来查看
        `-e canal.instance.dbUsername=canal`：数据库用户名
        `-ecanal.instance.dbPassword=canal`：数据库密码
        `-ecanal.instance.filter.regex=`：要监听的表名称
        表名称监听支持的语法：

        ```
        mysql数据解析关注的表，PerL正则表达式.
        多个正则之间以逗号（，)分隔，转义符需要双斜杠（\1)
        常见例子：
        1.所有表：.*or11..*
        2.canalschema下所有表：canal\1..*
        3.canal下的以canal打头的表：canal\\.canal.*
        4.canalschema下的—张表：canal.test1
        多个规则组合使用然后以逗号隔开：canal\\..*，mysql.testl，mysql.test2
        ```

##### 监听Canal

Canal提供了各种语言的客户端，当Canal监听到binlog变化时，会通知Canal的客户端

![image-20251006174832421](images/image-20251006174832421.png)

Canal提供了各种语言的客户端，当Canal监听到binlog变化时，会通知Canal的客户端，不过这里我们回使用GitHub上的第三方开源的canal-starter。地址：https://github.com/NormanGyllenhaal/cancal-cilent

引入依赖：

```xml
<!--canal-->
<dependency>
    <groupId>top.javatool</groupId>
    <version>1.2.1-RELEASE</version>
    <artifactId>canal-spring-boot-starter</artifactId>
</dependency>
```

编写配置：

```yaml
canal:
    destination：heima #canal实例名称，要跟canal-server运行时设置的destination一致
    server: 192.168.150.101:11111 # canal地址
```

编写监听器，监听canal消息

![image-20251006174758222](images/image-20251006174758222.png)

Canal推送给canal-client的是被修改的这一行数据(row)，而我们引入的cancal-cilent则会帮我们把行数据封装到

Item实体类中。这个过程中需要直到数据库与实体的映射关系，要用到JPA的几个注解

![image-20251006180717839](images/image-20251006180717839.png)

#### 多级缓存总结

![image-20251006175600739](images/image-20251006175600739.png)

### 最佳实现 

#### Redis的键值设计

##### 优雅的key结构

Redis的key虽然可以自定义，但最好遵循以下的几个最佳实践约定

- 遵循基本格式:[业务名称]:[数据名]:[id]
- 长度不超过44字节
- 不包含特殊字符

例如：我们登录业务，保存用户信息，其key是这样的：

![image-20251007103127849](images/image-20251007103127849.png)

优点：

1. 可读性强
2. 避免key冲突
3. 方便管理
4. 更节省内存：key是String类型，底层编码包括int、embstr和raw三种。embstr在小于44字节使用，采用连续内存空间，内存占用更少

##### 拒绝BigKey

BigKey通常以Key的大小和Key中的成员的数量来综合判定，例如：

- Key本身的数据量较大：一个String类型的Key，它的值为5MB
- Key中的成员数过多：一个ZSET类型的Key，它的成员数量为10000个
- Key中成员的数据量过大：一个Hash类型的Key，它的成员数量虽然只有1000个但这些成员的value(值)总大小为100MB

推荐值：

- 单个key的value小于10KB
- 对于集合类型的key，建议元素数量小于1000

BigKey的危害

- 网络阻塞
    对BigKey执行读请求时，少量的QPS就可能导致内存带宽使用率被占满，导致Redis示例，乃至所在物理机变慢
- 数据倾斜
    BigKey所在的Redis实例内存使用率远超其他实例，无法使数据分片的内存资源达到均衡
- Redis阻塞
    对元素较多的hash、list、zset等做运算时回耗时较旧，使主线程被阻塞
- CPU压力
    对BigKey的数据序列化与反序列化回导致CPU的使用率飙升，影响Redis实例和本机其他应用

发现BigKey

- redis-cli --bigkeys
    利用redis-cli --bigkeys参数，可以遍历分析所有key，并返回Key的整体统计信息与每个数据的Top1的big key
- scan扫描
    自己编程，利用scan扫描Redis中所有的key，利用strlen、hlen等命令判断key的长度(此处不建议使用MEMORY USAGE)
- 第三方工具
    利用第三方工具，如Redis-Rdb-Tools分析RDB快照文件，全面分析内存使用情况
- 网络监控
    自定义工具，监控进出Redis的网络数据，超出预警值时主动告警

BigKey内存占用较多，即便时删除这样的key也需要耗费很长的时间，导致Redis主进程阻塞，引发一系列问题

- Redis3.0及以下的版本
    如果是集合类型，则遍历BigKey的元素，先逐个删除子元素，最后删除BigKey
- Redis4.0以后
    Redis在4.0提供了异步删除的命令：unlink

##### 恰当的数据类型

例1：比如存储一个User对象，我们有三种存储方式

方式一：json字符串

| user:1 | {"name":"Jack","age":21} |
| ------ | ------------------------ |

优点：实现简单粗暴

缺点：数据耦合，不够灵活

方式二：字段打散

| user:1:name | Jack |
| ----------- | ---- |
| user:1:age  | 21   |

优点：可以灵活访问对象任意字段

缺点：占用空间大、没办法做到统一控制

方式三：hash

| user:1 | name | Jack |
| ------ | ---- | ---- |
|        | age  | 21   |

优点：底层使用ziplist，空间占用小，可以灵活访问对象的任意字段

缺点：代码相对复杂

Value的最佳实践：

- 合理拆分数据，拒绝BigKey
- 选择适合数据结构
- Hash结构的entry数量不要超过1000
- 设置合理的超时时间

#### 批处理优化

##### Pipeline

单个命令的执行流程

一次命令的响应时间 = 1次往返的网络传输的耗时+1次Redis执行命令的耗时

![image-20251007110626594](images/image-20251007110626594.png)

N个命令的执行流程

N次命令的响应时间 = N次往返的网络传输的耗时+N次Redis执行命令的耗时

![image-20251007110645062](images/image-20251007110645062.png)

N条命令的响应时间 = 1次往返的网络传输耗时+N次Redis执行命令耗时
![image-20251007110819891](images/image-20251007110819891.png)

###### MSET

Redis提供了很多Mxxx这样的命令，可以实现批量插入数据，例如：

- mset
- hmset

不要在一次批处理中传输太多命令，否则单次命令占用带块过多，会导致网络阻塞

利用mset批量插入10万条数据

```java
@Test
void testMxx(） {
    String[] arr = new String[20o0];
    int j;
    for （int i = 1;i <= 100000; i++）{
        j=（i%1000） 1;
        arr[j] = "test:Key_" + i;
        arr[j + 1] = "value_" i;
        if （j ==）{
            jedis.mset(arr) ;
        }
    }
}
```

###### Pipeline

MSET虽然可以批处理，但是只能操作部分数据类型，因此有对复杂数据类型批处理需要，建议使用Pipeline功能

```java
@Test
void testPipeline() {
    //创建管道
    Pipeline pipeline = jedis.pipelined();
    for （int i= 1; i<= 100000; i++）{
        //放入命令到管道
        pipelineset("test:key_" + i, "value_" + i);
        if （i % 1000 == 0） {
            //每放入1000条命令，批量执行
            pipeline.sync();
        }
    }
}
```

Pipeline的多个命令之间不具备原子性

##### 集群下的批处理

如MSET或pipeline这样的批处理需要在一次请求中携带多条命令，而此时如果Redis是一个集群，那批处理命令的多个key必须落在一个插槽中，否则则会执行失败

|          | 串行命令                      | 串行slot                                                     | 并行slot                                                     | hash_tag                                        |
| -------- | ----------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------------------------------------------- |
| 实现思路 | for循环遍历，一次执行每个命令 | 在客户端执行每个key的slot，将slot一致分为一组，每组都利用Pipeline批处理。<br />串行执行各组命令 | 在客户端计算每个key的slot，将slot一致分为一组，每组都利用Pipeline批处理<br />并行执行各组命令 | 将所有key设置相同的hash_tag,则所有key的slog相同 |
| 耗时     | N次网络耗时+N次命令耗时       | m次网络耗时+N次命令耗时<br />m=key的slot个数                 | 1次网络耗时+N次命令耗时                                      | 1次网络耗时+N次命令耗时                         |
| 优点     | 实现简单                      | 耗时较短                                                     | 耗时非常短                                                   | 耗时非常短，实现简单                            |
| 缺点     | 耗时非常久                    | 实现稍复杂<br />slot越多，耗时越久                           | 实现复杂                                                     | 容易出现数据倾斜                                |

#### 服务端优化

##### 持久化配置

Redis的持久化虽然可以保证数据安全，但也会带来很多额外的开销，因此持久化请遵循以下建议

1. 用来做缓存的Redis实例尽量不要开启持久化机制
2. 建议关闭RDB持久化功能，使用AOF持久化
3. 利用脚本定期在slave节点做RDB，实现数据备份
4. 配置合理的rewrite阈值，避免频繁的bgrewrite
5. 配置no-appendfsync-on-rewrite = yes，禁止在rewrite期间做aof，避免因AOF引起的阻塞

![image-20251007114859294](images/image-20251007114859294.png)

部署有关建议：

1. Redis实例的物理机要预留足够内存，应对fork和rewrite
2. 单个Redis实例内存上限不要太大，例如4G或8G。可以加快fork的速度、减少主从同步，数据迁移压力
3. 不要与CPU密集型应用部署在一起
4. 不要与高硬盘负载应用一起部署，例如：数据库、消息队列

##### 慢查询

慢查询：在Redis执行耗时超过某个阈值的命令，称为慢查询
![image-20251007170912303](images/image-20251007170912303.png)

慢查询的阈值可以通过配置指定：

- slowlog-log-slower-than：慢查询阈值，单位是微秒，默认是10000，建议1000，慢查询会被放入慢查询日志中，日志长度有上限，可以通过配置指定
- slowlog-max-len：慢查询日志(本质是一个队列)的长度。默认是128，建议1000
    修改这两个配置可以使用：config set命令

查看慢查询日志列表：

- slowlog len：查询慢查询日志长度
- slowlog get [n]：读取n条慢查询日志
- slowlog reset：清空慢查询列表

![image-20251007171821976](images/image-20251007171821976.png)

##### 命令及安全配置

Redis回绑定在0.0.0.0:6379,这样就会将Redis服务暴露在公网上，而Redis如果没有做身份认证，会出现严重的安全漏洞

漏洞出现的核心原因有以下几点

- Redis未设置密码
- 利用了Redis的config set命令动态修改Redis配置
- 使用了Root账号权限启动Redis



为了避免这样的漏洞，这里给出一些建议

1. Redis一定要设置密码
2. 禁止线上使用下面命令:keys、flushfall、flushdb、config set等命令。可以利用rename-command禁用
3. bind：限制网卡，禁止外网访问
4. 开启防火墙
5. 不要使用Root账户启动Redis
6. 尽量不是有默认的端口

##### 内存配置

当Redis内存不足时，可能导致Key频繁被删除、响应时间变长、QPS不稳定。当内存使用率达到90%以上时就需要我们警惕，并快速定位到内存占用的原因

| 内存占用   | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| 数据内存   | 是Redis最主要的部分，存储Redis的键值信息。主要问题是BigKey问题、内存碎片问题 |
| 进程内存   | Redis主进程本身运行肯定需要占用内存，如代码、常量池等等；这部分内存大约几兆，在大多数生产环境中与Redis数据占用的内存相比可以忽略 |
| 缓冲区内存 | 一般包括客户端缓冲区，AOF缓冲区，复制缓冲区等。客户缓冲区有包括输入缓冲区和输出缓冲区两种。这部分内存占用波动较大，不当使用BigKey，可能导致内存溢出 |

Redis提供了一些命令，可以查看Redis目前的内存分配状态

info memory

![image-20251007174801677](images/image-20251007174801677.png)

memory xxx

![image-20251007174840891](images/image-20251007174840891.png)

内存缓冲区常见有三种：

- 复制缓冲区：主从复制repl_backlog_buf，如果太小可能导致频繁全量复制，影响性能。通过repl-backlog-size来设置，默认1mb
- AOF缓冲区：AOF刷盘之前的缓冲区域，AOF执行rewrite缓冲区，无法设置容量上限
- 客户端缓冲区：分为输入缓冲区和输出缓冲区，输入缓冲区最大1G且不能设置。输出缓冲区可以设置

![image-20251007175527980](images/image-20251007175527980.png)

#### 集群最佳实践

在Redis的默认配置种，如果发现任意一个插槽不可用，则整个集群都会停止对外服务

![image-20251007175705906](images/image-20251007175705906.png)

为了保证高可用特性，建议将cluster-require-full-coverage配置为false

集群节点之间回不断的互相Ping来确定集群中其他节点的状态，每次Ping携带的信息包括：

- 插槽信息
- 集群状态信息

集群中的节点越多，集群的状态信息数据量也越大，10个节点相关的信息可能达到1kb，此时每次集群互通需要的带宽会非常高

解决路径：

1. 避免多个打击群，集群节点数不要太多，最好小于1000，如果业务庞大，则建立多个集群
2. 避免在单个物理机中运行太多Redis实例
3. 配置合适的cluster-node-timeout值

集群虽然具备高可用的特性，能实现自动故障恢复，但是如果使用不当，也会存在一些问题

1. 集群完整性问题
2. 集群带宽问题
3. 数据倾斜问题
4. 客户端性能问题
5. 命令的集群兼容性问题
6. lua和事务问题

注意

单体Redis(主从Redis)已经达到万级别的QPS，并且也具备高可用特性。如果主从性能满足业务，尽量不搭建Redis集群



## 原理篇

### 数据结构

#### 动态字符串SDS

我们都知道Redis中保存的Key是字符串，value往往是字符串或者字符串的集合，可见字符串是Redis中最常用的一种的数据结构

不过Redis没有直接使用C语言中的字符串，因为C语言字符串存在很多问题：

- 获取字符串的长度需要计算
- 非二进制安全
- 不可修改

```c
// c语言，声明字符串
char * s = "hello";
//本质是字符数组：{'h','e','l','l','o','\0'}
```

Redis构建了一种新的字符串结构，称为简单动态字符串(Simple Dynamic String)，简称SDS

Redis是C语言实现的，其中SDS是一个结构体，源码如下：

```c
struct __attribute__ ((__packed__)) sdshdr8{
    uint8_t len;//buf已保存的字符串字节数，不包含结束标示
    uint8_t alloc;//buf申请的总字节数，不包含结束标示
    unsigned char flags;//不同SDS的头类型，用来控制SDS的头大小
    char buf[];
};
```

![image-20251009162333562](images/image-20251009162333562.png)

SDS之所以叫做动态字符串，是因为它具备动态扩容的能力

假如我们要给SDS住家一段字符串，这里首先会申请新内存空间

- 如果新字符串小于1M，则新空间为拓展后字符串长度的两倍+1；
- 如果新字符串大于1M，则新空间为扩展后字符串长度+1M+1.称为内存预分配

![image-20251009162949640](images/image-20251009162949640.png)

优点： 

1. 支持动态扩容
2. 减少内存分配次数
3. 二进制安全

#### IntSet

IntSet是Redis中set集合的一种实现方式，基于整数数组，并且具备长度可变、有序等特征

结构如下：

```c
typedef struct intset{
    uint32_t encoding;//编码方式，支持存放16位、32位、64位整数
    uint32_t length;//元素个数
    int8_t contents[];//整数数组，保存集合数据
} intset;
```

其中encoding包含三种模式，标示存储的整数大小不同

```c
/*Note that these encoding are ordered,so:
 *INTSET_ENC_INT16 < INTSET_ENC_INT32 < INTSET */
#define INTSET_ENC_INT16 (sizeof(int16_t)) //2字节整数，范围类似Java的short
#define INTSET_ENC_INT32 (sizeof(int32_t)) //4字节整数，范围类似Java的int
#define INTSET_ENC_INT64 (sizeof(int64_t)) //8字节整数，范围类似java的long
```

为了方便查找，Redis会将intset中所有的整数按照升序依次宝尊在contents数组中

![image-20251009165212428](images/image-20251009165212428.png)

现在，数组中每个数字都在int16_t的范围内，因此采用的编码方式INTSET_ENC_INT16，每部分占用字节大小为：

- encoding：4字节
- length：4字节
- contents：2字节*3 = 6字节

假设有一个intset，元素为{5,10,20}，采用的编码是INTSET_ENC_INT16，则每个整数占两字节：

![image-20251009165731025](images/image-20251009165731025.png)

我们向其中添加一个数字：50000，这个数字超过了int16_t的范围，intset会自动升级编码方式到合适的大小

以当前案例来说流程如下：

1. 升级编码INTSET_ENC_INT32，每个整数占4字节，并按照新的编码方式及元素个数扩容数组
2. 倒序依次将数组中的元素，拷贝到扩容后的正确位置
3. 将待添加的元素放入数组末尾
4. 最后，将intset的encoding属性INTSET_ENC_INT32,将length属性改为4
   
    

![image-20251009170228843](images/image-20251009170228843.png)

源码如下：

```c
intset *intsetAdd(intset *is, int64_t value,uint8_t *success){
    uint8_tvalenc=_intsetValueEncoding(value)；//获取当前值编码
    uint32_t pos；// 要插入的位置
    if (success) *success = 1;
    //判断编码是不是超过了当前intset的编码
    if (valenc > intrev32ifbe(is->encoding)) {
    	//超出编码，需要升级
    	return intsetUpgradeAndAdd(is,value) ;
    }else{
        //在当前intset中查找值与value一样的元素的角标pos
        if (intsetSearch(is,value,&pos)){
            if(success)*success=0;//如果找到了，则无需插入，直接结束并返回失败
            return is;
        }
        //数组扩容	
        is=intsetResize(is,intrev32ifbe(is->length)+1);
        //移动数组中pos之后的元素到pos+1，给新元素腾出空间
        if (pos < intrev32ifbe(is->length)) intsetMoveTail(is,pos,pos+1);
    }
    //插入新元素
    _intsetSet(is,pos,value);
    //重置元素长度
    is->length = intrev32ifbe(intrev32ifbe(is->length)+1);
    return is;
}
```

```c
static intset *intsetUpgradeAndAdd(intset *is, int64_t value) {
    //获取当前intset编码
    uint8_t curenc = intrev32ifbe(is->encoding);
    //获取新编码
    uint8_t newenc =_intsetValueEncoding(value) ;
    //获取元素个数
    int length = intrev32ifbe(is->length);
    //判断新元素是大于0还是小于。，小于0插入队首、大于0插入队尾
    int prepend = value < 0 ? 1 : 0;
    //重置编码为新编码
    is->encoding= intrev32ifbe(newenc);
    //重置数组大小
    is = intsetResize(is,intrev32ifbe(is->length)+1);
    //倒序遍历，逐个搬运元素到新的位置，_intsetGetEncoded按照l旧编码方式查找旧元素
    while(length--)//_intsetSet按照新编码方式插入新元素
    intsetSet(is,length+prepend,_intsetGetEncoded(is,length,curenc));
    /*插入新元素，prepend决定是队首还是队尾*/
    if (prepend)
    	_intsetSet(is,0,value) ;
    else
    	intsetSet(is,intrev32ifbe(is->length) ,value) ;
    //修改数组长度
    is->length = intrev32ifbe(intrev32ifbe(is->length)+1);
    return is;
}
```

Intset可以看作是特殊的整数数组，具备一些特点：

1. Redis会确保Intset中的元素唯一，有序
2. 具备类型升级机制，可以节省内存空间
3. 底层采用二分查找方式来查询

#### Dict

我们知道Redis是一个键值型(key-Value Pair)的数据库，我们可以根据键实现快速的增删改查。而键与值的映射关系正式通过Dict来实现的。

Dict是由三部分组成的，分别是：哈希表(DictHashTable)、哈希节点(DictEntry)、字典(Dict)

```c
typedef struct dictht{
    //entry数组
    //数组中保存的是指向entry的指针
    dictEntry **table;
    //哈希表大小
    unsigned long size;
    //哈希表大小的掩码，总等于size-1
    unsigned long sizemask;
    //entry个数
    unsigned long used;
}dictht;
```

```c
typedef struct dictEntry{
    void *key;
    union {
        void *val;
        uint64_t u64;
        int64_t s64;
        double d;
    } v; 
}dictEntry;
```

![image-20251009175936228](images/image-20251009175936228.png)

```c
typedef struct dict{
    dictType *type;//dict类型，内置不同的hash函数
    void *privdata;//私有数据，在做特殊hash运算时用
    doctht ht[2];//一个Dict包含两个哈希表，其中一个是当时数据，另一个则为空，rehash时用
    long rehashidx;//rehash的进度。-1表示未进行
    int16_t pauserehash;//rehash是否暂停，1则暂停，0则继续
}dict;
```

![image-20251009180943929](images/image-20251009180943929.png)

Dict中的HashTable就是数组集合单向链表的实现，当集合中的元素较多时，必然导致哈希冲突增大，链表过长，则查询效率会大大降低

Dict在每次新增键值对都会检查负载因子(LoadFactor = used/size),满足以下两种情况会触发哈希表扩容：

- 哈希表的LoadFactor>=1，并且服务器没有指向BGSAVE或者BGREWRITEAOF
- 哈希表的LoadFactor>5

```c
static int _dictExpandIfNeeded(dict *d){
    //如果正在rehash，则返回OK
    if(dictIsRehasing(d)) Return DICT_OK;
    //如果哈希表为空，则初始化哈希表为默认大小：4
    if(d->ht[0].size == 0) return dictExpand(d,DICT_HT_INITIAL_SIZE);
    //当负载因子(used/size)达到1以上，并且当前没有进行bgwrite等子进程操作
    //或者负载因子超过5，则进行dictExpand，也就是扩容
    if(d->ht[0].used >= d->ht[0] &&
      (dict_can_resize || d->ht[0].used/d->ht[0].size > dict_force_resize_ratio){
          //扩容大小为used + 1，底层会对扩容大小做判断，实际上兆的时第一个大于等于 used+1 的 2^n
          return dictExpand(d,d->ht[0].used+1);
      }
      return DICT_OK;
}
```

Dict除了扩容以外，每次删除元素时，也会对负载因子做检查，当LoadFactor<0.1时，会做哈希表收缩

```c
//t.hash.c # hashTypeDeleted()
...
if(dictDelete((dict*)o->ptr,field)==C_OK){
    deleted = 1;
    //删除成功后，检查是否需要重置Dict的大小，如果需要则调用dictResize重置
    //Always check if the dictionary needs a resize after a delete
	if(htNeedsResize(o->ptr) dictResize(o->ptr));
}
...
```

```c
//server.c
int htNeedsResize(dict *dict){
    long long size,used;
    //哈希表大小
    size = dictSlots(dict);
    //entry数量
    used = dictSize(dict);
    //size > 4(哈希表初始大小)并且 负载因子低于1
    return (size >DICT_HT_INITIAL_SIZE &&(used*100/size<HASHTABLE_MIN_FILL));
}
```

```c
int dictResize(dict *d){
    unsigend long minial;
    //如果正在做bgsave或在bgrewriteof或rehash，则返回错误
    if(!dict_can_resize || dictIsRehashing(d))
        return DICT_ERR;
    //获取used，也就是entry个数
    minimal = d->ht[0].used;
    //如果used小于4，则重置为4
    if(minimal < DICT_HT_INITIAL_SIZE)
        minimal = DICT_HT_INITIAL_SIZE;
    //重置大小为minimal，其实是第一个大于等于minimal的2^n
    return dictExpand(d,minimal);
}
```



![image-20251009212253457](images/image-20251009212253457.png)

![image-20251009211642278](images/image-20251009211642278.png)

不管是收缩还是扩容，必定会创建新的哈希表，导致哈希表的size和sizemask变化，而key的查询与sizemask有关。因此必须对哈希表种的每一个Key重新计算索引，插入新的哈希表，这个过程称为rehash。过程是这样的

1. 计算新hash表的realeSize，值取决于当前要做的是扩容还是收缩：
    - 如果是扩容，则新size为第一个大于等于dict.ht[0].used+1的$2^n$
    - 如果是收缩，则新size为第一个大于等于dict.ht[0].used的$2^n$
2. 按照新的realeSize申请内存空间，创建dictht，并赋值给dict.ht[1]
3. 设置dict.rehashidx = 0，表示开始开始rehash
4. 将dict.ht[0]中的每一个dictEntry都rehash到dict.ht[1]
5. 将dict.ht[1]]赋值给dict.ht[0],给dict.ht[1]初始化为空哈希表，释放原来的dict.ht[0]的内存

Dict的rehash并不是一次性完成的，如果Dict中包含数百万的entry，要在一次rehash完成，极有可能导致主线程阻塞，因此Dict的rehash是分多次，渐进式的完成，因此称为渐进式的rehash

1. 计算新hash表的realeSize，值取决于当前要做的是扩容还是收缩：
    - 如果是扩容，则新size为第一个大于等于dict.ht[0].used+1的$2^n$
    - 如果是收缩，则新size为第一个大于等于dict.ht[0].used的$2^n$
2. 按照新的realeSize申请内存空间，创建dictht，并赋值给dict.ht[1]
3. 设置dict.rehashidx = 0，表示开始开始rehash
4. 每次执行新增、查询、修改、删除操作时，都检查一下dict.rehashidx是否大于-1，如果是则将dict.ht[0].table[rehashidx]的entry链表rehash到dict.ht[1],并且将rehashidx++。直至dict[0]的所有数据都rehash到dict.ht[1]
5. 将dict.ht[1]]赋值给dict.ht[0],给dict.ht[1]初始化为空哈希表，释放原来的dict.ht[0]的内存
6. 将rehashidx赋值为-1，代表rehash家属
7. 在rehash过程中，新增操作，则直接写入ht[1]、查询、修改、删除则会在dict.ht[0]和dict.ht[1]依次查找并执行。并确保ht[0]的数据只减不增，随着rehash最终为空

Dict的结构

- 类似于Java的hashtable，底层是数组加链表解决哈希冲突
- Dict包含两个哈希表，ht[0]平常用，ht[1]用来rehash

#### ZipList

ZipList是一种特殊的"双端链表"，由一系列特殊的编码的连续内存块组成。可以在任意一端进行压入操作/弹出操作，并且该操作的时间复杂度为O(1)

![image-20251010214211528](images/image-20251010214211528.png)

| 属性    | 类型     | 长度  | 用途                                                         |
| ------- | -------- | ----- | ------------------------------------------------------------ |
| zlbytes | uint32_t | 4字节 | 记录整个压缩列表占用的内存字节数                             |
| zltail  | uint32_t | 4字节 | 记录压缩列表表尾节点距离距离压缩列表的其实地址有多少字节，通过这个偏移量，可以确定表尾节点的地址 |
| zllen   | uint16_t | 2字节 | 记录了压缩列表包含的节点数量。最大值为UINT16_MAX(65534)，如果超过这个值，此处会记录为65535，但节点的真实数量需要遍历整个压缩列表才能计算得出 |
| entry   | 列表节点 | 不定  | 压缩列表包含的各个节点，节点的长度由节点保存的内容决定       |
| zlend   | uint8_t  | 1字节 | 特殊值0xFF(十进制255)，用于标记压缩列表的末尾                |

ZipList中的Entry并不像普通链表那样记录前后节点的指针，因为记录两个指针要占用16个字节，浪费内存。而是采用了以下结构

![image-20251010215018392](images/image-20251010215018392.png)

- previous_entry_length：前一节点的长度，占1个或5个字节
    - 如果前一节点的长度小于254字节，则采用1个字节来保存这个长度值
    - 如果前一节点长度大于254字节，则采用5个字节保存这个长度值 ，第一个字节为0xfe，后四个字节才是真实长度 
- encoding：编码属性，记录content的数据类型(字符串还是整数)以及长度，占用1个、2个或5个字节
- contents：负责保存节点的数据，可以是字符串或整数

ZipList中所有的存储长度的数值均采用采用小端字节序，即低位字节在前，高位字节在后，例如数值0x1234,采用小端字节序后实际存储值为：0x3412

ZipListEntry中的encoding编码分为字符串和整数两种

- 字符串：如果encoding是以"00"、"01"或者"10"开头，则证明content是字符串

    | 编码                                                | 编码长度 | 字符串大小        |
    | --------------------------------------------------- | -------- | ----------------- |
    | \|00pppppp\|                                        | 1bytes   | <= 63bytes        |
    | \|01pppppp\|qqqqqqqq\|                              | 2bytes   | <=16383bytes      |
    | \|1000000\|qqqqqqqq\|rrrrrrrr\|ssssssss\|tttttttt\| | 5bytes   | <=4294967295bytes |

    例如，我们要保存字符串:"ab"和"bc"

    ![image-20251011142011318](images/image-20251011142011318.png)

- 整数，如果encoding是以"11"开始，则证明content是整数，且encoding固定只占用一个字节

    | 编码     | 编码长度 | 整数类型                                               |
    | -------- | -------- | ------------------------------------------------------ |
    | 11000000 | 1        | int16_t(2bytes)                                        |
    | 11010000 | 1        | int32_t(4bytes)                                        |
    | 11100000 | 1        | int64_t(8bytes)                                        |
    | 11110000 | 1        | 24位有符整数(3bytes)                                   |
    | 11111110 | 1        | 8位有符整数(1bytes)                                    |
    | 1111xxxx | 1        | 直接在xxxx位置保存数值，范围从0001~1101，减1后为实际值 |

    例如：一个ZipList中包含两个整数值："2"和"5"

    ![image-20251011142624742](images/image-20251011142624742.png)

##### 连锁更新问题

现在，假设我们有N个连续的、长度为250~253字节之间的entry，因此entry的previous_entry_length属性用1个字节即可表示，如图所示：

![image-20251012142033052](images/image-20251012142033052.png)

ZipList这种特殊情况下产生的连续多此空间拓展操作称之为连锁更新(Cascade Update)。新增、删除都可能导致连锁更新的发生

#### QuickList

ZipList虽然节省内存，但申请内存必须是连续空间，如果内存占用过多，申请内存效率很低，怎么办

为了缓解这个问题，我们必须限制ZipList的长度和entry大小

但是我们要存储大量数据，超出ZipList最佳的上限怎么办

我们可以创建多个ZipList来分片存储数据

数据拆分后比较分散，不方便管理和查找，这多个ZipList如何建立联系

数据拆分后比较分散，不方便管理和查找，多个ZipList如何建立联系

Redis在3.2版本引入了新的数据结构QuickList，他是一个双端链表，只不过链表的每个节点都是一个ZipList

![image-20251012143648713](images/image-20251012143648713.png)

为避免QuickList中的每个ZipList中的entry较多，Redis提供了一个配置项：list-max-ziplist-size来限制

- 如果值为正，则代表ZipList的允许entry个数的最大值

- 如果值为负，则代表ZipList的最大内存大小，分5种情况

    1. -1：每个ZipList不能超过4kb
    2. -2：每个ZipList不能超过8kb
    3. -3：每个ZipList不能超过16kb
    4. -4：每个ZipList不能超过32kb
    5. -5：每个ZipList不能超过64kb

    其默认值为-2

    除了控制ZipList的大小，QuickList还可以对节点的ZipList做压缩，通过配置项list-compress-depth。因为连边都是从首尾访问居多，所以首位是不压缩的。这个参数是控制首尾不压缩的节点个数

    - 0：特殊值，代表不压缩
    - 1：表示QuickList的首尾各有一个节点不压缩，中间节点压缩
    - 2：表示QuickList的首尾各有两个节点不压缩，中间节点压缩
    - 依次类推

    quicklist和QuicklistNode的源码

    ```c
    typedef struct quicklist{
        //头节点指针
        quicklistNode *head;
        //
        quicklistNode *tail;
        //
        unsigned long count;
        //
        unsigned long len;
        //
        int fill ： QL_FILL_BITS;
        //首尾不压缩的节点数量
        unsigned int compress : QL_COMP_BITS;
        //内存重分配时的书签数量及数组，一般用不到
        unsigned int bookmark_count : QL_BM_BITS;
        quicklistBookmark bookmarks[];
    }quicklist;
    ```

    ```c
    typedef struct quicklistNode{
        //前一个节点指针
        struct quicklistNode *prev;
        //下一个节点指针
        struct quicklistNode *next;
        //当前节点的ZipList指针
        unsigned char *zl；
        //当前节点的ZipList的字节大小
        unsigned int sz;
        //当前节点的ZipList的entry个数
        unsigned int count : 16;
        //编码方式：1，ZipList；2，lzf压缩模式
        unsigned int encoding : 2;
        //数据容器类型(预留)：1，其他：2，ZipList
        unsigned int container ：2;
        //是否被解压缩1：则说明被解压缩了。将来要重新压缩：
        unsigned int recompress ：1;
        unsigned int attempted_compress ：1;
        unsigned int extra ：10 ;
    }quicklistNode;
    ```

    

![image-20251012143204257](images/image-20251012143204257.png)

#### SkipList

SkipList(跳表)首先是链表，但与传统链表比有几点差异

- 元素按升序排列
- 节点可能包含多个指针，只针跨度不同

![image-20251012165030040](images/image-20251012165030040.png)

```c
//t_zset.c
typedef struct zskiplist{
    //头尾节点指针
    struct zskiplist *header,*tail;
    //节点数量
    unsigned long length;
    //最大的索引层级，默认是1
    int level;
} Zskiplist
```

```c
//t_zset.c
typedef structzskiplistNode{
    sds ele;//节点存储的值
    double score;//节点分数、排序、查找用
    struct zskiplistNode *backward;//前一个节点指针
    struct zskiplistLevel{
        struct zskiplstNode *forward;//下一个节点指针
        unsigned long span;//索引跨度
    }level [];//多级索引数组
}zskiplistNode;
```

![image-20251012165443374](images/image-20251012165443374.png)



#### RedisObject

Redis种的任意数据类型的键和值会被封装成一个RedisObject，也叫做Redis对象，源码如下:

![image-20251012172531078](images/image-20251012172531078.png)

redis会根据存储数据类型的不同，选择不同的编码方式，共包含11种不同的类型：

| 编号 | 编码方式                | 说明                 |
| ---- | ----------------------- | -------------------- |
| 0    | OBJ_ENCODING_RAW        | raw编码的动态字符串  |
| 1    | OBJ_ENCODING_INT        | long类型的整数字符串 |
| 2    | OBJ_ENCODING_HT         | hash表(字典dict)     |
| 3    | OBJ_ENCODING_ZIPMAP     | 已废弃               |
| 4    | OBJ_ENCODING_LINKEDLIST | 双端链表             |
| 5    | OBJ_ENCODING_ZIPLIST    | 压缩列表             |
| 6    | OBJ_ENCODING_INTSET     | 整数集合             |
| 7    | OBJ_ENCODING_EMBSTR     | 跳表                 |
| 8    | OBJ_ENCODING_EMBSTR     | embstr的动态字符串   |
| 9    | OBJ_ENCODING_QUICKLIST  | 快速列表             |
| 10   | OBJ_ENCODING_STREAM     | stream流             |

Redis种会根据存储的数据类型不同，选择不同的编码方式。每种数据类型的使用的编码方式如下：

| 数据类型   | 编码方式                                         |
| ---------- | ------------------------------------------------ |
| OBJ_STRING | int、embstr、raw                                 |
| OBJ_LIST   | LinkedList和ZipList(3.2以前)、QuickList(3.2以后) |
| OBJ_SET    | intset、HT、                                     |
| OBJ_ZSET   | ZipList、HT、SkipList                            |
| OBJ_HASH   | ZipList、HT                                      |

#### 五种数据结构

##### String

String是Redis常见的数据类型：

- 其基本编码方式是RAW，基于简单动态字符串(SDS)实现，存储上限尾512mb
- 如果存储的SDS长度小于44字节，则会采用EMBSTR编码，此时object head与SDS是一段连续空间。申请内存是只需调用一次内存分配函数，效率更高
- 如果存储的字符串是整数值，并且大小在LONG_MAX,则会采用INT编码，直接将数据保存在RedisObject的ptr指针位置(刚好8字节),不在需要SDS了

 ![image-20251012180918516](images/image-20251012180918516.png)

##### List

Redis的List类型可以从首尾操作列表中的元素：

以下哪一个数据结构满足上述特征

- LinkedList：普通链表，可以双端访问，内存占用较高，内存碎片较多
- ZipList：压缩列表，可以双端访问，内存占用低
- QuickList：LinkedList+ZipList，可以双端访问，内存占用较低，包含多个ZipList，存储上限高

Redis的List结构类似一个双端链表，可以从首、尾操作列表中的元素

- 在3.2版本之前，Redis通过ZipList和LinkedList实现List，当元素数量小于512并且大小小于64字节四采用ZipList编码，超过则采用LinkedList编码
- 在版本3.2之后，Redis统一采用QuickList来实现List

```c
void pushGenericCommand(cilent *c, int where,int xx){
      int j;
    //尝试找到KEY对应的list
    robj *robj = lookupKeyWrite(c->db,c->argv[1]);
    //检查类型是否正确
    if(checkType(c,lobj,OBJ_LIST)) return;
    //检查是否为空
    if(!lobj){
        if(xx){
            addReply(c,shared.czero);
            return;
        }
        //为空，则创建新的QuickList
        lobj = createQuicklistObject();
        quicklistSetOptions(lobj->ptr,server.list_max_ziplist_size,
                           server.list_compress_depth);
        dbAdd(c->db,c->argv[1],lobj);
    }
}
```

```c
robj *createQuicklistObject(void){
    //申请内存并初始化QuickList
    quicklist *l = quicklistCreate();
    //创建RedisObject,type为OBJ_LIST
    //ptr指向QuickList
    robj *o = createObject(OBJ_LIST,l);
    //设置编码为QuickList
    o->encoding = OBJ_ENCODING_QUICKLIST;
    return o;
}
```

![image-20251014202543281](images/image-20251014202543281.png)

##### Set

Set集合是Redis中的单列集合，满足以下特点：

- 不保证有序性
- 保证元素唯一(可以判断元素是否存在)
- 求交集、并集、补集

HashTable，也就是Redis中的Dict，不过Dict是双列集合(可以存在键值对)

Set是redis集合，不一定确保元素有序，可以满足元素唯一，查询效率要求极高

- 为了查询效率和唯一性，set采用HT编码(Dict)。Dict中的key用来存储元素，value值统一为null
- 当存储的所有数据都是整数，并且元素数量不超过set-max-intset-entries时，Set会采用IntSet编码

set-max-intset-entires的默认值是512

```c
robj *setTypeCreate(sds value){
    //判断value是否是数值类型 long long
    if(isSdsRepresentableAsLongLong(value,NULL) == C_OK){
        //如果是数值类型，则采用IntSet编码
        return createIntsetObject();
        //否则采用默认编码，也就是HT
        return createSetObject();
    }
}

robj *createIntsetObject(void){
    //初始化INTSET并申请内存空间
    intset *is=intsetNew();
    //创建RedisObject
    robj *o = createObject(OBJ_SET,is);
    //指定编码为INTSET
    o->encoding = OBJ_ENCODING_INTSET;
    return o;
}

robj *createSetObject(void){
    //初始化Dict类型，并申请内存
    dict *d = dictCreate(&setDictType,NULL);
    //创建RedisObject(OBJ_SET,d);
    robj *o = createObject(OBJ_SET,d);
    //设置encoding为HT
    o->encoding = OBJ_ENCODING_HT;
    return o;
}
```

```c
int setTypeAdd(robj *subject，sds value）{
    long long llval;
    if(subject->encoding==OBJ_ENcoDING_HT){//已经是HT编码，直接添加元素
        dict *ht = subject->ptr;
        dictEntry *de = dictAddRaw(ht,value,NULL);
        if(de){
            dictSetKey(ht,de,sdsdup(value));
            dictSetVal(ht,de,NULL);
            return 1;
    	}
    }else if(subject>encoding ==OBJ_ENCODING_INTSET){//目前是INTSET
    //判断value是否是整数
    if (isSdsRepresentableAsLongLong(value,&llval) == C_OK) {
    	uint8_t success=0；//是整数，直接添加元素到set
   		subject->ptr = intsetAdd(subject->ptr,llval,&success);
        if (success）{
            /*当intset元素数量超出set_max_intset_entries，则转为HT.*/
            size_t max_entries = server.set_max_intset_entries;
            if (max_entries >= 1<<30）max_entries = 1<<30;
            if(intsetLen(subject->ptr）>max_entries)
            setTypeConvert(subject,OBJ_ENCODING_HT);
            return 1;
           }
       }else{//不是整数，直接转为HT
            setTypeConvert(subject,OBJ_ENCODING_HT);
            serverAssert(dictAdd(subject->ptr,sdsdup(value),NULL） == DICT_OK);
            return 1;
       }
	}else{
    serverPanic("Unknown set encoding");
    }
}
```

![image-20251014211714462](images/image-20251014211714462.png)

##### ZSet

Zset也就是sortedSet，其中每一个元素需要指定一个score和member值

- 可以根据score值排序后
- member必须唯一
- 可以根据member查询分数

键值存储，键必须唯一、可排序

- SkipList：可以排序，并且可以同时存储score和ele值(member)
- HT(Dtct)：可以根据键值存储，并且根据key找value

```c
//zset结构
typedef struct zset{
    //Dict指针
    dict *dict;
    //SkipList指针
    zskiplist *zsl;
}zset;

robj *createZsetObject(void){
    zset *zs = zmalloc(sizeof(*zs));
    robj *o;
    //创建Dict
    zs->dict = dictCreate(&zsetDictType,NULL);
    //创建SkipList
    zs->zsl = zslCreate();
    o = createObject(OBJ_ZSET,zs);
    o->encoding = OBJ_ENCODING_SKIPLIST;
    return o;
}
```

![image-20251014212419778](images/image-20251014212419778.png)

当元素不多时，HT和SkipList的优势不明显，而且更耗内存，因此zset还会采用ZipList结构来节省内存，不过需要满足条件：

1. 元素数量小于zset_max_ziplist_entries，默认值128
2. 每个元素都小于zset_max_ziplist_value，默认值64

```c
//zadd添加元素时，先根据key找到zset，不存在则创建新的zset
zobj =lookupKeywrite(c->db,key);
if (checkType(c,zobj,OBJ_ZSET)) goto cleanup;
//判断是否存在
if(zobj ==NULL){// zset不存在
    if (server.zset_max_ziplist_entries == 0 ||
    	server.zset_max_ziplist_value < sdslen(c->argv[scoreidx+1]->ptr))
    {//zset_max_ziplist_entries设置为0就是禁用了ZipList，
    	//或者value大小超过了zset_max_ziplist_value，采用HTSkipList
		zobj = createZsetobject();
    }else{//否则，采用ZipList
		zobj = createZsetZiplistobject();
    }
	dbAdd(c->db,key,zobj);
}
	zsetAdd(zobj，score，ele，flags，&retflags，&newscore);
}


robj *createZsetobject(void){
    //申请内存
    zset *zs = zmalloc(sizeof(*zs));
    robj *o;
    //创建Dict
    zs->dict=dictCreate(&zsetDictType,NULL);
    //创建SkipList
    zs->zsl = zslCreate();
    o= createObject(OBJ_ZSET,zs);
    o->encoding = OBJ_ENCODING_SKIPLIST;
    return o;
}
robj *createZsetZiplistobject(void){
    //创建zipList
    unsigned char *zl = ziplistNew();
    robj *o = createObject（OBJ_ZSET,zl)；
    o->encoding = OBJ_ENCODING_ZIPLIST;
    return o;
}
```

```c
int zsetAdd(robj *zobj, double score, sds ele, int in_flags, int
*out_flags, double *newscore){
    /*判断编码方式*/
    if (zobj->encoding == OBJ_ENCODING_ZIPLIST){// 是ZipList编码
        unsigned char *eptr;
        //判断当前元素是否已经存在，已经存在则更新score即可
        if （(eptr = zzlFind(zobj->ptr,ele,&curscore)） != NULL) {
        	//....略
        	return 1;
        } else if (!xx){
        //元素不存在，需要新增，则判断ziplist长度有没有超、元素的大小有没有超
        if (zzlLength(zobj->ptr)+1 > server.zset_max_ziplist_entries
        ||Tsdslen(ele) > server.zset_max_ziplist_value
        ||!ziplistSafeToAdd(zobj->ptr, sdslen(ele)))
        {//如果超出，则需要转为SkipList编码
        	zSetConvert(zobj,OBJ_ENCODING_SKIPLIST);
        }else{
            zobj->ptr = zzlInsert(zobj->ptr,ele,score);
            if (newscore) *newscore = score;
            *out_flags |= ZADD_OUT_ADDED;
            return 1;
        }
    }else{
        *out_flags |= ZADD_OUT_NOP;
        return 1;
        }
    }
    //本身就是SKIPLIST编码，无需转换
    if (zobj->encoding == OBJ_ENCODING_SKIPLIST){
    //...略
    }else{
    serverPanic("Unknown sorted set encoding");
    }
    return 0;/* Never reached.*/
}
```

ziplist本身没有排序功能,而且没有键值对的概念，因此需要有zset通过编码实现：

- ZipList是连续内存，因此score和element是紧挨在一起的两个entry，element在前，score在后
- score越小越接近队首，score越大越接近队尾，按照score值升序排列

![image-20251014214858847](images/image-20251014214858847.png)

##### Hash

Hash结构与Redis中的Zset非常类似

- 都是根据键值存储
- 都需要根据键获取值
- 键必须唯一

区别如下：

- zset的键是member，值是score；hash的键和值都是任意值
- zset要根据score排序；hash则无序排序

因此，Hash底层采用的编码与Zset基本一致，只需要把排序有关的SkipList去掉即可

![image-20251015212738649](images/image-20251015212738649.png)

![image-20251015212805078](images/image-20251015212805078.png)

- Hash机构默认采用ZipList编码，用以节省内存。ZipList中相邻的两个entry分别保存field和value
- 当数据量较大时，Hash结构会转为HT编码，也就是Dict，触发的条件有两个：
    1. ZipList中的元素数量超过了hash-max-ziplist-entries(默认512)
    2. ZipList中的任意entry大小超过了hash-max-ziplist-value(默认64字节)

```c
void hsetComgand(client *c) {// hset userl name Jack age 21
    int i, created = 0;
    robj *o;//略..
    //判断hash的key是否存在，不存在则创建一个新的，默认采用zipList编码
    if ((o = hashTypeLookupWriteOrCreate(c,c->argv[1])) == NULL) return;
    //判断是否需要把ZipList转为Dict
    hashTypeTryConversion(o,c->argv,2,c->argc-1) ;
    //循环遍历每一对field和value，并执行hset命令
    for (i = 2; i < c->argc; i += 2)
    	created += !hashTypeSet(o,c->argv[i]->ptr,c->argv[i+1]->ptr,HASH_SET_COPY);
    //略...
}

robj *hashTypeLookupWriteOrCreate(client *c，robj *key){
    //查找key
    robj *o =lookupKeywrite(c->db,key);
    if （checkType(c,o,OBJ_HASH)） return NULL;
    //不存在，则创建新的
    if(o==NULL){
    	o=createHashobject();
    	dbAdd(c->db,key,o);
    }
    return o;
}

robj *createHashobject(void){
    //默认采用zipList编码，申请zipList内存空间
    unsigned char *zl = ziplistNew();
    robj *o = createObject(OBJ_HASH, zl);
    //设置编码
    o->encoding = OBJ_ENCODING_ZIPLIST;
    return o;
}

void hashTypeTryConversion(robj *o,robjj **argv,int start, int end){
    int i;
    size_t sum = 0;
    //本来就不是zipList编码，什么都不用做了
    if (o->encoding != OBJ_ENCODING_ZIPLIST) return;
    //依次遍历命令中的field、value参数
    for (i = start; i<= end; i++){
        if (!sdsEncodedobject(argv[i]))
            continue;
        size_t len = sdslen(argv[i]->ptr);
        //如果field或value超过hash_max_ziplist_value，则转为HT
        if (len > server.hash_max_ziplist_value）{
            hashTypeConvert(o,OBJ_ENCODING_HT);
            return;
    	}
    	sum += len;
    }//zipList大小超过1G，也转为HT
    if (!ziplistSafeToAdd(o->ptr，sum))
    	hashTypeConvert(o, OBJ_ENCODING_HT);
    }
           
                     
int hashTypeSet(robj *o, sds field, sds value, int flags) {
    int update =0；
    //判断是否为ZipList编码
    if(o->encoding == OBJ_ENCODING_ZIPLIST){
        unsigned char *zl, *fptr, *vptr;
        zl=o->ptr;
        //查询head指针
        fptr = ziplistIndex(zl, ZIPLIST_HEAD);
        if(fptr！=NULL){//head不为空，说明ZipList不为空，开始查找key
        	fptr = ziplistFind(zl, fptr,(unsigned char*)field, sdslen(t);
        	if(fptr！=NULL){//判断是否存在，如果已经存在则更新
        		update = 1;
        		zl = ziplistReplace(zl, vptr，(unsigned char*)value,
       					 sdslen(value));
            }
        }                  
        //不存在，则直接push
        if(!update){//依次push新的field和value到ZipList的尾部
            zl = ziplistPush(zl,(unsigned char*)field, sdslen(field),
            ZIPLIST_TAIL);
            zl = ziplistPush(zl,(unsigned char*)value, sdslen(value),
            ZIPLIST_TAIL);
        }
        o->ptr = zl;
        /*插入了新元素，检查list长度是否超出，超出则转为HT*/
        if (hashTypeLength(o) > server.hash_max_ziplist_entries)
        	hashTypeConvert(o, OBJ_ENCODING_HT);
    } else if (o->encoding == OBJ_ENCODING_HT）{
    //HT编码，直接插入或覆盖
    else{
   	 serverPanic("Unknown hash encoding");
    }
    return update;
}
```

### 网络模型

#### 用户空间和内核空间

任何Linux发行版，其系统内核都是Linux，我们的应用都需要通过Linux内核与交互

![image-20251015215626384](images/image-20251015215626384.png)

Linux为了提高IO效率，会在用户空间和内核空间都加入缓冲区

- 写数据时，要把用户缓冲数据拷贝到内核缓冲区，然后写入设备
- 读数据时，要从设备读取数据到内核缓冲区，然后拷贝到用户缓冲区

![image-20251015220312674](images/image-20251015220312674.png)

#### 阻塞IO

 故名思意，阻塞IO就是两个阶段必须阻塞等待

![image-20251018210816194](images/image-20251018210816194.png)

 可以看到，阻塞IO模型，用户进程在两个阶段都是阻塞的状态

#### 非阻塞IO

顾名思义，非阻塞的IO的recvfrom操作会立即返回结果而不是阻塞用户进程

![image-20251018211043393](images/image-20251018211043393.png)

可以看到，非阻塞IO的模型中，用户进程在第一个阶段非阻塞，第二个阶段阻塞，虽然是非阻塞，但性能并没有得到提高。而且忙等机制会导致CPU空转，CPU使用率会暴增

#### IO多路复用 

无论是阻塞IO还是非阻塞IO，用户应用在一阶段都需要调用recvform来获取数据，差别在于无数据时的处理方案：

- 如果调用recvfrom，恰好没有数据，阻塞IO回事进程阻塞，非阻塞IO使CPU空转，都不能充分发挥CPU的作用
- 如果调用recvfrom，恰好有数据，则用户进程可以直接进入第二阶段，读取并处理数据

提高效率：

1. 多线程
2. 数据就绪了，用户应用就去读取数据

文件描述符(File Descriptor):简称FD，是一个从0开始递增的无符号整数，用来关联Linux中的一个文件，在Linux中一切接文件，例如常规文件，视频，硬件设备等，当然也包括网络套接字(Socket)

IO多路复用：是利用单线程来同时监听多个FD，并在某个FD可读，可写时得到通知，从而避免无效的等待，充分利用CPU资源

![image-20251018215245289](images/image-20251018215245289.png)

不过监听FD的方式、通知的方式又有多种实现，常见的有：

- select
- poll
- epoll

差异：

- select和poll只会通知用户进程有FD就绪，但不确定具体是内个FD，需要用户进程逐个遍历确认

- epoll则会通知用户进程FD就绪的同时，把已经就绪的FD写入用户空间

    ![image-20251018220429665](images/image-20251018220429665.png)

##### select

select是Linux中最早的I/O多路复用实现方案

```c
//定义类型别名__fd_mask，本质是Longint
typedef long int -_fd_mask;
/*fd_set记录要监听的fd集合，及其对应状态*/
typedef struct {
    //fds_bits是long类型数组，长度为1024/32=32
    //共1024个bit位，每个bit位代表一个fd，0代表未就绪，1代表就绪
    _fd_mask fds_bits[__FD_SETSIZE /__NFDBITS];
	//...
}fd_set;
//select函数，用于监听多个fd的集合
int select(
    int nfds,//要监视的fd_set的最大fd+1
    fd_set *readfds,//要监听读事件的fd集合
    fd_set *writefds,//要监听写事件的fd集合
    fd_set *exceptfds,////要监听异常事件的fd集合
    //超时时间，null-永不超时；0-不阻塞等待；大于0 -固定等待时间
    struct timeval *timeout
);
```

![image-20251019161334982](images/image-20251019161334982.png)

##### poll

poll模式对select模式做了简单修改，但性能提升并不明显，部分关键代码如下

```c
//pollfd中的事件类型
#define POLLIN//可读事件
#define POLLOUT//可写事件
#define POLLERR//错误事件
#define POLLNVAL//fd未打开
//pollfd结构
struct pollfd
    int fd;/*要监听的fd*/
    short int events;/*要监听的事件类型：读、写、异常*/
    shortintrevents;/*实际发生的事件类型*/
};
//pol函数
int poll(
structpoLfd*fds，//pollfd数组，可以自定义大小
nfds_tnfds，// 数组元素个数
inttimeout//超时时间
);
```

IO流程：

1. 创建pollfd数组，向其中添加关注的fd信息，数组大小自定义
2. 调用poll函数，将pollfd数组拷贝到内存空间，转链表存储，无上限
3. 内核遍历fd，判断是否就绪
4. 数据就绪或超时后，拷贝pollfd数组到用户空间，返回就绪fd数量n
5. 用户进程判断n是否大于0
6. 大于0则遍历pollfd数组，找到就绪的fd

与select对比

- select模式中的fd_set大小固定为1024，而pollfd在内核中采用链表，理论上无上限
- 监听FD越多，每次遍历消耗的时间也越久，性能反而会下降

##### epoll

epoll模式是对select和poll的改进，他提供了三个函数

```c
struct eventpoll {
    //...
    struct rb_rootrbr；//一颗红黑树，记录要监听的FD
    structList_headrdlist；//一个链表，记录就绪的FD
	//...
};
//1.会在内核创建eventpoll结构体，返回对应的句柄epfd
int epoll_create(int size);
//2.将一个FD添加到epoLL的红黑树中，并设置ep_poll_calLbak
//caLLback触发时，就把对应的FD加入到rdList这个就绪列表中
int epoll_ctl(
    int epfd,	//epoll实例的句柄
    int op,		//要执行的操作，包括：ADD、MOD、DEL
    int fd,		//要监听的FD
    structepoll_event*event//要监听的事件类型：读、写、异常等
);
//3.检查rdlist列表是否为空，不为空则返回就绪的FD的数量
int epoll_wait(
    int epfd,				//eventpoll实例的句柄
    structepoll_event*events,//空event数组，用于接收就绪的FD
    int maxevents,			//events数组的最大长度
    int timeout				//超时时间,-1用不超时；0不阻塞；大于0为阻塞时间
);
```

![image-20251019162652051](images/image-20251019162652051.png)

基于epoll实例中的红黑树保存要监听的FD，理论上无上限，而且增删改查效率都非常高，性能不会随监听的FD数量的增多而下降

每个FD只需要执行一次epoll_ctl添加到红黑树，以后每次epol_wait无需传递参数，无需重复拷贝FD到内存空间

内核会将就绪的FD直接拷贝到用户空间的指定位置，用户进程无需遍历所有FD就能知道就绪的FD是谁

##### 事件通知机制

当FD有数据可读式，我们调用epoll_wait就可以得到通知。但是事件通知的模式有两种：

- LevelTriggered：简称LT。当FD有数据可读的时候，会重复通知多次，直至数据处理完成，是Epoll的默认模式
- EdgeTriggered：简称ET。当FD有数据可读时，只会被通知一次，不管数据是否处理完成

结论：

- ET模式避免了LT模式可能出现的惊群现象
- ET模式最好结合非阻塞IO读取FD数据，相比LT会复杂一些

##### web服务流程

![image-20251019164747583](images/image-20251019164747583.png)

#### 信号驱动IO

信号驱动IO是与内核建立SIGIO信号关联并设置回调，当内核有FD就绪，会发出SIGIO信号通知用户，期间用户应用可以执行其他业务，无需阻塞等待

![image-20251019165009376](images/image-20251019165009376.png)

当有大量IO操作时，信号较多，SIGIO处理函数不能及时处理可能导致信号队列溢出而且内核空间与用户空间的频繁信号交互性能也较低

#### 异步IO

异步IO整个过程都是非阻塞的，用户进程调用完异步API就可以做其他事情，内核等待数据并拷贝到用户空间后才会递交信号，通知用户进程

![image-20251019165344049](images/image-20251019165344049.png)

可以看到，异步IO模型，用户进程在两个阶段都是非阻塞状态 

#### 同步或异步

IO操作无论是同步还是异步，关键看数据在内核空间与用户空间的拷贝过程(数据读写的IO操作)，也就是阶段二是同步还是异步

![image-20251019165644338](images/image-20251019165644338.png)



#### Redis网络模型

仅限于Redis的核心部分(命令处理)，是单线程

整个Redis，那么答案就是多线程 

Redis在版本迭代的过程中，在两个重要的时间节点引入了多线程支持

- ReidsV4.0：引入多线程异步处理一些耗时较长的任务，比如异步删除命令unlink
- RedisV6.0：在核心网络模型中引入多线程，进一步提高对于多核CPU的使用率

Redis为什么要选择单线程

- 抛开持久化不谈，Redis是纯内存操作，执行速度非常快，它的性能瓶颈是网络延迟而不是执行速度，因此多线程并不会带来巨大的性能提升
- 多线程会导致过多上下问切换，带来不必要的开销
- 引入多线程会面临线程安全的问题，必然引入线程锁这样的安全手段，实现复杂度增高，而且性能也会大打折扣

Redis通过IO多路复用来提高网络性能，并且支持各种不同的多路复用实现，并且将这些实现进行封装，提供了统一的高性能事件库API库AE：

![image-20251019172629985](images/image-20251019172629985.png)

```c
/*ae.c*/
#ifdef HAVE_EVPORT
#include"ae_evport.c"
#else
    #ifdef HAVE_EPOLL
    #include"ae_epoll.c"
    #else
        #ifdef HAVE_KQUEUE
        #include"ae_kqueue.c"
        #else
        #includee"ae_select.c"
        #endif
    #endif
#endif
```

Redis单线程网络模型整个结构

```c
server.c
int main(
	int argc,
	char**argv
){
    //...
    //初始化服务
	initServer(）;
	//开始监听事件循环
	aeMain(server.el);
	//...
}
```

```c
void initServer(void) {
	//...
    //内部会调用aeApiCreate（eventLoop），类似epoll_create
	server.el = aeCreateEventLoop(
				server.maxcLients+CONFIG_FDSET_INCR);
	//...
    //监听TCP端口，创建SerVerSocket，并得到FD
	listenToPort(server.port,&server.ipfd)
	//...
	//注册连接处理器，内部会调用aeApiAddEvent（&server.ipfd)监听FD
	createSocketAcceptHandler(&server.ipfd,acceptTcpHandler)
	//注册ae_api_poll前的处理器
	aeSetBeforeSleepProc(server.el,beforeSleep);
}
```

```c
voidaeMain(aeEventLoop*eventLoop){
    eventLoop->stop=0；
    //循环监听事件
    while(!eventLoop->stop){
    aeProcessEvents(
        eventLoop,
        AE_ALL_EVENTS|
            AE_CALL_BEFORE_SLEEP|
            AE_CALL_AFTER_SLEEP);
    }
}
```

```c
int aeProcessEvents(
	aeEventLoop *eventLoop,
	int flags){
	//... 调用前置处理器beforeSleep
	eventLoop->beforesleep(eventLoop);
	//等待FD就绪，类似epoLl_wait
	numevents = aeApiPoll(eventLoop,tvp);
	for(j=θ；j<numevents；j++){
		//遍历处理就绪的FD，调用对应的处理器
    }
}
```

```c
//数据读处理器
void acceptTcpHandler(...){
	//...
	//接收socket连接，获取FD
	fd = accept(s,sa,len);
	//...
	//创建connection，关联fd
	connection *conn = connCreateSocket();
	conn.fd = fd;
	//...
    //内部调用aeApiAddEvent（fd，READABLE），
	//监听socket的FD读事件，并绑定读处理器readQueryFromCLient
	connSetReadHandler(conn，readQueryFromClient);
}
```

![image-20251019173812615](images/image-20251019173812615.png)

```c
void readQueryFromClient(connection *conn)
    //获取当前客户端，客户端中有缓冲区用来读和写
    client *c = connGetPrivateData(conn);
    //获取c->querybuf缓冲区大小
    long int qblen = sdslen(c->querybuf);
    //读取请求数据到c->querybuf缓冲区
    connRead(c->conn, c->querybuf+qblen, readlen);
    //解析缓冲区字符串，转为Redis命令参数存入c->argv数组
    processInputBuffer(c);
    //处理c->argv 中的命令
    processCommand(c);
}
int processCommand(client *c）{
    //根据命令名称，寻找命令对应的command，例如setCommand
    c->cmd = c->lastcmd = lookupCommand(c->argv[o]->ptr);
    //执行command，得到响应结果，例如ping命令，对应pingCommand
    c->cmd->proc(c);
    //把执行结果写出，例如ping命令，就返回"pong"给cLient，
    //shared.pong是字符串"pong"的sDs对象
    addReply(c,shared.pong);
}
void addReply(client *c,robj *obj）{
    //尝试把结果写到c-buf客户端写缓存区
    if (_addReplyToBuffer(c,obj->ptr,sdslen(obj->ptr)) != C_OK)
    		//如果c->buf写不下，则写到c->reply，这是一个链表，容量无上限
    		addReplyProtoToList(c,obj->ptr,sdslen(obj->ptr));
    //将客户端添加到server.clients_pending_write这个队列，等待被写出
    listAddNodeHead(server.clients_pending_write,c);
}
```

![image-20251019174601715](images/image-20251019174601715.png)

Redis6.0版本中引入了多线程，目的是提高IO读写效率。因此在解析客户端命令、写响应结果时采用了多线程。核心命令执行。IO多路复用的模块依然是由主线程执行

### 通信协议

#### RESP协议

Redis是一个CS架构的软件，通信一般分两步(不包括pipeline和PubSub)：

1. 客户端(cilent)项服务端(server)发送一条命令
2. 服务端解析并执行命令，返回响应结果给客户端

因此客户端发送命令的格式、服务端响应结果的格式必须有一个规范，这个规范就是通信协议

而在Redis中采用的是RESP(redis serislization Protocol)协议：

- Redis1.2版本引入了RESP协议
- Redis2.0版本中成为与Redis服务端通信的标准，称为RESP2
- Redis6.0版本中，从RESP2升级到RESP3协议，增加了更多的数据类型并且支持6.0的新特性--客户端缓存

但目前，默认依然的使用的是RESP2协议，也是我们要学习的协议版本(以下简称RESP)

在RESP中，通过首字节的字符来区分不同的数据类型，常用的数组类型包括5种

- 单行字符串：首字节是'+',后面跟上单行字符串，以CRLF("\r\n")结尾，例如返回"OK":"+OK\r\n"

- 错误：首字节是'-'，与单行字符串格式一样，只是字符串以异常信息，例如"-Error message\r\n"

- 数值：首字节是':'，后面跟上数字格式的字符串，以CRLF结尾。例如":10\r\n"

- 多行字符串：首字节是'$',表示二进制安全的字符串，最大支持512MB：

    - 如果大小为0，则代表空字符串："$0\r\n\r\n"
    - 如果大小为-1，则代表不存在："$-1\r\n"

    ![image-20251019181229411](images/image-20251019181229411.png)

- 数组：首字节是'*',后面跟上数组元素个数，在跟上元素，元素数据类型不限
    ![image-20251019181240392](images/image-20251019181240392.png)

#### 模拟Redis客户端

手写socket

### 内存策略

Redis之所以性能强，最主要的原因是就是基于内存存储。然而单节点的Redis其内存不宜过大，会影响持久化或主从同步的功能

我们可以修改配置文件来设置Redis的最大内存

```yaml
#格式：
#maxmemory <bytes>
#例如：
maxmeory 1gb
```

当内存使用达到上限时，就无法存储更多数据了

#### 过期策略

##### DB结构

学习Redis缓存的时候我们说过，我们可以通过expire命令给Redis的key设置TTL（存活时间）：

可以发现，当key的TTL到期之后，再次访问name返回的时nil，说明这个key不存在了，对应的内存也得到释放。从而起到内存回收的作用

Redis本身时一个典型的key-value内存存储的数据库，因此所有的key、value都保存在之前学习过的Dict结构中。不过在database结构体中，有两个Dict：一个用来记录key-value；另一个用来记录key-TTL

```c
typedef struct redisDb {
    dict *dict;/*存放所有key及value的地方，也被称为keyspace*/
    dict *expires;/*存放每一个key及其对应的TTL存活时间，只包含设置了TTL的key*/
    dict *blocking_keys;/* Keys with clients waiting for data (BLPoP)*/
    dict *ready_keys;/* Blocked keys that received a PUSH */
    dict *watched_keys;/* WATCHED keys for MULTI/EXEC CAS */
    int id;/* Database ID, 0~15 */
    long long avg-ttl;/*记录平均TTL时长*/
    unsigned Long expires_cursor；/* expire检查时在dict中抽样的索引位置。*/
    list *defrag_later;/*等待碎片整理的key列表。*/
}redisDb;
```

![image-20251021081654088](images/image-20251021081654088.png)

##### 惰性删除

顾名思义并不是TTL到期后立即删除，而是在访问一个key的时候，检查key的存货事件，如果已经过期才执行删除

```c
//查找一个key执行写操作
robj *lookupKeyWriteWithFlags(redisDb *db，robj *key，int flags)
{
    //检查key是否过期
    return lookupkey(db,key,flags);
    expireIfNeeded(db,key);
}
//查找一个key执行读操作
robj *lookupKeyReadwithFlags(redisDb *db，robj *key，int flags)
{
    robj *val;
    //检查key是否过期
    if (expireIfNeeded(db,key) == 1){
    	//...略
    }
    return lookupkey(db,key,flags);
}


int expireIfNeeded(redisDb *db,robj *key){
    //判断是否过期，如果未过期直接结束并返回0
    if(!keyIsExpired(db,key)） return θ；
    //...略
    //删除过期key
    deleteExpiredKeyAndPropagate(db,key);
    return 1;
}
```

##### 周期删除

顾名思义就是一个定时任务，周期性的抽样部分过期的key，然后执行删除。执行周期有两种：

- Redis会设置一个定时任务serverCron(),按照server.hz的频率来执行过期key清理，模式为slow
- Redis的每个事件循环前会调用beforeSleep()函数，执行过期key清理，模式为FAST

```c
//server.c
void initServer(void){
	//...
    //创建定时器，关联回调函数serverCron，处理周期取决于server.hz，默认10
    aeCreateTimeEvent(server.el，1，ServerCron,NULL，NULL)
}

//server.c
int serverCron(struct aeEventLoop *eventLoop,long long id,void *clientData）{
    //更新LrucLock到当前时间，为后期的LRU和LFU做准备
    unsigned int lruclock= getLRUclock();
    atomicSet(server.lruclock,lruclock);
    //执行database的数据清理，例如过期key处理
    databasesCron();ev
    return 1000/server.hz;
}
               
voidbeforeSleep(structaeEventLoop
*eventLoop){
	//...
    //尝试清理部分过期key，清理模式默认为FAST
	activeExpireCycle(
		ACTIVE_EXPIRE_CYCLE_FAST);
}
               
void aeMain(aeEventLoop *eventLoop){
    eventLoop->stop = 0;
    while(eventLoop->stop){
    //beforeSleep(）-->Fast模式清理
    //n=aeApiPoll（)
    //如果n>O，FD就绪，处理IO事件
    //如果到了执行时间，则调用serverCron（）-->SLOW模式清理
    }
}

void databasesCron(void){
    //尝试清理部分过期key，清理模式默认为SLOW
    activeExpireCycle(ACTIVE_EXPIRE_CYCLE_SLOW);
}
```

SLOW模式规则：

1. 执行频率收server.hz影响，默认为10，即每秒执行10次，每个执行周期100ms
2. 执行清理耗时不超过一次执行周期的25%
3. 逐个遍历db，逐个遍历db中的bucket，抽取20key是否过期
4. 如果没有达到事件上限(25ms)并且过期的key比例大于10%，在进行一次抽样否则结束

FAST模式规则(过期key比例小于10%不执行)：

1. 执行效率受beforeSleep()调用频率影响，但两次FAST模式间隔不低于2ms
2. 执行清理耗时不超过1ms
3. 逐个遍历db，逐个遍历db中的bucket，抽取20个key判断是否过期
4. 如果没有达到事件上限(1ms)并且过期key的比例大于10%，在进行一次抽样，否则结束

#### 淘汰策略

内存淘汰：就是当Redis内存使用达到设置的阈值时，Redis主动挑选部分key删除以释放更多的内存的流程。Redis会在处理客户端命令的方法processCommand()中尝试做内存淘汰

```c
int processCommand(client *c) {
    //如果服务器设置了server.maxmemory属性，并且并未有执行Lua脚本
    if (server.maxmemory && !server.lua_timedout) {
        //尝试进行内存淘汰performEvictions
        int out_of_memory = (performEvictions() == EVICT_FAIL);
        if (out_of_memory && reject_cmd_on_oom){ 
            rejectCommand(c, shared.oomerr);
            return C_OK;
        }
        //...
    }
}
                       
```

Redis支持8中不同策略选择删除的key

- noeviction：不淘汰任何key，但是内存写满时，不允许写入新数据，默认就是种新策略
- volatile-ttl：对设置了TTL的key，比较key的剩余TTL值，TTL越小越先被淘汰
- allkeys-random：对全体key随机进行淘汰。也就是直接从db->dict种随机挑选
- volatile-random：对设置了TTL的key，随机进行淘汰。也就是从db->expires中随机挑选
- allkeys-lru：对全体key，基于LRU算法进行淘汰
- volatile-lru：对设置了TTL的key，基于LRU算法进行淘汰
- allkeys-lfu：对全体key，基于LFU算法淘汰
- volatile-lfu：对设置了TTL的key，基于LFI算法进行淘汰

比较容易混淆的两个

- LRU(Least Recently Used)，最少最近使用，用当前时间减去最后一次访问的时间，这个值越大，淘汰的优先级越高
- LFU(Least Frequently Used)，最少频率使用。会统计每个key的访问频率，值越小淘汰优先级越高

Redis的数据都会被封装为RedisObject结构：

```c
typedef struct redisobject {
    unsigned type:4;		//对象类型
    unsigned encoding:4;	//编码方式
    unsigned lru:LRU_BITS;	//LRU：以秒为单位记录最近一次访问时间，长度24bit
    					  //LFU：高16位以分钟为单位记录最近一次访问时间，低8位记录逻辑访问次数
    int refcount;		   //引用计数，计数为0则可以回收
    void *ptr;			   //数据指针，指向真实数据
} robj;
```

LFU的访问次数之所以叫做逻辑访问次数，是因为并不是每次key被访问都计数，而是通过运算：

1. 生成0~1之间的随机数R
2. 计算1/(旧次数*lfu_log_factor+1),记录为P，lfu_log_factor默认为10
3. 如果R<P,则计数器+1，且最大不超过255
4. 访问次数会随时间衰减，距离上一次访问间隔每隔lfu_decay_time(默认1)，计数器-1

![image-20251021084038390](images/image-20251021084038390.png)
