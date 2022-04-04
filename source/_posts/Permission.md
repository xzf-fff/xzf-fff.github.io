---
layout: 解决git@github.com
title: Permission
date: 2022-04-04 20:19:17
tags:
---
客户端生成ssh key

ssh-keygen -t rsa -C "470812087@qq.com"
然后再终端下执行命令：

ssh -v git@github.com

在终端再执行以下命令

ssh-agent -s 

接着在执行

ssh-add ~/.ssh/id_rsa

出现Could not open a connection to your authentication agent.
这时可以使用：ssh-agent bash 命令，然后再次使用ssh-add ~/.ssh/id_rsa这个命令就没问题了。

配置服务端
打开你刚刚生成的id_rsa.pub，将里面的内容复制，进入你的github账号，在settings下，SSH and GPG keys下new SSH key，然后将id_rsa.pub里的内容复制到Key中，完成后Add SSH Key。

验证Key
ssh -T git@github.com 
