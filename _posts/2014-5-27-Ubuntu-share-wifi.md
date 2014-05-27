---
category: Tools
layout: post
title: Ubuntu中创建一个Android手机能够识别的AP(hostapd和dnsmasq)
---

用Ubuntu系统自带功能创建AP操作是非常简单，但大多数Android手机都搜索不到它的信号，那是因为Android一般都不支持Ad-hoc模式的Wifi。为了在Ubuntu中创建一个Android手机能够识别的AP,下面向大家介绍另外一种方法： 

###1. 安装hostapd和dnsmasq两个软件
{% highlight ruby %} 
sudo apt-getinstall hostapd dnsmasq
{% endhighlight %} 

###2. 配置hostapd
打开/etc/hostapd.conf，里面有很多的可配置选项，其中大部分都已经用#来注释了。为了使得一些配置有效，我们要将一些配置前的#去掉，然后根据我们的需要去进行参数设置。要配置的选项和参数如下内容：
{% highlight ruby %} 
interface=wlan0
driver=nl80211
ssid=Ubuntu-wifi #设置wifi名称
hw_mode=g
channel=11
dtim_period=1
rts_threshold=2347
fragm_threshold=2346
macaddr_acl=0
auth_algs=3
ieee80211n=0

wpa=3 #以下是加密方法的设置，如果不要密码不用设置以下内容
wpa_passphrase=0123456789 #设置密码
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
{% endhighlight %} 

###3. 配置dnsmasq
打开/etc/dnsmasq.conf(如果没有这个文件，可以自己创建一个)，添加以下内容：
{% highlight ruby %} 
interface=wlan0
bind-interfaces #只监听wlan0
except-interface=lo
dhcp-range=192.168.1.100,192.168.1.254,12h #设置dhcp地址范围，即租借时间6小时
#address=/#/10.0.0.1 #如果你的配置中有这个，请注释掉，应为这个会把#(代表所有网址)的dns到10.1.1.1这个地址
dhcp-option=3,192.168.1.1 #为手机配置网关，要和dhcp-arange对应
dhcp-option=6,202.114.128.2 #为手机配置dns，可根据实际情况修改
{% endhighlight %} 

###4. 添加路由规则
可以使用iptalbes命令,也可用命令行的方式去添加路由规则，这里推荐使用脚本的方式，创建一个文件myap，添加如下内容：
{% highlight ruby %} 
#!/bin/sh
#为无线添加路由规则
iptables-F
iptables-X
iptables -t nat -F
iptables -t nat-X
iptables -t nat -APOSTROUTING -s 192.168.1.0/24 -o eth0 -jMASQUERADE
iptables -A FORWARD -s 192.168.1.0/24 -o eth0 -jACCEPT
iptables -A FORWARD -d 192.168.1.0/24-m conntrack --ctstateESTABLISHED,RELATED -i eth0 -jACCEPT
{% endhighlight %} 

添加完后，保存文件。为了使得文件具有可执行的属性，我们可以利用如下的命令去修改
{% highlight ruby %} 
sudo chmod a+x  myap
{% endhighlight %} 

说明：由于在上面我们将dhcp-range设置为192.168.1.100,192.168.1.254，也就是指定了wifi动态分配的地址范围为192.168.1.100至192.168.1.254，所以这里要配置路由规则的时候使用192.168.1.0。如果上面你的dhcp-range不是192.168.1.100,192.168.1.254，那么你的路由规则也要修改。

###5. 打开转发功能
打开文件/etc/sysctl.conf，找到net.ipv4.ip_forward=1，如果被注释了，要将其前面的注释去掉，以便使其生效。

###6. 启动AP
{% highlight ruby %} 
killallnamed #一般情况下bind的named会占了53端口，从而导致dnsmasq启动不了，所以要用killallnamed来杀了named再启动dnsmasq。
killallhostapd
ifconfig wlan0 192.168.1.1 #由于上面我们将dhcp-range设置为192.168.1.100,192.168.1.254，所以这里我们要将wlan0的ip设置为同一网段的ip。
hostapd-B/etc/hostapd.conf
/etc/init.d/dnsmasq restart #使用静态ip的朋友注意了，dnsmasq启动后会出现电脑突然上不了网，因为dnsmasq更了/etc/resolv.conf的原因。可以在/etc/resolv.conf加一行，执行命令echo"nameserver202.114.128.2">>/etc/resolv.conf即可。202.114.128.2是dns服务器，你可以根据你的当地的实际情况去修改。
echo1>/proc/sys/net/ipv4/ip_forward #启动转发功能
sudo./myap #如果myap不在当前路径下，要加路径
{% endhighlight %} 

至此，AP创建已经完成。打开手机扫描一下wifi，如果还不可以，建议重启一下电脑，再操作一次第6步。
