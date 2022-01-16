---
title: "Java Data Structure 11: Fault Tolerance Mechanism"
date: 2022-01-11T16:00:11+08:00
draft: true
images:
  - "/images/totoro.jpeg"
tags: 
  - Java Data Structure


---

**Fault tolerance mechanism: fail-over, fail-fast, fail-back and fail-safe**

四种容错机制：失效转移， 快速失效， 备份失效， 安全失效。

\1. Fail over：fail over
fail over的意思是“故障转移”，是一种备份操作模式。当主组件出现异常时，其功能转移到备用组件。关键是既有主备又有主备，主备故障时可以使能备，设置为主。比如在MySQL的双主模式下，当使用中的master出现故障时，可以将standby master作为master。

\2. Failfast：快速失败的
字面意思是“快速失败”。尝试找出系统中的错误，使系统按照预设的错误流程执行。对应的方式是“容错”。以Java collection的快速失败为例，当多个线程对同一个collection的内容进行操作时，可能会发生fail fast事件。例如：当一个线程a通过迭代器遍历一个集合时，如果该集合的内容被其他线程改变了；线程a访问集合时，会抛出并发修改异常（发现错误，执行设置错误的进程），并产生fail fast事件。

\3. Failback：故障切换后的自动恢复：在集群网络系统（两台或多台服务器互连的网络）中，由于需要修复一台服务器，需要将网络资源和服务临时重定向到备用系统。之后将网络资源和服务器恢复到原主机的过程称为自动恢复。

\4. Fail safe：fail safe
fail safe的意思是“故障安全”，即使在发生故障的情况下，也不会造成伤害或将伤害降到最低。维基百科上的一个图像示例是交通信号灯的“冲突监控模块”。当检测到错误或冲突信号时，路口的红绿灯将变为闪烁错误模式，而不是全部显示为绿灯。