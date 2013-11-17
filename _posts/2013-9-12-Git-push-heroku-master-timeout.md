---
category: Tools
layout: post
title: 通过Git将应用程序推送到Heroku失败解决办法
---

今天尝试'git push heroku master'的时候一直出现：

    ssh: connect to host heroku.com port 22: Bad file number
    fatal: The remote end hung up unexpectedly

百度查找原因，在Ruby-China中发现如下两个帖子：

[Heroku push timeout 错误，折腾半天，已解决。Fuck GFW!!!](http://ruby-china.org/topics/10813)

[求教 Heroku 不能 push 的问题：port22](http://ruby-china.org/topics/11097)

都提到在'$ vi ~/.ssh/config'中更改配置，实际上，我在这个路径下就没有找到对应config文件。

参考上面两篇文章一些办法，最后我是这样解决的：

* 使用'ssh -v git@heroku.com'命令，找出sshconfig文件具体路径

      debug1: Reading configuration data /etc/ssh/ssh_config

* 使用'sudo gedit /etc/ssh/ssh_config'打开文件，增加如下内容

      Host heroku.com
      User yourusername
      Hostname proxy.heroku.com
      PreferredAuthentications publickey
      IdentityFile ~/.ssh/id_rsa
      port 22

说明：不设置这步，就不会挖出很多IP，你也就找不到可用节点。

* 再使用'ssh -v git@heroku.com'命令，找出可用节点，我这里找到IP是107.21.99.190

* 再使用'sudo gedit /etc/ssh/ssh_config'打开文件，修改配置

      Host heroku.com
      User yourusername
      Hostname 107.21.99.190 
      PreferredAuthentications publickey
      IdentityFile ~/.ssh/id_rsa
      port 22

说明：用具体IP代替proxy.heroku.com是最关键一步。

完成以上处理，就可以通过Git把应用程序推送到Heroku～_～







    















