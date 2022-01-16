---
title: "Networking 3: Http vs Https"
date: 2021-12-12T11:43:43+08:00
draft: true
toc: false
images:
  - "images/totoro.jpeg"
tags: 
  - Network
---

[HTTP vs HTTPS](https://www.guru99.com/difference-http-vs-https.html)![img](https://lh4.googleusercontent.com/7yQxjAANYEPix4OvvtZieM8K62fc-bKvP8KArs9U2SVhV3Lb7RfdZrO4RO0W31n3yVOuNw1AVJjHiZkGdFhFUGPSI2lQDc90KicFqSIv9AgWRKBQrir6_D3Qs4S14DZiepFJVVw)**HTTP** is Hypertext Transfer Protocol,超文本传输协议,是建立在 TCP 之上的应用层网络协议。HTTP 使用超文本结构化文本,HTTP 为 Web 浏览器和服务器之间的通信提供了标准规则。

**HTTPS** is Hypertext Transfer Protocol Secure超文本传输​​协议安全。它是高度先进和安全的 HTTP 版本。它使用端口号。443 用于数据通信。它通过使用 SSL 加密整个通信来实现安全交易。它是 SSL/TLS 协议和 HTTP 的组合。它提供网络服务器的加密和安全标识。HTTP 还允许您在服务器和浏览器之间创建安全的加密连接。它提供数据的双向安全性。这有助于您保护潜在的敏感信息免遭窃取。在 HTTPS 协议中，SSL 事务是在基于密钥的加密算法的帮助下协商的。此密钥的强度通常为 40 或 128 位。与 HTTPS 一起使用的 SSL/TLS 证书类型现在，在本 HTTPS 和 HTTP 差异教程中，我们将介绍与 HTTPS 一起使用的 SSL/TLS 证书类型
域验证 Domain Validation:域验证验证申请证书的人是域名的所有者。这种类型的验证通常需要几分钟到几个小时。
组织验证 Organization Validation:证书颁发机构不仅验证域的所有权，还验证所有者的身份。这意味着可能会要求所有者提供个人身份证明文件以证明其身份。
扩展验证 Extended Validation:扩展验证是最高级别的验证。它包括验证域所有权、所有者身份以及业务注册证明。

### **主要区别：**

1. HTTP 协议以明文方式发送内容，数据都是未加密的，安全性较差。HTTPS 数据传输过程是加密的，安全性较好。
2. HTTP 和 HTTPS 使用的是完全不同的连接方式，用的端口也不一样，前者是 80 端口，后者是 443 端口。
3. HTTPS 协议需要到数字认证机构（Certificate Authority, CA)申请证书，一般需要一定的费用。
4. HTTP 页面响应比 HTTPS 快，主要因为 HTTP 使用 3 次握手建立连接，客户端和服务器需要握手 3 次，而 HTTPS 除了 TCP 的 3 次握手，还需要经历一个 SSL 协商过程。



### **HTTP/3了解吗？**

HTTP/3 是在 QUIC 基础上发展起来的，其底层使用 UDP 进行数据传输，上层仍然使用 HTTP/2。在 UDP 与 HTTP/2 之间存在一个 QUIC 层，其中 TLS 加密过程在该层进行处理。



### **HTTP 长连接短连接使用场景是什么？**

**长连接**：多用于操作频繁，点对点的通讯，而且客户端连接数目较少的情况。例如**即时通讯、网络游戏**等。
**短连接**：用户数目较多的Web网站的 HTTP 服务一般用短连接。例如**京东，淘宝这样的大型网站**一般客户端数量达到千万级甚至上亿，若采用长连接势必会使得服务端大量的资源被无效占用，所以一般使用的是短连接。



### **HTTP 是不保存状态的协议,如何保存用户状态？**

基于 Session 实现的会话保持优点：安全性高，因为状态信息保存在服务器端。缺点：由于大型网站往往采用的是分布式服务器，
基于 Cookie 实现的会话保持， 若遇到 Cookie 被禁用的情况，则可以通过重写 URL 的方式将会话标识放在 URL 的参数里，也可以实现会话保持。优点：服务器不用保存状态信息， 减轻服务器存储压力，同时便于服务端做水平拓展。缺点：该方式不够安全，因为状态信息存储在客户端。

### **Describe how a HTTP request is made and processed？**

首先通过DNS服务器把域名解析成IP地址，通过IP和子网掩码判断是否属于同一个子网构造应用层请求http报文，传输层添加TCP/UDP头部，网络层添加IP头部，数据链路层添加以太网协议头部数据经过路由器、交换机转发，最终达到目标服务器，目标服务器同样解析数据，最终拿到http报文，按照对应的程序的逻辑响应回去。

