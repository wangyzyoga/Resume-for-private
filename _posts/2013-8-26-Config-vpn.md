---
category: Tools
layout: post
title: Ubuntu12.04中配置VPN
---

今天想在Ubuntu上使用VPN，看到网上很多人谈到如何配置，很多都写的相当复杂，看的我一直犯迷糊。最后终于找到一篇简单明了说明，成功指导我完成VPN配置。在此将自己的配置过程记录下来，分享给需要的人。

###1 配置 VPN

单击屏幕左上角 Network Connections 标志，在下拉选项里单击 "VPN Connections"，单击 "Configure VPN..." 进入 VPN 的设置。

###2 添加 VPN

点击 "VPN" 菜单下右侧的 "Add" 按钮，添加 VPN 服务。

###3 选择 VPN 类型

我电脑上只有 "Point-to-Point Tunneling Protocol (PPTP)"，选择后点击 "Create..." 按钮。

###4 填写 VPN 信息

"Connection name"栏中填入“VPN (PPTP)”；"Gateway"中填入服务器域名；"User name"中填入你的VPN帐号用户名；"Password"中填入你的VPN帐号密码；最后点击"Advanced..."按钮。
 
###5 PPTP 高级选项

选中 "Use Point-to-Point encryption (MPPE)"，点击 "OK" 按钮。

###6 保存 VPN

点击 "Save..." 按钮。

###7 连接 VPN

单击 "VPN Connections" 下的“VPN (PPTP)”，就是之前填写的Connection name，开始连接 VPN。

###8 连接成功

VPN 连接成功后系统会有提示信息，同时 Network Connections 上会有小锁的标志。如果提示连接失败，重新执行上一步连接 VPN，应该就成功了。







