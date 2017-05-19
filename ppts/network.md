title: 网络分享
speaker: 陈洪
url: https://github.com/ksky521/nodePPT
transition: slide3
files: /js/demo.js,/css/demo.css,/js/zoom.js
theme: moon
usemathjax: yes

[slide style="background-image:url('/img/netbg2.jpg')"]
## 网络分享
<small>分享者：陈洪</small>

[slide]
## 需求：计算机通信
----
* 硬件层面，比特流传输，在局域网内主机到主机 {:&.rollIn}
* 跨网络找到主机
* 找到应用（端口查找），可靠传输
* 用什么语言和对方沟通

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
## 网络总体流程
----
缺一张网络通信总体流程图

[slide]
## 网络接口层
<font size="4" color="yellow">物理层和数据链路层</font>
----

* 负责的内容(不过路由器)
    * 封装成帧
    * 透明传输
    * 差错校验

[slide]
## 网络接口层(mac 报头)

<div >
    <img src="/img/mac.png">
</div>
---
> 为什么数据会有大小限制 {:&.rollIn}

[slide]
## MTU（Maximum Transmission Unit）

<div >
    <img src="/img/mtu.png">
</div>

---
> MTU大点好还是小点好 {:&.rollIn}

[slide]
## 网际层
<font size="4" color="yellow">网络层</font>
----

解决问题：多个网络使用路由器互联成为互联网中的各个问题

* 负责的内容
    * 虚拟互联网络，屏蔽各种物理网络的异构性
    * IP地址分类，子网划分
    * 路由转发
    * NAT
---    
> 有了mac地址为什么还要有IP地址 {:&.rollIn}

[slide]
## 网际层(IP 报头)

<div >
    <img src="/img/ip.png">
</div>
---
> 有MTU限制，IP大包如何传递 {:&.rollIn}

[slide]
## ARP(Address Resolution Protocol)
----
 解决问题：IP转MAC {:&.flexbox.vleft}
    * ARP缓存、静态ARP
    * VIP（HA）
    * ARP欺骗、ARP攻击

[slide]
## ICMP <font size='5'>(Internet Control Message Protocol)</font>
----
    * Ping
    * TTL(tracert traceroute)

[slide]
## 传输层
<font size="4" color="yellow">传输层</font>
----
解决问题：端到端的传输

* 端口
* UDP (User Datagram Protocol)
* TCP (Transmission Control Protocol)

---
> UDP不可靠指的是包容易丢还是内容不可靠 {:&.rollIn}

[slide]
## 端口
<font size="4" color="yellow">传输层</font>
----
* 常用端口
* 登记端口号
* 随机端口

---
> udp和tcp的端口可以相同吗 不同进程可以绑定同个端口吗 {:&.rollIn}

[slide]
## UDP 报头

<div >
    <img src="/img/ip.png">
</div>

---
> udp不可靠是指包容易丢，还是收到的内容会有问题 {:&.rollIn}

[slide]
## TCP
----

* 连接管理
* 可靠传输
* 流量控制
* 拥塞避免
* 心跳

[slide]
## TCP 报头

<div >
    <img src="/img/tcp.png">
</div>

--- 
> 没什么问题 {:&.rollIn}

[slide]
## TCP 三次握手

<div >
    <img src="/img/handshake.png">
</div>

--- 
> 三次握手是否可以改成两次 {:&.rollIn}

[slide]
## TCP 四次挥手

<div >
    <img src="/img/bey.jpg">
</div>

--- 
> 可以强制关闭连接吗{:&.rollIn}


[slide]
## TCP 抓包图

<div >
    <img src="/img/handshakeSnap.jpg">
</div>

--- 
> 没有问题 {:&.rollIn}

[slide]
## TCP 可靠、有序传输

* 对字节编号
* 确认
* 差错校验
* 丢包重传

--- 
> 没有问题 {:&.rollIn}

[slide]
## TCP 流量控制-滑动窗口

<div >
    <img src="/img/window.jpg">
</div>

--- 
> 窗口最大能有多大 {:&.rollIn}

[slide]
## MSS(Maximum Segment Size)

--- 
> IP能分片为什么要有MSS {:&.rollIn}


[slide]
## 糊涂窗口综合征 && Nagle 算法
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
## TCP 拥塞避免

<div >
    <img src="/img/congestionAvoid.jpg">
</div>

---
> 没啥问题 {:&.rollIn}

[slide]
## TCP 拥塞避免-现象

---
* 下载慢慢变快 {:&.rollIn}
* 使用BT下载后上网很卡
* http1.0 1.1 2.0在这方面的区别

[slide]
# heartbeat 应用和场景
----
* TCP keep-alive
* 应用层心跳
* 断网、断电、kill进程

---
> 有问题吗 {:&.rollIn}

[slide]
# 线程模型
----
* JAVA BIO、NIO
* 同步异步
* 阻塞非阻塞
* select、poll、epoll

---
> 有问题吗 {:&.rollIn}

[slide]
# 应用层
----
* 举个例子
    * 最简单模拟tomcat实现
    * 最简单模拟kafka实现
