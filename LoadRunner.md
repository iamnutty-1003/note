# LoadRunner

## 一、QS

## 二、创建脚本

开始菜单-->LR-->Samples-->Web-->Start Web Server

(若被1080端口被占用，查看端口号

> netstat -ano
>
> 任务管理器-->查看PID所在进程-->结束进程

进入[LR自带网站](http://127.0.0.1:1080/WebTours/)

开始菜单-->LR-->Application-->HP Virtual User Generator



### 测试脚本概要

#### 脚本创建流程

Recording	录制生成脚本 	

Verification	验证脚本

Enhancements	增强,设置时间参数等参数

Prepare for Load	设置负载



#### Init,action,end说明

- init 录制的一般是业务流程开始前的初始化工作（如登录，服务器初始化
- action 录制业务流程操作事件
- end 录制退出时执行的操作(用户退出，注销)
- init和end不能迭代多次,只能执行一次。action可以迭代多次运行。(如一个用户登录后重复订票10次，就要把订票部分的脚本放在action当中进行迭代。登录部分脚本放在init，退出部分放在end。)



### 脚本录制

#### 录制

1. File-->new 
2. Recording Application-->Start Recording
3. 执行录制操作，完成后关闭
4. Script 存放脚本代码 Tree存放截图 再右边存放log

#### 回放

Verify Replay(验证脚本是否正常运行)-->Run-time Settings

工具栏Tools -->General Options -->Display 回放时显示视图，了解脚本运行过程

replay开始回放

完成时打开View-->Test Results

若失败，需要添加关联，因为回访时执行原有ID，而浏览器打开新会话会新生成一个ID，操作如下

- 手动关联：

  点开Tree右侧Show Output Window按键，打开Correlation Options，全部关联一遍

- 自动关联(不建议)

  Tools -->Recording Options -->Correlation

### URL模式与HTML模式

URL录制的脚本中web_concurrent_start是并发组开始的标记，web_concurrent_end是并发组结束的标记。开始时记录函数，结束时，所有函数并发执行。操作:

Tools -->Recording Options -->Recording

### 事务（transaction）

设置开始点和结束点，计算事务消耗时间

操作Insert-->Insert Start Transaction

操作Insert-->Insert End Transaction

示例选择自动判断状态LR_AUTO,日志中会有Transaction执行时长

### 脚本参数化

选定变量-->右键Replace With Parameter-->Properties-->Create Table-->add row-->browser-->导入.dat文件

(可使用数据向导)

## 三、创建测试场景

### 手工场景(Manual Scenario)

手动设置场景(用户数等)

#### 手动场景-计划方式

scenario:多个脚本按设定的场景计划来统一运行

group:多个脚本按独立设置跑，各个脚本可以单独设置虚拟用户、运行时间等

#### 手工场景运行模式

Real-world schedule(实际计划)

​	可以通过Add Action来添加多个用户变化过程，包括多次负载增加用户，持续时间，停止用户

basic schedule

​	经典模式，只能设置一次负载运行的虚拟用户配置，不能设置多个用户运行

### 目标场景(Goal-Oriented Scenario)

#### 定义:

​	设置一个运行目标，通过Controller的自动加载功能进行自动化负载，如果测试的结果达到目标，说明系统的性能符合测试目标

#### 5种目标类型

- Virtual Users

- Hits per Second

- Transactions per Second

- Transactions Response Time

  ​	表示事物的响应时间，反应系统的处理速度以及一个操作花费的时间

- Pages per Minutes

  ​	表示每分钟页面的刷新次数

### 负载生成器(Load Generators)

​	Load Generators是运行脚本的负载引擎，相当于加压机。默认情况下是使用本地负载生成器来运行脚本。

操作:	

​	每产生一个用户需要花费2-3M的内存空间，通常运行controller的主机很少用作负载生成器。负载生成器的工作通常由其他装有LR Agent的PC机来担任。如果负载生成器的内存使用率大于了70%，就会成为系统瓶颈，导致测试成绩下降。所以大量虚拟用户需要多个Load Generators来完成大规模的性能负载。

### 负载运行时设置(Run-time Settings)

### windows系统资源性能常用计数器

1. System
   - %Total Processor Time 所有CPU的平均利用率
   - File Data Operations/sec 计算机读取写入频率
   - Process Queue Length 线程在等待分配CPU资源所排队列的长度，如果大于处理器个数+1,则处理器可能处于阻塞状态
   

2. Process
   - %Process Time CPU利用率，如果持续超过95%，则说明当前系统瓶颈为CPU
   - %Priviliaged Time CPU在特权模式下说话时间百分比。一般系统服务，进程管理，内存管理属于这个
   - %User Time 与上面相反
   - %DPC Time 网络处理上消耗的时间
   - private Bytes 进程无法与其他进程共享的字节数量，当该值较大时，可能是内存泄露的信号
   - Work set 最近处理进程所用的内存页

3. Memory
4. Physical Disk
5. Network Interface