Ragnarok 0.1 BETA C# Rebuild
===========

加密聊天器

服务端 
------
Ragnarok_server\server.py 

python3.6.4

### 说明

考虑到很多宽带都是NAT的内网，所以通过公网小鸡桥接。

服务端只做用户合法性验证和双向搭桥，可以放在国内小鸡上。

有一根长长的网线，一直伸到你家里，你说什么做什么他们都知道的一清二楚。

于是我决定写这玩意，名字随便起的。再也不用担心被视奸了

### 设置
在config里改小鸡的公网IP和端口，对linux了解不太多，所以怎么在服务器上运行还请dalao写个shell加进来（写了个实验版后台shell）


聊天模块
------
Ragnarok_C#

### 使用环境
请使用正版 win10 64bit 1709 (16299.248)

.NET Framework 4.7.1 

VS2017


### 设置
UserID：你自己的代号,仅限大小写字母和数字

TargetID：你想和谁说悄悄话

Local_IP：本机的网口IP4，内网一般是192.168.xxx.xxx（不是网页查出来的公网IP）

Local_Port：0-65535

Target_IP：小鸡的公网IP

Target_Port：服务器监听端口

### 使用

先设置参数，再保存，再连接服务器，两个客户端都连上服务器以后，就可以开始网上冲浪了。

### 加密特性
C#重构的客户端，加密逻辑完全重写

大概阐述一下逻辑：

客户端A先行连接服务器，获得主动权。

|客户端A|    ---连接--→  |服务端|  ←--断开---     |客户端B|

|客户端A|    ---等待----   |服务端|     ←--断开---     |客户端B|

|客户端A|    ---等待----   |服务端|     ←--连接---     |客户端B|

|客户端A|    ←--桥接---   |服务端|     ---桥接--→     |客户端B|

|客户端A|    ---A公钥--→   |服务端|     ←--B公钥---     |客户端B|

|客户端A|    ←--B公钥---   |服务端|     ---A公钥--→     |客户端B|

|客户端A|     -AESkey→   |服务端|      -AESkey→     |客户端B|

|客户端A|     ---密文--→   |服务端|     ---密文--→     |客户端B|

客户端A用B公钥加密AESkey，返回客户端B，客户端B私钥解密得到AESkey

通信双方用客户端A产生的AESkey进行通信。

我就不吹有多保密了（量子计算机出来之前，谁都看不到你们说了什么悄悄话）但是有一些人为因素问题后面说。



人为因素
------
中间人攻击是个目前没有什么解决办法的事情，所以才有了CA去保证RSA公钥的可靠。一个程序中，最薄弱的环节是人。最迫不得已的办法，显示接收到的秘钥以便在旁路（线下py交易，企鹅vx）上进行公钥可靠性的确认。不过不干坏事也不会招致高科技的中间人攻击……技术无罪。

另外考虑到社工的问题，ID最好不要起自己喜欢的一些字段。因为和服务器交换ID的时候是明文，可能是个隐患。


一点小小的心愿
-----
历时一个月从什么都不懂，到开始盲人摸python，到撸出来这个程序。今天算是瞎猫撞上死耗子撸出来了，差点弃坑。有的时候比较喜欢大开脑洞，比如2100年的一个晚上，K摘下了手表眼睛手机，带着一张写满英文数字的纸条出门了。在一个小巷和一个老哥擦肩而过的时候，仿佛手里的纸条有一点点的不一样。回到家，拿出爷爷的信仰阿苏斯笔记本，打开了Ragnarok，进入了这个cyberpunk时代最后的世外桃源。

没有C#大佬，我就自己动手丰衣足食吧。安装和使用都会更方便。不过命令行更有黑客的感觉，做人不装逼，和咸鱼有什么区别。

做了个文件传输以后，我实在是想不出来还有什么拓展性，如果各位大佬有什么好的建议请fork或者留言

更新信息
------

0.1.0 Beta C# Rebuild :梦回OICQ。

0.2.1 Beta : 一些标准化异常处理

0.2.0 Beta : 加入AES字节流文件加密传输端

0.1.0 Beta ：第一版实现了非对称加密文字流互换
