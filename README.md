# log模块的设计与实现开发过程记录

#### 1. 需求分析

#### 1.1 功能需求
- [x] 注册日志对象
- [x] 日志服务只记录注册成功，过滤级别以上的日志
- [x] 日志存储在/log/testlog/
- [x] 每条日志使用linux换行符结束
- [x] 按照日志大小保存

##### 1.2 性能指标
1.时间
2.cpu
3.内存
4.压缩比
5.数据完整性



### 2. 设计
##### 2.1 技术穿刺
- [x] 压缩技术
- [x] tcp-server实现
- [x] DDD框架
- [x] tcp client发包 demo
- [x] tcp server端收报demo
- [x] 领域驱动设计初步设计


##### 2.2 软件设计
- [x] ddd框架
- [x] 领域对象抽象
- [x] 并发设计


### 3  实现
##### 3.1编码
- [x] tcp-server
- [x] service + repository
- [x] logWorker
 	- [x]  过滤符合业务要求的日志
- [x] logSaver
 	- [x] 如何在内存中压缩
 	- [x] 保存文件为指定大小

##### 3.2 重构和优化
- [x] 优化cpu
    - [x] 优化json
    - [x] 优化map	
    - [x] 优化select

- [x] 验证不压缩的数据完整性
- [x] 使用zappy压缩，并优化
- [x] 优化压缩算法的内存
- [x] 优化String转切片

### 4. 测试用例
- [x] 客户端连续发送，查看受包是否正常
- [x] 客户端单连接多携程发包
- [x] 客户端单连接单协程发包
- [x] 客户端多连接发包
- [x] 客户端只发送一包然后断链查看看服务短是否正常。
- [x] 不注册组件，发送日志， 主次组件， 发送日志，



### 5.疑问记录

1.每条日志是一个短连接？

2.如何判断一个日志的结束。

3.client是并发发送日志文件吗

4.日志对象没有注册时会不会发送这个对象的日志？会不会出现这种情况，在一个tcp连接上a在发送一个日志对象的日志，这时应该丢弃这些日志，然后又一个连接b上 注册这个日志对象，在这个注册以后的时间段需要在a上收日志。

5.cpu使用率如何考察？

6.测试环境上会不会有测试用例？

7.最后一个字符串也会有/0结尾？

8.在硬盘中压缩和在cpu中压缩的区别

9.会不会出现文件句柄过多的问题





### 6. 亮点

已注册组件的持久化

功能完整性

扩展性

支持调试参数







### 7. 黑客松总结
1.性能调优的方法
  -	在每个阶段的结束位置大点，统计每个阶段的时间
  -	使用分析工具分析性能指标 pprof
  -	协程的控制顺序打开顺序关闭


2.需求分析
 1. 需求分析时应看到本质，如果不能确定，不要过早的动手

3.开发阶段
 1. 过早的优化是万恶之源 
 2. tdd非常重要，tdd会帮助你对需求的理解，同时会让你的工作永远在需求之内。


4.其它
 1. 对于底层操作的理解非常重要
 2. ddd的可扩展性和职责分离在性能调试时修改代码很方便。
 3. ddd很重要的一方面是拆分技术的复杂度和业务的复杂度。
 4. 对文件系统，编译原理，虚拟机，cpu处理时间等知识的了解不够。
 5. 业务方面的知识非常重要，非常重要，非常重要！
 6. 团队合作非常重要，如何把人组到一个团队中，并让大家爆发出最大的生产力是一个很重要的能力。单兵作战是没有前途的。
 7. 健康很重要，强度再高也要吃早餐

### 8 黑客松正赛总结:

在ppt方面，没有把最能证明自己的性能方面的东西展示出来。应该一开始就说明自己性能的成绩是第二名

在ppt展示方面，又犯了中软件技能而不重业务的错。对于业务的如何调优，也是非常关键的，没有把业务如何优化讲清楚，两者都很重要

### 9. 后续学习
1.如何进行任务拆分
2.linux系统。