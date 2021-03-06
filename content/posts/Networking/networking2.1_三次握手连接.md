---
title: "Networking 2.1: TCP 3-Way Handskake"
date: 2021-12-10T11:43:43+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Network

---

### TCP 3-Way Handshake (SYN, SYN-ACK,ACK)

| Message                              | Description                                                  |
| ------------------------------------ | ------------------------------------------------------------ |
| SYN<br />Synchronize [ˈsiŋ-krə-ˌnīz] | Used to initiate and establish a connection. It also helps you to synchronize sequence numbers between devices.用于发起和建立连接。它还可以帮助您在设备之间同步序列号。 |
| ACK<br />Acknowledgement             | Helps to confirm to the other side that it has received the SYN.有助于向对方确认它已收到 SYN。 |
| SYN-ACK<br />                        | SYN message from local device and ACK of the earlier packet.来自本地设备的 SYN 消息和较早数据包的 ACK。 |
| FIN                                  | Used to terminate a connection.用于终止连接。                |

![img](https://lh3.googleusercontent.com/VXn4OENswdtc0yZ6Bh19PovrKS5fJrbQFZJSIYzXRxKNpfdgfIE5oqL5tVaDbAmkCV2GNa0muQ-36wU0uOhWpMrlsKU3ZP2jRb-Eu5SqmAZx2Nqzu8CrWTgHc7jWG3PEB0E-LwM)

### **TCP 3-way handshake** 是在 TCP/IP 网络中用于在服务器和客户端之间建立连接的过程。

第1步（SYN）：在第一步中，客户端希望与服务器建立连接，因此它发送一个SYN段，通知服务器，客户端可能开始通信，并以什么序列号开始段。Client进入SYN_SENT状态，等待Server确认。

第二步（SYN + ACK）: 服务器以SYN-ACK信号位的设置响应客户端的请求。确认(ACK)表示它收到的段的响应，SYN表示它可能以什么序列号开始段。Server进入SYN_RCVD状态。

第3步（ACK）：在最后一部分，客户端发送ACK信号确认服务器的响应，他们都建立了一个可靠的连接，并开始实际的数据传输。



### **TCP连接握手为什么是三次而不是二次或者四次呢？**

原理:在不可靠信道上可靠地传输信息.可靠消息传输是基于我们的ack:确认号实现的，假如我们采用2次握手,client端发送建立连接请求后,server端收到消息之后,发送确认收到消息之后就分配资源等待client端发送数据，会存在在不可靠的网络通道下,client端发送了数据包A然后又发送了数据包B由于网络原因,后发送的数据包B先到达,然后server端收到数据包之后给其分配资源,准备接收数据,此时client跟server端就正常发送数据。

但是由于后面达到的数据包A又到达建立连接,此时server端就会再次分配资源。但是此时client端已经可以正常发送数据,已经进入了连接建立状态所以不再理会server端的资源分配，这样的话,在信道不可靠的情况下,多个请求发送时候会创建大量连接请求,服务端资源浪费。因为3次握手已经可以建立连接了不需要4次。三次握手不是TCP本身的要求, 而是为了满足"在不可靠信道上可靠地传输信息"这一需求所导致的。



### **如果已经建立了连接，但是客户端突然出现故障了怎么办？**

TCP设有一个保活计时器,客户端如果出现故障,服务器不能一直等下去白白浪费资源。服务器每收到一次客户端的请求后都会重新复位这个计时器，时间通常是设置为2小时，若两小时还没有收到客户端的任何数据，服务器就会发送一个探测报文段，以后每隔75秒钟发送一次。若一连发送10个探测报文仍然没反应，服务器就认为客户端出了故障，接着就关闭连接。



### **TCP long connection vs short connection**

**Long connection:** the client and the server do not disconnect after establishing the connection. After that, when the client accesses the content on the server again, it will continue to use this connection channel. 客户端和服务器在建立连接后不会断开连接。之后，当客户端再次访问服务器上的内容时，它将继续使用这个连接通道。
**Short connection:** the client and server establish a connection and immediately disconnect after sending data. The next time you want to retrieve data, you need to establish a connection again.客户端和服务器建立一个连接，并在发送数据后立即断开连接。下次你想检索数据时，你需要再次建立连接。