---
layout: post
title: TCPIP Illustrated--TCP
category: Basic
---

基本分层：链路层（SLIP，PPP，ARP，RARP），网络层（IP/ICMP/IGMP)，运输层（TCP/UDP)，应用层  
ARP和RARP用于转换IP地址和MAC地址，包装在IP包中。  
ICMP和IGMP也都是用IP包发送。PING是利用的ICMP，  
路由搜索顺序：匹配IP地址，匹配网络号，匹配default  
路由表：netstat -rn，其中 U表示可以使用，G表示下一个是网关，H表示是到主机，D表示重定向而创建，M表示被重定向报文修改  
应用程序应该关注IP报文段长度，因为UDP不主动分片，而TCP试图避免分片  
DNS域名系统：顶级域被分为三个部分，1）arpa是一个用作地址到名字的转换，用于指针查询，例如根 33.13.252.140.in-addr.  arpa，2)7个三长度的普通域；3）国家代码  


TCP  
建立链接用3次握手，拆连接用4次握手。需要用到2MSL等待状态，等待期间端口能否被重用用设置 SO_REUSEADDR  
经受时延确认：即捎带确认  
小数据：Nagel算法：为了避免微小分组可能增加阻塞的问题，规定一个TCP连接上最多只能有一个未被确认的未完成的小分组，可以用 TCP_NODELAY关闭  
慢启动：指数级增加  
拥塞避免：增加慢启动门限ssthresh，超过后加法增加。发生超时时反应剧烈，ssthresh=cwnd/2，cwnd=1，进入慢启动  
快速重传: 收到3个相同ack时，cwnd=ssthresh+3  
快速恢复：发送方收到一个重复的ACK，那么根据TCP的ACK机制就表明有一个数据包离开了网络，于是cwnd加1。因此在快速回复的基础上，每次收到重复ACK时, 拥塞窗口加1
