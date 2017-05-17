title: 网络分享
speaker: 陈洪
url: https://github.com/ksky521/nodePPT
transition: slide3
files: /js/demo.js,/css/demo.css,/js/zoom.js
theme: moon
usemathjax: yes

[slide style="background-image:url('/img/netbg2.jpg')"]
# 网络分享
<small>陈洪</small>

[slide]
# 网络需求
----
计算机通信 {:&.rollIn}

[slide]
# 计算机通信流程 
----
* 硬件层面，比特流传输，在局域网内主机到主机 {:&.rollIn}
* 跨网络找到主机
* 找到应用（端口查找），可靠传输
* 应用交互语言

<!--
 各自解决什么问题，局域网内传输，主机查找，端口查找，传输内容协调 3
 网络分层，网络访问层、互联网层、传输层和应用层，粗略讲一下OSI，标准和工业标准(不听建议)。3
 网络通信整个流程图 1 p66
 问题 2
 -->

[slide]
## 网络分层
----
OSI | TCP/IP | PDU（协议数据单元） | protocol
:-------|:------|:-------|:--------
<table><tbody<tr><td>应用层</td></tr><tr><td>表示层</td></tr><tr><td>会话层</td></tr></tbody></table> | 应用层 | message  |  HTTP、TSL/SSL、SMTP</br> FTP、SSH、TELNET、IMAP</br> POP、DNS、MIME、SNMP
传输层 | 传输层 | segment | TCP、UDP
网络层 | 网际层 | packet | IP 、ARP、RARP、ICMP
<table><tbody><tr><td>数据链路层</td></tr><tr><td>物理层</td></tr></tbody></table>| 网络接口层 | <table><tbody><tr><td>frame</td></tr><tr><td>bit</td></tr></tbody></table> | <table><tbody><tr><td>FDDI、Ethernet、PDN、SLIP、PPP</td></tr><tr><td>IEEE 802.1A  IEEE802.2-IEEE 802.11</td></tr></tbody></table> 

[slide]
# 网络接口层
<font size="4" color="yellow">物理层和数据链路层</font>
----

<div class="bs-example" data-example-id="text-capitalization">
    <p class="text-lowercase">Lowercased text.</p>
    <p class="text-uppercase">Uppercased text.</p>
    <p class="text-capitalize">Capitalized text.</p>
  </div>

<p class="text-center text-uppercase">abc主要确定与传输媒体的接口的一些特性，以及在局域网内主机与主机之间的通信 </p>
> 不经过路由器 
> 不保证可靠传输

负责的内容
* 封装成帧 {:&.rollIn}
* 透明传输 
* 差错校验

<!--
数据包的组装格式（mac，IP,端口)
报文格式：
跳网络mac会变
mac帧结构 

ping -D -s 1453 www.fenqile.com
-->

[slide]
# MTU（Maximum Transmission Unit）
----
最大传输单元是指一种通信协议的某一层上面所能通过的最大数据包大小
<div >
    <img src="/img/mtu.png">
</div>

<!--
    MTU太大或者太小有什么问题？
-->

[slide]
# 网际层
<font size="4" color="yellow">网络层</font>
----

多个网络使用路由器互联成为互联网中的各个问题

负责的内容
* 虚拟互联网络，屏蔽各种物理网络的异构性 {:&.rollIn}
* IP地址分类，子网划分
* 路由转发
* NAT

* IP包内容
* ARP协议（跳网络时换MAC）：VIP（HA),ARP欺骗
* ICMP协议（PING）
* tracert traceroute 命令 TTL的概念

<!-- 
有了MAC为什么还需要有IP地址
-->


[slide]
#ARP/IP/TCP协议
<div class="columns2">
    <div >
        <img src="/img/arp.png" height="250" width="550">
        <img src="/img/ip.png" height="250" width="550">
    </div>
    <div>
        <img src="/img/tcp.png" height="350">
    </div>
</div>

<!--
各个协议头的原地址和目标地址有什么不一样？
-->