### **HTTPS 工作原理？**

用户通过浏览器请求https网站，服务器收到请求，选择浏览器支持的加密和hash算法，同时返回数字证书给浏览器，包含颁发机构、网址、公钥、证书有效期等信息。浏览器对证书的内容进行校验，如果有问题，则会有一个提示警告。否则，就生成一个随机数X，同时使用证书中的公钥进行加密，并且发送给服务器。服务器收到之后，使用私钥解密，得到随机数X，然后使用X对网页内容进行加密，返回给浏览器浏览器则使用X和之前约定的加密算法进行解密，得到最终的网页内容

### **什么是中间人攻击数字签名证书RSA加密过程？man-in-the-middle attack**.

A man-in-the-middle attack is a type of eavesdropping attack, where attackers interrupt an existing conversation or data transfer. After inserting themselves in the "middle" of the transfer, the attackers pretend to be both legitimate participants. This enables an attacker to intercept information and data from either party while also sending malicious links or other information to both legitimate participants in a way that might not be detected until it is too late.
Successful MITM execution has two distinct phases: interception and decryption.
Interception, The most common (and simplest) way of doing this is a passive attack in which an attacker makes free, malicious WiFi hotspots available to the public. IP spoofing, ARP spoofing, DNS spoofing.After interception, any two-way SSL traffic needs to be decrypted without alerting the user or application. HTTPS spoofing, SSL BEAST, SSL Hijacking, SSL stripping.

中间人 (MitM) 攻击是指攻击者拦截两方之间的通信以秘密窃听或修改在两者之间传输的流量。攻击者可能会使用中间人攻击来窃取登录凭据或个人信息、监视受害者或破坏通信或损坏数据。 MITM 执行有两个不同的阶段：拦截和解密。
预防：身份验证和篡改检测，不要在公共场所使用开放式公共 Wi-Fi 或 Wi-Fi 产品，使用 VPN 来帮助确保安全连接。网站运营商而言，安全通信协议（包括 TLS 和 HTTPS）通过对传输数据进行稳健的加密和身份验证来帮助减轻欺骗攻击。



 ### **对称加密和非对称的区别，非对称加密有哪些？**
加密和解密的过程不同：对称加密和解密过程使用同一个密钥；非对称加密中加密和解密采用公钥和私钥两个密钥，一般使用公钥进行加密，使用私钥进行解密。加密和解密的速度不同：对称加密和解密速度较快，当数据量比较大时适合使用；非对称加密和解密时间较长，速度相对较慢，适合少量数据传输的场景。传输的安全性不同：采用对称加密方式进行通信时，收发双方在数据传送前需要协定好密钥，而这个密钥还有可能被第三方窃听到的，一旦密钥泄漏，之后的通信就完全暴漏给攻击者了；非对称加密采用公钥加密和私钥解密的方式，其中私钥是基于不同的算法生成的随机数，公钥可以通过私钥通过一定的算法推导得出，并且私钥到公钥的推导过程是不可逆的，也就是说公钥无法反推导出私钥，即使攻击者窃听到传输的公钥，也无法正确解出数据，所以安全性较高。常见的非对称加密算法主要有：RSA、Elgamal、背包算法、Rabin、D-H 算法等等。



### **DDoS 有哪些，如何防范？**

DDoS 为分布式拒绝服务攻击，是指处于不同位置的多个攻击者同时向一个或数个目标发动攻击，或者一个攻击者控制了不同位置上的多台机器并利用这些机器对受害者同时实施攻击。DDoS 攻击主要有两种形式：流量攻击和资源耗尽攻击。



### **ARP 攻击有哪些，如何防范？**

在 ARP 的解析过程中，局域网上的任何一台主机如果接收到一个 ARP 应答报文，并不会去检测这个报文的真实性，而是直接记入自己的 ARP 缓存表中。并且这个 ARP 表是可以被更改的，当表中的某一列长时间不适使用，就会被删除。ARP 攻击就是利用了这一点，攻击者疯狂发送 ARP 报文，其源 MAC 地址为攻击者的 MAC 地址，而源 IP 地址为被攻击者的 IP 地址。通过不断发送这些伪造的 ARP 报文，让网络内部的所有主机和网关的 ARP 表中被攻击者的 IP 地址所对应的 MAC 地址为攻击者的 MAC 地址。这样所有发送给被攻击者的信息都会发送到攻击者的主机上，从而产生 ARP 欺骗。通常可以把 ARP 欺骗分为以下几种：
洪泛攻击，欺骗主机，欺骗网关，中间人攻击，IP 地址冲突