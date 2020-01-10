## 性能需求指标
两个层面定义性能场景的需求指标：  
* 业务指标
* 技术指标
> 两者有映射关系，技术指标不能脱离业务指标。  
一旦脱离，能回答“一个系统在多少RT之下能支持多少TPS”这样的问题，但回答不了“业务状态是什么”的问题。  

> e.g.如果一个系统要支持1000W人在线，可能测试结果是系统能支持1W的TPS，但很难回答1000W人在线是否会有问题。  

![031](https://github.com/zhengxiaoyu59/Notes/blob/master/%E6%80%A7%E8%83%BD%E6%B5%8B%E8%AF%95%E5%AE%9E%E6%88%9830%E8%AE%B2/images/031.png?raw=true)  
所有技术指标都是在有业务场景的前提下制定的，而技术指标和业务指标之间也要有详细的换算过程。  

![032](https://github.com/zhengxiaoyu59/Notes/blob/master/%E6%80%A7%E8%83%BD%E6%B5%8B%E8%AF%95%E5%AE%9E%E6%88%9830%E8%AE%B2/images/032.jpg?raw=true)  
