# redis 

[学习链接](https://github.com/ityouknow/spring-boot-examples)

#### 背景

一般的数据都是面向磁盘的，读写比较慢，当大量请求到来，极其容易造成数据库瘫痪。

1.redis市当前比较广泛的NoSQL，性能远超数据库，并且支持集群、分布式、主从同步等配置，原则上可以无限扩展，还支持一定的事务能力。

2.存储缓存用的数据，需要高速读写的场景。

3.一般用来存储一些常用和主要的数据，比如用户登陆信息。

4.写操作多的没必要存在缓存中，数据量大的也没必要存在缓存中。

#### Spring boot中应用

1.Pom

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
<dependency>
    <groupId>org.apache.commons</groupId>
    <artifactId>commons-pool2</artifactId>
</dependency>
```

2.添加配置文件

```
# Redis数据库索引（默认为0）
spring.redis.database=0  
# Redis服务器地址
spring.redis.host=localhost
# Redis服务器连接端口
spring.redis.port=6379  
# Redis服务器连接密码（默认为空）
spring.redis.password=
# 连接池最大连接数（使用负值表示没有限制） 默认 8
spring.redis.lettuce.pool.max-active=8
# 连接池最大阻塞等待时间（使用负值表示没有限制） 默认 -1
spring.redis.lettuce.pool.max-wait=-1
# 连接池中的最大空闲连接 默认 8
spring.redis.lettuce.pool.max-idle=8
# 连接池中的最小空闲连接 默认 0
spring.redis.lettuce.pool.min-idle=0
```

3.添加cache的配置类

```java
@Configuration
@EnableCaching
public class RedisConfig extends CachingConfigurerSupport{
    
    @Bean
    public KeyGenerator keyGenerator() {
        return new KeyGenerator() {
            @Override
            public Object generate(Object target, Method method, Object... params) {
                StringBuilder sb = new StringBuilder();
                sb.append(target.getClass().getName());
                sb.append(method.getName());
                for (Object obj : params) {
                    sb.append(obj.toString());
                }
                return sb.toString();
            }
        };
    }
}
```





# jpa

### 是啥

 Java 持久化规范，它为 Java 开发人员提供了一种对象/关联映射工具来管理 Java 应用中的关系数据，和android中room差不多，操作对象来操作数据库。



# RabbitMQ

### 简介

RabbitMQ是一个开源的AMQP （Advanced Message Queuing Protocol，高级消息队列协议）实现，面向消息、队列、路由、可靠性、安全。服务端用Erlang语言编写，支持多个客户端。

AMQP是应用层协议的一个开放标准，为面向消息的中间件设计。消息中间件主要用于组件之间的解耦，消息的发送者无需知道消息使用者的存在，反之亦然。





