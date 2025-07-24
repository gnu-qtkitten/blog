---
title: "[折腾记]记一次折腾记录——移动牌光猫获取超级密码以及改桥接教程"
date: 2025-07-03 19:44:33
tags:
---
## 免责声明
这两天手欠，看家里的移动光猫不爽，所以想要改桥接，以下是仅我自己折腾的过程，折腾有风险，需要一定的计算机知识，有问题评论见，若稚问题概不回答
我的教程亲测可以用于H3-8s和HX5-9sLite，其它型号应该也行，折腾有风险，操作需谨慎（部分图片来自网络）
## 正文
首先，我们先登录光猫的管理页面
![登录光猫的管理页面](res/a7862cae09ede5174c40d4c14df39767651012210.jpg@1192w.avif)
然后输入以下网址 http://[光猫IP]/usr=CMCCAdmin&psw=aDm8H%25MdA&cmd=1&telnet.gch
此时，你会看到大大的TelnetSet Success，那么你成功开启了telnet
我们在找一个telnet客户端，android设备装termux或者电脑都可以，然后输入
```shell
telnet 192.168.1.1
```
用户名CMCCAdmin密码aDm8H%MdA
成功后会有一个shell的提示符
然后，坑就来了。直接看的话是星号，如果按照网上改密码的方法，你就在也别想登陆了，所以我们把它拷出来在读取
```shell
sidbg 1 DB p DevAuthInfo 
sidbg 1 DB decry /userconfig/cfg/db_user_cfg.xml 
cd /tmp 
vi debug-decry-cfg 
```
```vim
:/DevAuthInfo
```
然后我们就可以轻松获取密码
然后拿着这个用户名密码在去登录web控制台，你会发现这里发生了些许微妙的变化
![web控制台](res/2ac0bf0dcde34f8f27bd07370f710b4b651012210.jpg@1192w.avif)
按照图上的顺序进行修改2处先调到有internet字样的选项，记录3处所有配置然后把2处改为新建WAN连接，5处改为Bridge桥模式，将3处修改的和原来一样，将路由器连接的端口勾上，最后不要忘了保存
然后手机打开移动应用，查看宽带账号，修改密码（直接忘记密码用短信验证码重置就行）
![移动应用](res/7fada143ff6450382ebca8cc950777f6651012210.jpg@1192w.avif)
再登录路由器，此时无法上网
![路由器](res/e0246db75fba89d2df4cb09df6d53bdc651012210.jpg@1192w.avif)
把上网模式改为拨号上网（PPPoE）然后输入移动app中宽带账号和密码，最后保存
此时路由器会开始拨号，稍后就可以上网了~
