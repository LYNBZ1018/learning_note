##  1.数据通信网络基础

### 通信与网络

* 华为设备图标

![image-20220912215211551](https://gitee.com/lynbz1018/image/raw/master/img/20220912215212.png)

* 常见术语
  * 头部 + 数据载荷 + 尾部 =封装> 数据报 =解封装> 数据载荷

![image-20220912220535350](https://gitee.com/lynbz1018/image/raw/master/img/20220912220536.png)

* 数据通信网络基本概念
  * 通过防火墙访问Internet

![image-20220912223415975](https://gitee.com/lynbz1018/image/raw/master/img/20220912223417.png)

* 交换机
  * 是距离终端用户最进的设备
  * 用于终端设备的网络接入
  * 二层交换

![image-20220912223718088](https://gitee.com/lynbz1018/image/raw/master/img/20220912223719.png)

* 路由器

![image-20220912224056508](https://gitee.com/lynbz1018/image/raw/master/img/20220912224057.png)

* 防火墙
  * 网络安全设备

![image-20220912224214523](https://gitee.com/lynbz1018/image/raw/master/img/20220912224215.png)

* 无线设备
  * 无线胖AP
  * 无线瘦AP 更多的功能放到AC上

![image-20220912224354838](https://gitee.com/lynbz1018/image/raw/master/img/20220912224356.png)



### 网络类型与网络拓扑

* 局域网LAN、广域网WAN

![image-20220913233317721](https://gitee.com/lynbz1018/image/raw/master/img/20220913233319.png)

* 局域网组成城域网，然后通过广域网的节点由城域网组成广域网

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220913233646.png" alt="image-20220913233645628" style="zoom:50%;" />



* 网络拓扑：用传输介质互联各种设备所呈现的结构化布局。

* 全网状型网络：可靠性最高，同时成本也会较高。

![image-20220913235020360](https://gitee.com/lynbz1018/image/raw/master/img/20220913235021.png)



### 网络工程与网络工程师

* 网络工程

机房里的网络设备通过传输介质连接起来

交换机、路由器都属于路由部分

用户通过AP等无线设备连接

![image-20220913235610152](https://gitee.com/lynbz1018/image/raw/master/img/20220913235611.png)

* 网络工程师

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220913235928.png" alt="image-20220913235927486" style="zoom:50%;" />



## 2.网络参考模型

### 网络参考模型

#### OSI参考模型

![image-20220915173927165](https://gitee.com/lynbz1018/image/raw/master/img/20220915173928.png)

#### TCP/IP参考模型

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220915181108303.png" alt="image-20220915181108303" style="zoom: 67%;" />

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220915181258.png" alt="image-20220915181256831" style="zoom:67%;" />

##### 应用层

* 应用层的PDU称为数据

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220915181826.png" alt="image-20220915181825663" style="zoom:67%;" />

##### 传输层

* 传输层的PDU 成为段

![image-20220915183101590](https://gitee.com/lynbz1018/image/raw/master/img/20220915183102.png)

* TCP的三次握手

![image-20220915184129695](https://gitee.com/lynbz1018/image/raw/master/img/20220915184130.png)

* Ack：上一个序列号+数据载荷长度

![image-20220915184738170](https://gitee.com/lynbz1018/image/raw/master/img/20220915184739.png)

​                                                                                                             Ack = a + 13 + 66

* 滑动窗口

![image-20220915190813885](https://gitee.com/lynbz1018/image/raw/master/img/20220915190815.png)

* 四次挥手
  * pc2收到断开请求 并发送收到报文后，会向pc1再发送一个请求断开报文

![image-20220915190948159](https://gitee.com/lynbz1018/image/raw/master/img/20220915190949.png)

##### 网络层

* 网络层中PDU称为包

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220915192842.png" alt="image-20220915192841274" style="zoom:67%;" />

##### 数据链路层

* 数据链路层的PDU 称为帧

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220915192922828.png" alt="image-20220915192922828" style="zoom:67%;" />

* 每一个网卡都有一个唯一的MAC地址
* 交换机会维护一个MAC地址表

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220915193119184.png" alt="image-20220915193119184" style="zoom: 67%;" />

* ARP地址解析协议

1. 发送一个数据报之前，需要MAC地址，**会先在ARP缓存中查找**
2. 如果缓存中没有，就会发送一个ARP请求报文，**目的地址全F进行广播**，收到MAC地址后再进行发送
3. 接收到arp请求的主机，会对目的ip和自己ip进行比较，相同的主机会**将发送的ip和mac地址存到自己的arp缓存中**
4. 收到arp request 的主机会再发送一个 arp reply

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220915194549465.png" alt="image-20220915194549465" style="zoom:50%;" />

##### 物理层

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220915195425.png" alt="image-20220915195424590" style="zoom:50%;" />



### 数据通信过程

* 发送方发送数据

![image-20220915201341378](https://gitee.com/lynbz1018/image/raw/master/img/20220915201342.png)

* 中间网络数据传输

发送方封装到物理层 

在交换机中解封到数据链路层获取MAC地址

在路由器中解封装到网络层获取IP地址

最终到目的主机解封装获取数据载荷

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220915202419969.png" alt="image-20220915202419969" style="zoom:67%;" />

* 接收方数据解封装

![image-20220915202950193](https://gitee.com/lynbz1018/image/raw/master/img/20220915202951.png)



  

## 3.华为VRP系统

### 华为VRP系统概述

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220918172310494.png" alt="image-20220918172310494" style="zoom: 67%;" />

* 可以将控制平面和转发平面分离
* 可以解决不同产品在数据链路层使用不同的硬件而对网络层的影响

![image-20220918172823319](https://gitee.com/lynbz1018/image/raw/master/img/20220918172824.png)

* VRP发展进程

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220918173243.png" alt="image-20220918173242614" style="zoom:67%;" />

* 文件系统

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220918173517.png" alt="image-20220918173516085" style="zoom:80%;" />

* 存储设备

![image-20220918174018038](https://gitee.com/lynbz1018/image/raw/master/img/20220918174019.png)

#### 设备管理

* 用户界面

![image-20220918174944624](https://gitee.com/lynbz1018/image/raw/master/img/20220918175119.png)

* 用户级别

![image-20220918175135167](https://gitee.com/lynbz1018/image/raw/master/img/20220918175136.png)

* WEB网管理方式
  * 主机和路由器必须网络可达的，即可以ping通

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220918175445.png" alt="image-20220918175444429" style="zoom:67%;" />

* 命令行-本地登录
  * 网络设备第一次通电配置 需要本地通电
  * console是网络设备上的借口

![image-20220918175803564](https://gitee.com/lynbz1018/image/raw/master/img/20220918175804.png)



<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220918175934145.png" alt="image-20220918175934145" style="zoom:67%;" />

* 远程登录
* ssh是加密登录 会对用户名和密码加密 别人抓包抓到了也不能用加密后的字符用于登录
* 终端和设备之间要可以ping通才可以连接

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220918180520646.png" alt="image-20220918180520646" style="zoom:67%;" />



<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220918221256254.png" alt="image-20220918221256254" style="zoom:80%;" />



### 华为VRP系统基本操作

* 配置任务
* 因为是全新没有配置过的路由器，所以第一次配置要用本地连接，通过串行口和console port

![image-20220918222547159](https://gitee.com/lynbz1018/image/raw/master/img/20220918222548.png)

```markdown
display version  // 查看版本信息
system-view  // 进入系统视图
sysname DAtacom-Router  // 更改设备名称
interface GigabitEthernet 0/0/1  // 进入接口视图
ip address 20.1.1.1 24  // 配置ip
undo ip address  // 删除上次配置
display this  // 查看当前视图的配置
quit  // 退会低级别的视图

save  // 保存
compare configuration  // 比较

save datacom.cfg  // 保存配置文件
dir // 查看
display startup  // 查看启动文件
startup saved-configuration datacom.cfg  // 设置启动文件
reset saved-configuration

reboot  // 重启设备
```

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220918230218348.png" alt="image-20220918230218348" style="zoom:80%;" />



## 4.网络层协议及IP编制

### 4.1网络层协议

* 对网络层的设备提供逻辑地址
* 负责数据报的寻址和转发
* 经常被提及的IP是指直接或者间接与IP协议有关的任何内容

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220918234348824.png" alt="image-20220918234348824" style="zoom:67%;" />

* TTL Time To Life 8bit，0-255
* 协议号指明了数据部分使用了什么样的协议，即指明传输层使用了什么协议。

![image-20220918235128932](https://gitee.com/lynbz1018/image/raw/master/img/20220918235130.png)

### 4.2IPv4地址介绍

#### IPv4地址定义

* 用于在网络中标识一个节点
* 用于IP报文在网络中寻址
* IPv4地址有32bit，用点分十进制表示

* 由 网络位 和 主机位 组成，后边要跟着网络掩码



#### IPv4地址分类方式

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220919001739829.png" alt="image-20220919001739829" style="zoom:80%;" />



* 主机位全为0是网络地址
* 主机位全为1是广播地址
* 可用地址数是2^n - 2

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220919002010.png" alt="image-20220919002009017" style="zoom:80%;" />

* 私网IP地址

![image-20220919002612105](https://gitee.com/lynbz1018/image/raw/master/img/20220919002613.png)

* 特殊IP地址

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220919002930.png" alt="image-20220919002929129" style="zoom:80%;" />



### 4.3子网划分

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220919235242825.png" alt="image-20220919235242825" style="zoom:80%;" />

* 在实际网络划分中，常常从主机数多的子网开始划分

### 4.4网际控制信息协议ICMP协议

* 用来在网络设备中传递各种差错和控制信息

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220919235556129.png" alt="image-20220919235556129" style="zoom:80%;" />



<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220920000005619.png" alt="image-20220920000005619" style="zoom:80%;" />

* ICMP 重定向

当路由检测到一台机器使用非最优路由时，回向该主机发送一个ICMP重定向报文，请求主机改变路由。

![image-20220920000324141](https://gitee.com/lynbz1018/image/raw/master/img/20220920000325.png)

* ICMP差错检测

用ping检测到达目的主机的可达性

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220920000651.png" alt="image-20220920000650834" style="zoom:67%;" />

* ICMP错误报告

Tracert通过每次更改TTL来获取每一条的超时报告报文，来追踪路径和通过时间戳来计算往返时间

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220920001112620.png" alt="image-20220920001112620" style="zoom:67%;" />



### 4.5IPv4地址配置及基本应用



* IP地址规划

应该是自顶向下，规划的目标是易管理、易扩展、利用率高

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220920001425.png" alt="image-20220920001424680" style="zoom:80%;" />



## 5.以太网交换基础

### 5.1以太网交换协议

* 以太网是当今局域网中最常用的通信协议标准
* 以太网是建立在CSMA/CD（载波监听多路访问/冲突检测）机制上的广播型网络

* 早期的以太网是共享式的发送数据帧前需要对网络进行监听
  * 先在是交换机组网以太网，交换机可以隔离冲突域，但是不能隔离广播域



* 冲突域

冲突域是连接在同一个共享介质上的所有节点的集合。

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220920225356.png" alt="image-20220920225355017" style="zoom: 50%;" />

* 广播域：广播报文所能到达的整个访问范围称为二层广播域

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220920225725160.png" alt="image-20220920225725160" style="zoom:50%;" />

* 以太网卡

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220920225909967.png" alt="image-20220920225909967" style="zoom:50%;" />



### 5.2以太网帧

* 以太网技术所使用的帧

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220920230359800.png" alt="image-20220920230359800" style="zoom:50%;" />

* 每一个网卡都有一个全球唯一的MAC地址来标识

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220920230728504.png" alt="image-20220920230728504" style="zoom:50%;" />

* MAC地址48bit，用12个十六进制数标识

* 前24位是IEEE分配的厂商代码 后24位是厂商自己分配的代码

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220920231314124.png" alt="image-20220920231314124" style="zoom:50%;" />

* 组播帧的从前开始数第八个是 1

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220920231806036.png" alt="image-20220920231806036" style="zoom:50%;" />

### 5.3以太网交换机介绍

* 二层交换机 工作在TCP/IP对等模型的第二层即数据链路层的交换机

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220920233801.png" alt="image-20220920233800173" style="zoom:67%;" />

* 交换机接收到数据帧后，会对比该帧的目的地址和mac地址表上的mac地址
* 如果有对应的就从那个接口发送出去；
* 如果没有找到就会采用泛洪方式向除接受口的所有接口发送该报文；
* 目的主机接收到后会发送一个回复报文 交换机接收到后 继续匹配 且会记录这个源mac和端口号到mac地址表

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220921000557023.png" alt="image-20220921000557023" style="zoom:67%;" />

* 单播帧没有匹配到就泛洪发送（出了接收口）
* 广播帧直接泛洪发送

* 如果目的**mac对应的接口和接受的端口一样就丢弃**



<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220921001124041.png" alt="image-20220921001124041" style="zoom:50%;" />

### 5.4同网段数据通信过程

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220921001715.png" alt="image-20220921001713870" style="zoom:80%;" />

## 6.VLAN原理与配置

### 6.1VLAN基本概念

* 当交换机的mac地址表为空的时候，就会进行泛洪式转发，如果网络过大主机很多就会有很多垃圾流量
* 可以利用VLAN划分多个广播域

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220921172913594.png" alt="image-20220921172913594" style="zoom:67%;" />

* 通过VLAN 标签区分VLAN

![image-20220921191952966](https://gitee.com/lynbz1018/image/raw/master/img/20220921191954.png)

* VLAN数据帧 由交换机打上
* PC处理的数据都是没有标签的
* 交换机将数据帧发送给主机时，会把VLAN标签去掉

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220921192515143.png" alt="image-20220921192515143" style="zoom:67%;" />



#### VLAN 划分方式

* 基于**接口**的划分
* 主机移动了需要重新划分VLAN

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220921193046649.png" alt="image-20220921193046649" style="zoom: 33%;" />

* 基于**MAC地址**划分
* 主机移动了不需要重新配置VLAN

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220921193306072.png" alt="image-20220921193306072" style="zoom: 33%;" />

#### 交换机端口

在交换机处理的帧都必须有vlan标签1

交换机的三种接口 Access Trunk Hybrid

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220921194058113.png" alt="image-20220921194058113" style="zoom: 33%;" />

* 在发送帧时，**只有vlan和pvid相同时才可以脱掉标签**

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220921194431390.png" alt="image-20220921194431390" style="zoom:33%;" />

* 即使主机1发送的是广播，也是只有主机3能发送

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220921195053179.png" alt="image-20220921195053179" style="zoom:33%;" />

* Hybrid相当于是Access和Trunk的杂交

* Hybrid中，在发送时，vid在untagged中就脱掉标签，在tagged中就不能脱掉

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220921195850522.png" alt="image-20220921195850522" style="zoom:33%;" />



## 7.生成树

### 7.1生成树基础

以太网交换网络中为了进行链路备份，通常会使用冗余链路，这会再交换网络中产生环路。

Spanning Tree Protocol就是用于解决交换网络中二层环路问题。

`运行STP协议的设备通过彼此交互信息发现网络中的环路，并且有选择的对某个接口进行阻塞，最终使环形网络变成树形网络。`

**STP**是一个用于局域网中消除环路的协议。

`1.防止环路 2.提供冗余备份链路`

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220921220646363.png" alt="image-20220921220646363" style="zoom:67%;" />

* 二层交换机网络通过冗余线路来增强网络的可靠性

* 引入冗余性同时也引入了二层环路问题，可能会到时数据帧在环路中不断循环

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220921230745.png" alt="image-20220921230744047" style="zoom:33%;" />

#### 二层环路问题

广播风暴 mac地址漂移

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220921231620188.png" alt="image-20220921231620188" style="zoom:50%;" />

#### 生成树的解决方案

* 交换机之间进行STP报文交互并进行无环拓扑计算，将某个接口阻塞，打破环路
* 生成树能**动态响应网络拓扑变化**调整阻塞接口

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220921232310844.png" alt="image-20220921232310844" style="zoom:50%;" />

#### 三层环路

* 三层环路 有ip头部的TTL可以防止无尽转发
* 二层环路就是指tcp/ip的第二层数据连路层的环路

![image-20220921233008223](https://gitee.com/lynbz1018/image/raw/master/img/20220921233009.png)

### 7.2基本概念和工作原理	

#### 生成树基本概念

**BID**

* BID越小越优，优先级相同，MAC地址越小越优，**最优的选举为根桥**
* 优先级范围 0 ~ 65535，默认32768，可以修改但必须为**4096的倍数**
* 802.1D 规定BID由16位桥优先级和48位桥MAC地址构成

![image-20220929095131715](https://gitee.com/lynbz1018/image/raw/master/img/20220929095133.png)

![image-20221002193626146](https://gitee.com/lynbz1018/image/raw/master/img/20221002193627.png)

Cost的默认值与接口速率、Cost计算方法有关

![image-20221002193730050](https://gitee.com/lynbz1018/image/raw/master/img/20221002193731.png)

根桥的RPC为0

![image-20221002193944629](https://gitee.com/lynbz1018/image/raw/master/img/20221002193945.png)

##### 端口优先级

![image-20221002194127059](https://gitee.com/lynbz1018/image/raw/master/img/20221002194128.png)

##### BPDU

![image-20221002194459235](https://gitee.com/lynbz1018/image/raw/master/img/20221002194500.png)

![image-20221002195115784](https://gitee.com/lynbz1018/image/raw/master/img/20221002195116.png)

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20221002195125.png" alt="image-20221002195124440" style="zoom: 50%;" />



![image-20221002195159444](https://gitee.com/lynbz1018/image/raw/master/img/20221002195200.png)

#### 生成树工作过程

1. 选举根桥

![image-20221002195952100](https://gitee.com/lynbz1018/image/raw/master/img/20221002195953.png)

2. 选举根端口

![image-20221002200241328](https://gitee.com/lynbz1018/image/raw/master/img/20221002200242.png)

3. 选举指定端口

![image-20221002200503529](https://gitee.com/lynbz1018/image/raw/master/img/20221002200504.png)



4. 阻塞预备端口

![image-20221002200616335](https://gitee.com/lynbz1018/image/raw/master/img/20221002200617.png)

![image-20221002200643679](https://gitee.com/lynbz1018/image/raw/master/img/20221002200644.png)

![image-20221002200736218](https://gitee.com/lynbz1018/image/raw/master/img/20221002200737.png)

#### 拓扑变化过程

![image-20221002201024923](https://gitee.com/lynbz1018/image/raw/master/img/20221002201026.png)

![image-20221002201314233](https://gitee.com/lynbz1018/image/raw/master/img/20221002201315.png)

![image-20221002201432120](https://gitee.com/lynbz1018/image/raw/master/img/20221002201433.png)

![image-20221002201659960](https://gitee.com/lynbz1018/image/raw/master/img/20221002201701.png)

![image-20221002201806592](https://gitee.com/lynbz1018/image/raw/master/img/20221002201807.png)



### 7.3RSTP对STP的改进

![image-20221002202042317](https://gitee.com/lynbz1018/image/raw/master/img/20221002202043.png)

![image-20221002202112384](https://gitee.com/lynbz1018/image/raw/master/img/20221002202113.png)



![image-20221002202149478](https://gitee.com/lynbz1018/image/raw/master/img/20221002202150.png)

![image-20221002202249726](https://gitee.com/lynbz1018/image/raw/master/img/20221002202250.png)

![image-20221002202306444](https://gitee.com/lynbz1018/image/raw/master/img/20221002202307.png)

## 8.以太网链路聚合与交换机堆叠、集群

### 8.1网络可靠性需求

**网络可靠性**：当设备或链路上出现一个或过个故障时仍能保障网络不间断的服务的能力

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220922122040166.png" alt="image-20220922122040166" style="zoom:50%;" />

* 单板可以增加备份主板、线路
* 设备可以增加冗余设备备份，用STP辅以解决环路问题
* 生成树可以实现没有环路；有冗余备份；但是会造成带宽浪费。



### 8.2链路聚合技术原理与配置

* 通过将多个物理接口捆绑成一个逻辑接口，可以在不升级硬件的情况下，达到升级链路带宽的目的。
* 聚合模式有 手工模式 和 LACP模式

![image-20220922124005612](https://gitee.com/lynbz1018/image/raw/master/img/20220922124006.png)

#### 手工模式

`老旧设备、低端，不支持LACP模式`

`Eth-Trunk的建立、成员接口的加入都是由手动配置的`

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220922172656471.png" alt="image-20220922172656471" style="zoom:67%;" />

##### 缺陷

`为了使链路聚合接口正常工作，必须保证本端成员接口的对端接口：1.属于同一设备;2.加入同一链路聚合接口`

`设备间没有报文交互，只能通过管理员人工确认`

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220922172856949.png" alt="image-20220922172856949" style="zoom:67%;" />



#### LACP模式

* 链路聚合控制协议数据单元

`通过协议协商保证对端是同一设备、同一聚合接口的成员接口`

`LACPDU包括 设备优先级 MAC地址 接口优先级 接口号`

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220922175250475.png" alt="image-20220922175250475" style="zoom:67%;" />

##### 系统优先级

系统两端的活动接口数必须一样，否则无法建立聚合链路。这是可以**使一端成为主动端**，另一端根据主动端选择活动接口。

`1.系统优先级默认为32768，越小优先级越高；2.系统优先级相同时比较MAC地址，值越小优先级越高`

##### 接口优先级

选出主动端后，会根据主动端的接口优先级选择活动接口。

`1.接口优先级默认为32768，越小越优；2.接口优先级相同时，根据接口编号选择，越小越优`

##### 最大活动接口数

LACP模式下支持配置最大活动接口数，当接口数超过限制后，会比较主动端的接口优先级、接口号选出最优的使用，其余的作为备份链路。

如果有链路发生故障,在非活动链路中选择出一条优先级最高的替换掉，**实现总体带宽不变化、业务的不间断转发。**

##### 负载分担

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220922210708295.png" alt="image-20220922210708295" style="zoom:80%;" />

* 采用源目IP模式较好，可以使数据流较均衡的分担到各个活动链路上

![image-20220922210933647](https://gitee.com/lynbz1018/image/raw/master/img/20220922210934.png)

##### 链路聚合使用的典型场景

![image-20220922211555592](https://gitee.com/lynbz1018/image/raw/master/img/20220922211556.png)

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220922211721041.png" alt="image-20220922211721041" style="zoom: 67%;" />

### 8.3交换机堆叠、集群概述

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220922212449676.png" alt="image-20220922212449676" style="zoom:67%;" />

`1.逻辑上一台设备，简化运维方便管理；2.可以避免单点故障；3.物理上五环网络；4.链路聚合中链路全部有效使用`

![image-20220922212547743](https://gitee.com/lynbz1018/image/raw/master/img/20220922212549.png)

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220922212905030.png" alt="image-20220922212905030" style="zoom:50%;" />

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220922212921097.png" alt="image-20220922212921097" style="zoom:50%;" />

* 两个设备之间采用链路聚合
* 上下层之间使用集群或堆叠实现备份路线 增加带宽 提高网络可靠性

![image-20220922213103846](https://gitee.com/lynbz1018/image/raw/master/img/20220922213105.png)







## 9.IP路由基础

### 9.1路由基本概念

IP地址**唯一**标识了网络中的一个节点，每个IP地址都有自己的一个网段，要实现IP寻址，分布在不同区域的网段要能够相互通信

* 三层网络设备**路由器**，指导报文转发路径，要维护一个路由表

   

路由信息： 目的IP/网络掩码、出口、下一条地址

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220922235504.png" alt="image-20220922235503534" style="zoom:50%;" />

   

**路由条目的生成**

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220923000430118.png" alt="image-20220923000430118" style="zoom: 50%;" />

   

**直连路由**

直连路由的目的IP和接口IP是同一网段

直连路由出现在路由表中的前提是：该接口的物理转态和协议状态都是UP

![image-20220923000852281](https://gitee.com/lynbz1018/image/raw/master/img/20220923000853.png)

​         

**最优路由条目优选**

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220923001747.png" alt="image-20220923001746532" style="zoom:50%;" />

目的网络不同 - 都加入路由表

目的网络相同 - 将优先级低的加入路由表



<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220923002406465.png" alt="image-20220923002406465" style="zoom:50%;" />



优先级相同时 - COST度量小的加入路由表

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220923002500536.png" alt="image-20220923002500536" style="zoom:50%;" />

​    

**路由转发**

* 最长匹配原则

`当有多个路由条目匹配时，选择匹配长度最长的那个路由条目进行转发`

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220923003442193.png" alt="image-20220923003442193" style="zoom:50%;" />



### 9.2静态路由

静态路由需要网络管理员手动配置，不能动态适应网络拓扑变化

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220923004109.png" alt="image-20220923004108783" style="zoom: 50%;" />

* 默认路由，

`ip route-static 0.0.0.0 10.0.0.2  // 将默认路由设置为10.0.0.2`

![image-20220923004252336](https://gitee.com/lynbz1018/image/raw/master/img/20220923004253.png)

### 9.3动态路由

动态路由可以自主发现和生成路由，在拓扑变化时能及时更新路由，适合大规模的三层设备给网络

![image-20220923004626173](https://gitee.com/lynbz1018/image/raw/master/img/20220923004627.png)

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220923004832350.png" alt="image-20220923004832350" style="zoom:67%;" />



### 9.4路由高级特性

* 递归路由

![image-20220923005141899](https://gitee.com/lynbz1018/image/raw/master/img/20220923005143.png)

* 等价路由

来源相同、开销相同的路由都会加入路由表，两条路由指向相同的目的网段，但是有不同的下一条，会进行流量的分担

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220923005328.png" alt="image-20220923005327412" style="zoom:50%;" />



* 浮动路由

主路由的备份，保障路由链路稳定

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220923005557099.png" alt="image-20220923005557099" style="zoom:67%;" />

##### 路由汇总

CIDR无类别域间路由：允许任意长度的掩码长度，由IP地址/掩码长度组成。

路由汇总：将一组有规律的路由汇聚成一条路由，从而达到减小路由表规模以及优化设备资源利用率的目的。

将一组路由的二进制表示形式放到一起，找到所有目的网络地址中”相同的比特位“

**汇总引发的问题**

带来环路问题

因为进行了路由汇总，RTA的汇总后的目的网络更加宽泛

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220925222641454.png" alt="image-20220925222641454" style="zoom: 67%;" />

增加一条指向Null0的路由即可解决环路问题

![image-20220925223026337](https://gitee.com/lynbz1018/image/raw/master/img/20220925223027.png)

**精确汇总**

![image-20220925223938522](https://gitee.com/lynbz1018/image/raw/master/img/20220925223939.png)





## 10.实现VLAN间通信

### 10.1VLAN通信技术背景

同网段、同VLAN的主机进行通信可以通过二层交换机进行转发，不需要三层网络设备。

不同VLAN进行通信，需要三层设备。

![image-20220925231542632](https://gitee.com/lynbz1018/image/raw/master/img/20220925231543.png)



### 10.2使用路由器实现VLAN间通信

**通过物理接口实现**

每一个VLAN间都要在路由器和二层交换机之间有一条链路，如果VLAN过多就会使路由器的接口占用过于庞大

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220925232850.png" alt="image-20220925232848947" style="zoom:67%;" />

**通过子接口实现**

优点：减少了物理接口的使用，降低了成本

缺点：只使用了一个物理接口，坏掉后所有的VLAN间通信都会中断，所有VLAN通信都占用同一个物理接口会造成平均带宽很低

![image-20220925234125327](https://gitee.com/lynbz1018/image/raw/master/img/20220925234126.png)



### 10.3使用VLANIF技术实现VLAN间通信



![image-20220925235834424](https://gitee.com/lynbz1018/image/raw/master/img/20220925235835.png)

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220926000612.png" alt="image-20220926000611770" style="zoom:80%;" />

### 10.4三层通信过程解析

![image-20220926001626191](https://gitee.com/lynbz1018/image/raw/master/img/20220926001627.png)



![image-20220926000841244](https://gitee.com/lynbz1018/image/raw/master/img/20220926000842.png)



## 11.OSPF基础

### 11.1OSPF协议概述

#### 动态路由协议分类

* 静态路由的缺点
  * 无法适应规模较大的网络
  * 无法动态响应网络变化



<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220926113456083.png" alt="image-20220926113456083" style="zoom:80%;" />

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220926113828722.png" alt="image-20220926113828722" style="zoom:67%;" />

建立邻居关系 - 传递LSDB，分享自己的接口信息 - 根据数据库建立最短路径树 - 生成路由表

![image-20220926114147993](https://gitee.com/lynbz1018/image/raw/master/img/20220926114149.png)

#### OSPF简介

![image-20220926222630831](https://gitee.com/lynbz1018/image/raw/master/img/20220926222632.png)



* 在核心交换机和汇聚交换机上运行OSPF，实现园区网络内的路由可达。



**区域**

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220926223448609.png" alt="image-20220926223448609" style="zoom:50%;" />

**Router-id**

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220926223528824.png" alt="image-20220926223528824" style="zoom: 33%;" />

**度量值**

Cost是没有小数的，如果值为0.1则会显示1；`100/100 = 1; 100/1000 = 0.1 = 1;两个Cost值相同`

可以手动修改Cost值，也可通过修改100Mbit/s来修改最大值 `1000/100 = 10;1000/1000 = 1;`

![image-20220926223613702](https://gitee.com/lynbz1018/image/raw/master/img/20220926223614.png)



**OSPF五种报文**

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220926224630.png" alt="image-20220926224246791" style="zoom:67%;" />



**邻居表**

**<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220926224627.png" alt="image-20220926224503858" style="zoom:67%;" />**

**LSDB表**

![image-20220926224616909](https://gitee.com/lynbz1018/image/raw/master/img/20220926224618.png)

**OSPF表**

OSPF表由的IP表不一定有

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220926224750588.png" alt="image-20220926224750588" style="zoom:67%;" />

### 11.2OSPF协议工作原理

#### OSPF邻居建立

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220926225348.png" alt="image-20220926225347468" style="zoom:67%;" />

![image-20220926225451745](https://gitee.com/lynbz1018/image/raw/master/img/20220926225452.png)

1. 发现了自己的邻居在邻居表中状态为 **2-Way**

![image-20220926225639634](https://gitee.com/lynbz1018/image/raw/master/img/20220926225652.png)

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220926230218.png" alt="image-20220926230217130" style="zoom:80%;" />

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220926230325.png" alt="image-20220926230323950" style="zoom:80%;" />



#### OSPF路由表建立

OSPF有四种网络类型：Broadcast、NBMA、P2MP、P2P

![image-20220926231033672](https://gitee.com/lynbz1018/image/raw/master/img/20220926231034.png)

![image-20220926231243678](https://gitee.com/lynbz1018/image/raw/master/img/20220926231244.png)

![image-20220926231329936](https://gitee.com/lynbz1018/image/raw/master/img/20220926231331.png)

##### DR与BDR制定路由器与备份制定路由器

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220926231626910.png" alt="image-20220926231626910" style="zoom:67%;" />

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220926231805802.png" alt="image-20220926231805802" style="zoom:67%;" />

##### 多区域

![image-20220926232100069](https://gitee.com/lynbz1018/image/raw/master/img/20220926232101.png)

##### OSPF路由器类型

![image-20220926232307473](https://gitee.com/lynbz1018/image/raw/master/img/20220926232308.png)





## 12.ACL原理与配置

### 12.1ACL技术概述

* 需要实现流量过滤

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927182015456.png" alt="image-20220927182015456" style="zoom:67%;" />

* **ACL是由一些列permit和deny语句组成的、有序规则的列表。**

![image-20220927182046918](https://gitee.com/lynbz1018/image/raw/master/img/20220927182048.png)



### 12.2ACL的基本概念及其工作原理

**ACL的组成**

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220927182804.png" alt="image-20220927182803805" style="zoom:67%;" />

**匹配规则**

![image-20220927182912529](https://gitee.com/lynbz1018/image/raw/master/img/20220927182913.png)

**通配符**

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927183328429.png" alt="image-20220927183328429" style="zoom:67%;" />

ACL中的通配符可以不连续

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927183436438.png" alt="image-20220927183436438" style="zoom:67%;" />

#### ACL分类

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927183802873.png" alt="image-20220927183802873" style="zoom:67%;" />

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927183848212.png" alt="image-20220927183848212" style="zoom:67%;" />

#### ACL匹配

系统按照ACL**规则编号从小到大**的顺序进行报文匹配，规则编号越小越容易匹配。

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927184137365.png" alt="image-20220927184137365" style="zoom:67%;" />

**匹配位置**

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927184524854.png" alt="image-20220927184524854" style="zoom:50%;" />



<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927184909216.png" alt="image-20220927184909216" style="zoom:67%;" />



## 13.AAA原理与配置

### 13.1AAA概述

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927185619801.png" alt="image-20220927185619801" style="zoom: 80%;" />

AAA是Authentication（认证）、Authorization（授权）和Accounting（计费）的简称，是网络安全的一种管理机制，提供了认证、授权、计费三种安全功能。

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927194626502.png" alt="image-20220927194626502" style="zoom:67%;" />

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927195237495.png" alt="image-20220927195237495" style="zoom:80%;" />

**认证**



![image-20220927195803289](https://gitee.com/lynbz1018/image/raw/master/img/20220927195804.png)



**授权**



<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927200132061.png" alt="image-20220927200132061" style="zoom:67%;" />



**计费**

路由器不具备计费功能

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927200256934.png" alt="image-20220927200256934" style="zoom:67%;" />

**RADIUS**

![image-20220927200558159](https://gitee.com/lynbz1018/image/raw/master/img/20220927200559.png)

**使用场景**

![image-20220927200700735](https://gitee.com/lynbz1018/image/raw/master/img/20220927200701.png)

## 14.网络地址转换

### 14.1NAT概述

* 随着互联网用户的增多，IPv4的共有地址资源显得越发短缺
* IPv4地址资源存在分配不均的问题，部分地区的IPv4可用公有地址严重短缺。

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927212237618.png" alt="image-20220927212237618" style="zoom:67%;" />



<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927212931581.png" alt="image-20220927212931581" style="zoom:80%;" />



### 14.2静态NAT

* 静态NAT要增加新的映射需要**网络管理员手动添加**

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927224641319.png" alt="image-20220927224641319" style="zoom:67%;" />

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927224809237.png" alt="image-20220927224809237" style="zoom:80%;" />

**配置**

![image-20220927225122970](https://gitee.com/lynbz1018/image/raw/master/img/20220927225124.png)



### 14.3动态NAT

访问外网时，临时从地址池分配一个没有使用的地址

![image-20220927230452252](https://gitee.com/lynbz1018/image/raw/master/img/20220927230453.png)



![image-20220927231135565](https://gitee.com/lynbz1018/image/raw/master/img/20220927231136.png)

**配置**

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927231215762.png" alt="image-20220927231215762" style="zoom:80%;" />

**no-pat 不做端口转换**

进行端口转换的是NAPT

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927231224070.png" alt="image-20220927231224070" style="zoom:80%;" />



### 14.4NAPT、Easy-IP

NAPT也会对端口进行转换，可以有效提高公网地址利用率

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220927232510.png" alt="image-20220927232509389" style="zoom:80%;" />

没有no-pat，进行端口转换

![image-20220927232602799](https://gitee.com/lynbz1018/image/raw/master/img/20220927232603.png)

#### Easy-IP

适用于不具备固定公网IP地址的场景

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927233020570.png" alt="image-20220927233020570" style="zoom:67%;" />

**配置**

也需要配置acl进行过滤

![image-20220927233157984](https://gitee.com/lynbz1018/image/raw/master/img/20220927233159.png)



### 14.5NAT Serer

布置在内网的服务器需要和外网连接需要使用NAT server

实现了内网主机对外网的服务

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927233946909.png" alt="image-20220927233946909" style="zoom:80%;" />

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220927234041613.png" alt="image-20220927234041613" style="zoom:80%;" />



![image-20220927234113667](https://gitee.com/lynbz1018/image/raw/master/img/20220927234114.png)



## 15.网络服务与应用

### 15.1FTP

#### FTP

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929170906972.png" alt="image-20220929170906972" style="zoom:67%;" />

**主动模式**

FTP有两个端口20和21

![image-20220929171547937](https://gitee.com/lynbz1018/image/raw/master/img/20220929171549.png)

**被动模式**

![image-20220929172127698](https://gitee.com/lynbz1018/image/raw/master/img/20220929172128.png)

#### TFTP

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929173620929.png" alt="image-20220929173620929" style="zoom:80%;" />

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929173706827.png" alt="image-20220929173706827" style="zoom:67%;" />



### 15.2Telnet

IP地址可达，可以连通TCP23号端口

![image-20220929174506321](https://gitee.com/lynbz1018/image/raw/master/img/20220929174726.png)



多个用户同时在VTY中进行配置，生效的是最后配置的那个

![image-20220929174652653](https://gitee.com/lynbz1018/image/raw/master/img/20220929174653.png)

### 15.3DHCP

要配置IP、掩码、网关，复杂；如果用户多，工作量大；利用率低；灵活性差；

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929182437451.png" alt="image-20220929182437451" style="zoom:67%;" />

#### DHCP优点

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929182728803.png" alt="image-20220929182728803" style="zoom:67%;" />

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929183146643.png" alt="image-20220929183146643" style="zoom:67%;" />



![image-20220929183345814](https://gitee.com/lynbz1018/image/raw/master/img/20220929183347.png)





### 15.4HTTP

![image-20220929185716645](https://gitee.com/lynbz1018/image/raw/master/img/20220929185717.png)

![image-20220929185953372](https://gitee.com/lynbz1018/image/raw/master/img/20220929185954.png)

使用TCP80端口

域名需要通过DNS转换为IP地址

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929190130293.png" alt="image-20220929190130293" style="zoom:67%;" />

服务器根据url在本地找到文件后传输给客户端

![image-20220929190230667](https://gitee.com/lynbz1018/image/raw/master/img/20220929190231.png)





### 15.5DNS

用UDP进行DNS请求和回应

![image-20220929190704680](https://gitee.com/lynbz1018/image/raw/master/img/20220929190705.png)

一般根域名不显示

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929190833356.png" alt="image-20220929190833356" style="zoom:67%;" />



**DNS查询**

![image-20220929190910655](C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929190910655.png)



### 15.6NTP

快速传输，使用UDP，端口123

用于同步时钟

![image-20220929191913115](https://gitee.com/lynbz1018/image/raw/master/img/20220929191914.png)

![image-20220929192138827](https://gitee.com/lynbz1018/image/raw/master/img/20220929192140.png)

![image-20220929192211871](https://gitee.com/lynbz1018/image/raw/master/img/20220929192213.png)



## 16.WLAN概念

### 16.1WLAN概述

WLAN指用无线信号代替有限局域网中的部分或全部传输介质所构成的网络。

WiFi是WLAN的一个子集。使用的无线电波，802.11是一个协议族。

WIFI是一个共享介质，是所有使用的终端加起来不超过最高的理论速度。

![image-20220929205255277](https://gitee.com/lynbz1018/image/raw/master/img/20220929205256.png)



![image-20220929210017698](https://gitee.com/lynbz1018/image/raw/master/img/20220929210018.png)





### 16.2WLAN的基本概念

**WLAN设备**

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929211500111.png" alt="image-20220929211500111" style="zoom:67%;" />

![image-20220929211741571](https://gitee.com/lynbz1018/image/raw/master/img/20220929211742.png)



<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929212049333.png" alt="image-20220929212049333" style="zoom:67%;" />

#### 有线侧组网概念

![image-20220929212643307](https://gitee.com/lynbz1018/image/raw/master/img/20220929212644.png)

![image-20220929212755429](https://gitee.com/lynbz1018/image/raw/master/img/20220929212756.png)

#### 无线侧组网

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929213444180.png" alt="image-20220929213444180" style="zoom:50%;" />

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220929213656.png" alt="image-20220929213655544" style="zoom:67%;" />

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220929215224.png" alt="image-20220929215223129" style="zoom:67%;" />

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929215704125.png" alt="image-20220929215704125" style="zoom:67%;" />

虚拟AP，可以设置不同的SSID

![image-20220929215837901](https://gitee.com/lynbz1018/image/raw/master/img/20220929215839.png)

由不同的BSS，相同的SSID，组成的一个大的虚拟BSS

![image-20220929220134399](https://gitee.com/lynbz1018/image/raw/master/img/20220929220135.png)



### 16.3WLAN的工作原理

![image-20220929230137513](https://gitee.com/lynbz1018/image/raw/master/img/20220929230138.png)



### 16.5新一代WLAN解决方案

<img src="https://gitee.com/lynbz1018/image/raw/master/img/20220929231256.png" alt="image-20220929231255559" style="zoom:67%;" />

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220929231347846.png" alt="image-20220929231347846" style="zoom:67%;" />

![image-20220929231428800](https://gitee.com/lynbz1018/image/raw/master/img/20220929231430.png)

![image-20220929231704948](https://gitee.com/lynbz1018/image/raw/master/img/20220929231706.png)





## 17.广域网技术

### 17.1早期广域网技术概述

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220930000146136.png" alt="image-20220930000146136" style="zoom:67%;" />

早期WAN和LAN的区别在与数据链路层和物理层的差异

![image-20220930000457168](https://gitee.com/lynbz1018/image/raw/master/img/20220930000458.png)

**广域网络设备**

![image-20220930000843699](https://gitee.com/lynbz1018/image/raw/master/img/20220930000844.png)

![image-20220930001010676](https://gitee.com/lynbz1018/image/raw/master/img/20220930001011.png)

### 17.2PPP协议原理与配置

#### PPP协议原理

![image-20220930095129492](https://gitee.com/lynbz1018/image/raw/master/img/20220930095131.png)

PPP**建立过程**

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220930095324770.png" alt="image-20220930095324770" style="zoom:67%;" />

PPP**链路接口状态机**

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220930095431135.png" alt="image-20220930095431135" style="zoom:67%;" />

**LCP协议报文**

![image-20220930095826554](https://gitee.com/lynbz1018/image/raw/master/img/20220930095827.png)

**LCP协商过程**

<img src="C:%5CUsers%5Clyn95%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5Cimage-20220930204849525.png" alt="image-20220930204849525" style="zoom:67%;" />



![](https://gitee.com/lynbz1018/image/raw/master/img/20220930205027.png)

**ppp认证模式**

![image-20220930205820839](https://gitee.com/lynbz1018/image/raw/master/img/20220930205822.png)

![image-20220930210650986](https://gitee.com/lynbz1018/image/raw/master/img/20220930210652.png)

**NCP协商**

![image-20220930211018345](https://gitee.com/lynbz1018/image/raw/master/img/20220930211019.png)



![image-20220930211111422](https://gitee.com/lynbz1018/image/raw/master/img/20220930211112.png)





### 17.3PPPoE原理与配置

既有以太网的灵活组网，又有PPP协议的认证、计费功能

![image-20220930212120458](https://gitee.com/lynbz1018/image/raw/master/img/20220930212121.png)

![image-20220930212417150](https://gitee.com/lynbz1018/image/raw/master/img/20220930212418.png)

#### PPPoE回话建立

![image-20220930212736754](https://gitee.com/lynbz1018/image/raw/master/img/20220930212737.png)

![image-20220930212926017](https://gitee.com/lynbz1018/image/raw/master/img/20220930212927.png)

![image-20220930213024677](https://gitee.com/lynbz1018/image/raw/master/img/20220930213025.png)

![image-20220930213058807](https://gitee.com/lynbz1018/image/raw/master/img/20220930213100.png)

![image-20220930213135200](https://gitee.com/lynbz1018/image/raw/master/img/20220930213136.png)

### 17.4广域网技术的发展

![image-20220930224241818](https://gitee.com/lynbz1018/image/raw/master/img/20220930224243.png)

#### MPLS标签转发

![image-20220930224540905](https://gitee.com/lynbz1018/image/raw/master/img/20220930224542.png)

![image-20220930224936764](https://gitee.com/lynbz1018/image/raw/master/img/20220930224938.png)

#### SR segment routing

![image-20220930225220619](https://gitee.com/lynbz1018/image/raw/master/img/20220930225221.png)

![image-20220930225351371](https://gitee.com/lynbz1018/image/raw/master/img/20220930225353.png)

![image-20220930225547540](https://gitee.com/lynbz1018/image/raw/master/img/20220930225548.png)

![image-20220930225727812](https://gitee.com/lynbz1018/image/raw/master/img/20220930225729.png)

![image-20220930225737057](https://gitee.com/lynbz1018/image/raw/master/img/20220930225738.png)

## 18.网络管理与运维

### 18.1网络管理与运维基本概念

![image-20220930232654811](https://gitee.com/lynbz1018/image/raw/master/img/20220930232656.png)

![image-20220930232827460](https://gitee.com/lynbz1018/image/raw/master/img/20220930232828.png)

![image-20220930233200475](https://gitee.com/lynbz1018/image/raw/master/img/20220930233201.png)







### 18.2传统网络管理

#### SNMP原理

![image-20220930233523390](https://gitee.com/lynbz1018/image/raw/master/img/20220930233524.png)

网络管理员通过NMS对不同的网络设备进行统一管理，NMS通过SNMP报文进行交互

![image-20220930233751952](https://gitee.com/lynbz1018/image/raw/master/img/20220930233753.png)

![image-20220930233917121](https://gitee.com/lynbz1018/image/raw/master/img/20220930233918.png)

![image-20220930234109937](https://gitee.com/lynbz1018/image/raw/master/img/20220930234111.png)



![image-20220930234248981](https://gitee.com/lynbz1018/image/raw/master/img/20220930234250.png)

![image-20220930234435759](https://gitee.com/lynbz1018/image/raw/master/img/20220930234436.png)



![image-20220930234601016](https://gitee.com/lynbz1018/image/raw/master/img/20220930234602.png)



### 18.3基于华为iMaster NCE的网络管理

![image-20220930234857657](https://gitee.com/lynbz1018/image/raw/master/img/20220930234858.png)

![image-20220930234947399](https://gitee.com/lynbz1018/image/raw/master/img/20220930234948.png)



![image-20220930235044337](https://gitee.com/lynbz1018/image/raw/master/img/20220930235045.png)



## 19.IPv6技术

### 19.1IPv6概述

![image-20221001231624101](https://gitee.com/lynbz1018/image/raw/master/img/20221001231625.png)

#### **IPv6的优势**

![image-20221001231734591](https://gitee.com/lynbz1018/image/raw/master/img/20221001231735.png)

#### IPv6的包头

![image-20221001232445829](https://gitee.com/lynbz1018/image/raw/master/img/20221001232447.png)

![image-20221001232538184](https://gitee.com/lynbz1018/image/raw/master/img/20221001232539.png)

![image-20221001232642727](https://gitee.com/lynbz1018/image/raw/master/img/20221001232643.png)

#### IPv6地址

![image-20221001232915894](https://gitee.com/lynbz1018/image/raw/master/img/20221001232917.png)

![image-20221001233201378](https://gitee.com/lynbz1018/image/raw/master/img/20221001233202.png)

### 19.2IPv6分类

![image-20221002000110676](https://gitee.com/lynbz1018/image/raw/master/img/20221002000112.png)

![image-20221002000541104](https://gitee.com/lynbz1018/image/raw/master/img/20221002000542.png)

![image-20221002001531713](https://gitee.com/lynbz1018/image/raw/master/img/20221002001532.png)

#### IPv6常见单播

##### 全球单播地址

![image-20221002001932449](https://gitee.com/lynbz1018/image/raw/master/img/20221002001933.png)

##### 本地唯一地址

![image-20221002002051131](https://gitee.com/lynbz1018/image/raw/master/img/20221002002052.png)



##### 链路地址

![image-20221002002245271](https://gitee.com/lynbz1018/image/raw/master/img/20221002002246.png)

#### 组播地址

![image-20221002002500102](https://gitee.com/lynbz1018/image/raw/master/img/20221002002501.png)

![image-20221002002710096](https://gitee.com/lynbz1018/image/raw/master/img/20221002002711.png)

#### 任播地址

当一组服务器提供相同的服务时，希望主机获取到最近的服务器提供服务，可以让这一组服务器提供一个任播地址

![image-20221002002911131](https://gitee.com/lynbz1018/image/raw/master/img/20221002002912.png)

![image-20221002003738028](https://gitee.com/lynbz1018/image/raw/master/img/20221002003739.png)

## 20.SDN与NFV概念

### 20.1SDN概述

#### 传统网络的缺点

![image-20221002105219000](https://gitee.com/lynbz1018/image/raw/master/img/20221002105220.png)

![image-20221002105556597](https://gitee.com/lynbz1018/image/raw/master/img/20221002105557.png)

![image-20221002105618482](https://gitee.com/lynbz1018/image/raw/master/img/20221002105619.png)



#### SDN定义

![image-20221002111630361](https://gitee.com/lynbz1018/image/raw/master/img/20221002111631.png)

![image-20221002111835575](https://gitee.com/lynbz1018/image/raw/master/img/20221002111836.png)



![image-20221002111957464](https://gitee.com/lynbz1018/image/raw/master/img/20221002111958.png)

![image-20221002112158784](https://gitee.com/lynbz1018/image/raw/master/img/20221002112159.png)



![image-20221002112338097](https://gitee.com/lynbz1018/image/raw/master/img/20221002112339.png)

![image-20221002112425139](https://gitee.com/lynbz1018/image/raw/master/img/20221002112426.png)



#### iMaster NCE解决方案

![image-20221002114645062](https://gitee.com/lynbz1018/image/raw/master/img/20221002114646.png)

![image-20221002114803704](https://gitee.com/lynbz1018/image/raw/master/img/20221002114804.png)



### 20.2NFV概述

![image-20221002115108852](https://gitee.com/lynbz1018/image/raw/master/img/20221002115110.png)

![image-20221002115238758](https://gitee.com/lynbz1018/image/raw/master/img/20221002115239.png)

![image-20221002115410218](https://gitee.com/lynbz1018/image/raw/master/img/20221002115411.png)

![image-20221002115519832](https://gitee.com/lynbz1018/image/raw/master/img/20221002115521.png)

![image-20221002115911225](https://gitee.com/lynbz1018/image/raw/master/img/20221002115912.png)

![image-20221002115957137](https://gitee.com/lynbz1018/image/raw/master/img/20221002115958.png)

![image-20221002115949824](https://gitee.com/lynbz1018/image/raw/master/img/20221002115951.png)



![image-20221002120116481](https://gitee.com/lynbz1018/image/raw/master/img/20221002120117.png)



## 21.网络编程与自动化

![image-20221002121037592](https://gitee.com/lynbz1018/image/raw/master/img/20221002121038.png)![image-20221002121058631](https://gitee.com/lynbz1018/image/raw/master/img/20221002121059.png)

![image-20221002121241331](https://gitee.com/lynbz1018/image/raw/master/img/20221002121242.png)

## 22.园区网络基本概念

用802.3 802.11构建一个局域网 -> 园区网

![image-20221002121506453](https://gitee.com/lynbz1018/image/raw/master/img/20221002121507.png)

![image-20221002122002652](https://gitee.com/lynbz1018/image/raw/master/img/20221002122003.png)

![image-20221002122059619](https://gitee.com/lynbz1018/image/raw/master/img/20221002122100.png)

![image-20221002122127076](https://gitee.com/lynbz1018/image/raw/master/img/20221002122128.png)

![image-20221002122205010](https://gitee.com/lynbz1018/image/raw/master/img/20221002122206.png)

![image-20221002122233877](https://gitee.com/lynbz1018/image/raw/master/img/20221002122235.png)