
1、 URL访问网站的整个过程
http://blog.csdn.net/gs_008/article/details/50976483

2、所使用到的协议
一个HTTP请求的所有协议: arp (电脑刚刚接上下一跳获取下一跳mac地址--广播), UDP/TCP，基于IP协议--（DNS协议）、TCP建立连接、HTTP（GET请求）

（上层封装DNS报文(TCP/udp),再封装IP,以太层-无ARP缓存。发送时如果ARP缓存中没有相关数据，则发送ARP广播请求，等待ARP回应；）。开始转发。


