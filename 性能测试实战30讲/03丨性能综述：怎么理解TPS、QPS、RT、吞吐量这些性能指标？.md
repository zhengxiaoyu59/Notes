# 性能需求指标
两个层面定义性能场景的需求指标：  
* 业务指标
* 技术指标
> 两者有映射关系，技术指标不能脱离业务指标。  
一旦脱离，能回答“一个系统在多少RT之下能支持多少TPS”这样的问题，但回答不了“业务状态是什么”的问题。  

> e.g.如果一个系统要支持1000W人在线，可能测试结果是系统能支持1W的TPS，但很难回答1000W人在线是否会有问题。  

![031](https://github.com/zhengxiaoyu59/Notes/blob/master/%E6%80%A7%E8%83%BD%E6%B5%8B%E8%AF%95%E5%AE%9E%E6%88%9830%E8%AE%B2/images/031.png?raw=true)  
所有技术指标都是在有业务场景的前提下制定的，而技术指标和业务指标之间也要有详细的换算过程。  


|简写|英文全称|含义|
|--|--|--|
| RT | Response Time | 响应时间。包括Request Time和Response Time |
| HPS | Hits Per Second | 每秒点击数 |
| TPS | Transactions Per Second | 每秒事务数 |
| QPS | Queries Per Second | 在MySQL中指每秒SQL数 |
| RPS | Requests Per Second | 每秒请求数 |
| CPS | Codes Per Second | 在HTTP协议中，CPS偶有提及，指的是HTTP返回码每秒 |
| PV | Page View | 页面浏览量 |
| UV | Unique Visitor | 独立访问者 |
| IP | Internet Protocol | 本意是IP地址，在性能中一般指独立IP数 |
| Throughput | / | 吞吐量 |
| IOPS | Input/Output Operations Per Second | 通常描述磁盘 |

## 对性能指标的误解
QPS 一开始是用来描述 MySQL 中 SQL 每秒执行数 Query Per Second，所有的 SQL 都被称为 Query。后来，由于一些文章的转来转去，QPS 被慢慢地移到了压力工具中，用来描述吞吐量，于是这里就有些误解，QPS 和 TPS 到底是什么关系呢？  

RPS 指的是每秒请求数。这个概念字面意思倒是容易理解，但是有个容易误解的地方就是，它指的到底是哪个层面的 Request？如果说 HTTP Request，那么和 Hits Per Second 又有什么关系呢？  

HPS，这也是个在字面意思上容易理解的概念。只是 Hit 是什么？有人将它和 HTTP Request 等价，有人将它和用户点击次数等价。  

CPS，用的人倒是比较少，在性能行业中引起的误解范围并不大。同时还有喜欢用 CPM（Calls Per Minute，每分钟调用数）的。这两个指标通常用来描述 Service 层的单位时间内的被其他服务调用的次数，这也是为什么在性能行业中误解不大的原因，因为性能测试的人看 Service 层东西的次数并不多。  


### TPS中的T如何定义
通常，根据场景的目的来定义TPS的粒度。  
如果是接口层性能测试，T可以直接定义为接口级；如果是业务级性能测试，T可以直接定义为每个业务步骤和完整的业务流。  
![033](https://github.com/zhengxiaoyu59/Notes/blob/master/%E6%80%A7%E8%83%BD%E6%B5%8B%E8%AF%95%E5%AE%9E%E6%88%9830%E8%AE%B2/images/033.png?raw=true)  
> 如果单独测试接口1、2、3，那T就是接口级的；如果从用户的角度来下一个订单，那1、2、3应该在一个T中，那T就是业务级的。  
还要分析系统是如何设计的。通常，积分服务是异步的，库存服务是同步的，所以这个业务可以看成只有1、2两个接口，但在做这样的业务级压力时，接口3也是必须要监控分析的。

性能中TPS的T的定义取决于场景目标和T的作用。一般这样定义事务：
* 接口级脚本  
——事务 start（接口 1）  
接口 1 脚本  
——事务 end（接口 1）  
——事务 start（接口 2）  
接口 2 脚本  
——事务 end（接口 2）  
——事务 start（接口 3）  
接口 3 脚本  
——事务 end（接口 3）  
> 每个接口分别对应一个事务，看哪个接口快。  

* 业务级接口层脚本（就是用接口拼接出一个完整的业务流）：  
——事务 start（业务 A）  
接口 1 脚本 - 接口 2（同步调用）  
接口 1 脚本 - 接口 3（异步调用）  
——事务 end（业务 A）  

* 用户级脚本  
——事务 start（业务 A）  
点击 0 - 接口 1 脚本 - 接口 2（同步调用）  
点击 0 - 接口 1 脚本 - 接口 3（异步调用）  
——事务 end（业务 A）  
> 从用户级的角度来说，包括了一个点击操作。  

要创建什么级别的事务，通常取决于测试目的。一般按由上到下的顺序（接口级-业务级-用户级）一一测试，这样路径清晰地执行是容易定位问题的。  

## 重新理解性能指标概念
