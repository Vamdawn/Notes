# Redis key 命名规范

## 解释

目前所有微服务开发公用一套redis集群, 即所有服务设置的key-value都可以认为存放在一起, 如果key随意命名, 很可能出现问题:

1. key命名冲突, 如果2个服务使用了相同的keyname(不是特地这么做的情况下), 很大概率会造成数据的错误, 进而......

2. 假如随意命名, 且忘记设置key失效时间(而这其实很容易发生orz...), redis中会"散落"大量的key, 需要对redis进行清理时会是一个很恐怖的工作量(既要清理无效key, 又要保证不影响别的服务)

鉴于目前大家逐渐开始在项目中使用redis, 制定合适的规范会让大家少掉进一些坑

## key 命名时的关注点

redis官网对于key的规范有几点说明:

> - Very long keys are not a good idea. For instance a key of 1024 bytes is a bad idea not only memory-wise, but also because the lookup of the key in the dataset may require several costly key-comparisons. Even when the task at hand is to match the existence of a large value, hashing it (for example with SHA1) is a better idea, especially from the perspective of memory and bandwidth.
> 
> - Very short keys are often not a good idea. There is little point in writing "u1000flw" as a key if you can instead write "user:1000:followers". The latter is more readable and the added space is minor compared to the space used by the key object itself and the value object. While short keys will obviously consume a bit less memory, your job is to find the right balance.
> 
> - Try to stick with a schema. For instance "object-type:id" is a good idea, as in "user:1000". Dots or dashes are often used for multi-word fields, as in "comment:1234:reply.to" or "comment:1234:reply-to".
>
> - The maximum allowed key size is 512 MB.

1. keyname要在考虑可读性的基础上尽量短(节省空间)

2. keyname根据具体场景, 以环境/服务做隔离 (当下掉一个业务时就很方便...)

3. redis通常使用的keyname分隔符为 :

## 规范

目前暂定下4种规范, 之后会在base-tools封装工具给各个服务使用:

1. {env}:{application}:{service}:{feature}:{variable1}:{variable2}......

2. {env}:{service}:{feature}:{variable1}:{variable2}......

3. {application}:{service}:{feature}:{variable1}:{variable2}......

4. {service}:{feature}:{variable1}:{variable2}......

小小的说明:

规范#1, #2用于需要区分环境的key, 比如: 用在redis的生产消费模型, 需要隔离rc和prod(当然能用mq的场景还是用mq)

规范#1, #3命名包含application, 应该是最通常用的形式(大概..可能..), 用于服务之间的隔离

规范#2, #4不区分application, 可以用于通用的缓存设置

- env: 执行环境

- application: 服务名

- service: 业务

- feature: 功能

- variabeln: 第n个变量名(可选)

## 其他

1. 通常使用redis的场景, 建议都要设置过期时间

2. keyname虽然要保证可读性, 但是也不能太长, 过多的variable区分可以使用MD5或别的摘要算法来缩短其长度

## 更新记录

2020/09/25 建立文档, 更新v1.0.0版本
