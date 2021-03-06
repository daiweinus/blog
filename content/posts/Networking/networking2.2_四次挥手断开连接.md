---
title: "Networking 2.2: TCP 4-way Handshake"
date: 2021-12-11T11:43:43+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Network
---

### [TCP 4-Way Handshake (FIN, ACK,FIN,ACK)](https://www.geeksforgeeks.org/tcp-connection-termination/)

![img](https://lh3.googleusercontent.com/A8Mf8oMVvrWZ4-zmf2kHcWQTd8f8X9yH2KPtkj0YkyNjm7L3M3--syXpPXGj-Mg9d2wVXYI00RGgi8F3dj__V4WLpgknPQsQocFpQefc8Qlr02LWMdheMNxXK_t7iDhJ0I0N-7Q)

1. client端向server发送FIN包，进入FIN_WAIT_1状态，这代表client端已经没有数据要发送了。
2. server端收到之后，返回一个ACK，进入CLOSE_WAIT等待关闭的状态，因为server端可能还有没有发送完成的数据。
3. 等到server端数据都发送完毕之后，server端就向client发送FIN，进入LAST_ACK状态。
4. client收到ACK之后，进入TIME_WAIT的状态，同时回复ACK，server收到之后直接进入CLOSED状态，连接关闭。但是client要等待2MSL(报文最大生存时间)的时间，才会进入CLOSED状态。



### **为什么TIME_WAIT状态需要经过2MSL(最大报文段生存时间)才能返回到CLOSE状态？**

因为网络是不可靠的，有可以最后一个ACK丢失。所以**TIME_WAIT状态就是用来重发可能丢失的ACK报文**。在Client发送出最后的ACK回复，但该ACK可能丢失。Server如果没有收到ACK，将不断重复发送FIN片段。所以Client不能立即关闭，它必须确认Server接收到了该ACK。Client会在发送出ACK之后进入到TIME_WAIT状态。Client会设置一个计时器，等待2MSL的时间。如果在该时间内再次收到FIN，那么Client会重发ACK并再次等待2MSL。所谓的**2MSL是两倍的MSL(Maximum Segment Lifetime)**。MSL指一个片段在网络中最大的存活时间，2MSL就是一个发送和一个回复所需的最大时间。如果**直到2MSL，Client都没有再次收到FIN，那么Client推断ACK已经被成功接收，则结束TCP连接**。 



### **Why need 4 ways handshake? 四次挥手的过程为什么server端ACK和FIN不在同一个请求里面发送？** 

因为数据发送的截止时间不同，当client发送FIN给server后，只是表示client所有数据都已经发送完毕，client还可以接受数据。但是server的数据发送的数据可能还没有截止，所以server需要先发送一个ACK告诉client我收到你的FIN信息了，等到server端的数据全部发送完成，在发送FIN告知client我的信息也已经全部发送，现在可以关闭链接了。因此，己方ACK和FIN一般都会分开发送。