[slide]
## 传输层
<font size="4" color="yellow">传输层</font>
----

* UDP
* TCP
* 端口

UDP（不可靠传输）
优势以及合适的场景，语音 视屏
广播和多波，QQ自己重写确认机制，游戏，视频

TCP（可靠传输）
滑动窗口
流量控制
拥塞控制
连接管理

端口： 
熟知端口号
登记端口号
客户端使用的端口号
tip: UDP和TCP使用的是两套端口，可以相同 

问题：UDP不可靠指的是包容易丢还是内容不可靠？

<!--
端口和套接字
21/tcp FTP 文件传输协议
22/tcp SSH 安全登录、文件传送(SCP)和端口重定向
23/tcp Telnet 不安全的文本传送
25/tcp SMTP Simple Mail Transfer Protocol (E-mail)
53	DNS域服务器所开放的端口
67/68／udp DHCP Dynamic Host Configuration Protocol
69/udp TFTP Trivial File Transfer Protocol
79/tcp finger Finger
80/tcp HTTP 超文本传送协议 (WWW)
110/tcp POP3 Post Office Protocol (E-mail)
113/tcp ident old identification server system
119/tcp NNTP used for usenet newsgroups
161	SNMP简单网络管理协议 的端口号
162	SNMP简单网络管理协议 的端口号
220/tcp IMAP3
443/tcp HTTPS used for securely transferring web pages
-->

[slide]
## 端口
* 常用端口
* 登记端口号
* 随机端口

问题： udp和tcp的端口可以相同吗， 多个进程可以绑定同个端口吗

[slide]
## UDP
图

问题： udp不可靠是指包容易丢，还是收到的内容会有问题

[slide]
# tcp 
----
报头
* 连接管理 三次握手 四次挥手
<!-- 三次握手是否可以改成两次？  -->
* 可靠传输
<!-- 单双工，半全，抓包图， http机制的又改成了单工 -->

* 滑动窗口 MSS
<!-- MTU,为什么要有mss，为什么不让IP层分片? -->
<!-- 有两张图，发送窗口，接收窗口，序号按字节来算 -->

* 拥塞避免 
<!-- 
慢开始（下载慢慢变快）
快重传（不需要等timeout）
快恢复（迅雷为什么那么快，端口平分网速）
-->

* 糊涂窗口综合症
<!-- 什么时候发送数据的问题，攒数据，满mss或者200ms -->

<!--
抓包图
心跳（tcp自带心跳，业务心跳，reset）
不讲：同个端口是否能被多个应用绑定，reuse readdr , UDP和TCP端口是否能重复
-->


[slide]
## Nagle’s Algorithm：
----

<pre><code class="markdown">/* 伪代码如下 */
if there is new data to send
  if the window size >= MSS and available data is >= MSS
    send complete MSS segment now
  else
    if there is unconfirmed data still in the pipe
      enqueue data in the buffer until an acknowledge is received
    else
      send data immediately
    end if
  end if
end if
</code>
</pre>

[slide]
# heartbeat
----
* 保证通讯双方具备通信能力 - 三次握手 {:&.rollIn}
<!-- 三次握手是否可以改成两次？  -->
* keep-alive
* 应用层心跳
* reset 
[slide]
# 应用层
<font size="4" color="yellow">会话层/表示层／应用层</font>
----
http 超文本传输协议
Linux IO模型 理解socket编程从应用层接口到驱动收发包的全部过程 2
BIO,NIO,AIO, 比较。 select,epoll,iocp 2 对比图
同步异步（消息通信机制），阻塞非阻塞的区别（程序在等待调用结果（消息，返回值）时的状态）。 
bio自己去邮局取快递，取不到就不回家，一直打电话，知道有快递到。
NIO，大家一起请一个快递员帮大家送（netty中work线程不推荐耗时操作


[slide]
JAVA
BIO 面向流
NIO 面向缓冲

[slide]
#例子
小tomcat(半包问题，BIO)
小kafka(NIO, zero copy，协议类似tcp)