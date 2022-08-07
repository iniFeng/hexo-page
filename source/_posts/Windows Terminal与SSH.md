---
title: Windows Terminal与SSH
date: 2021-09-20 18:12:02
tags: [Window Terminal, Tips]
---

最近新装了电脑，需要重新迁移一下Hexo Blog。Hexo使用起来很便利，但是迁移环境的时候往往需要将本地的文件保存下来，通过U盘或者云存储转移整个Hexo项目，如果有更方便的方法，比如把项目直接上传至GitHub，或者直接能从GitHub Pages的项目中恢复Hexo项目的话，当我没说。  
Anyway，我现在需要重新配置一次Node环境和恢复先前的Hexo项目。挺久没更新了，刚好可以写篇文章水一下。

## 配置Node、Git环境
这部分的话，我算是配环境老手了。这次既然要重新装了环境，我就打算用NVM安装Node，顺带实现Node版本的管理，Git的话直接官网下载就可以了。  
在Windows下安装NVM就没有像Mac那么麻烦了，在Mac安装NVM上踩了不少的坑......
Windows下只要在这个GitHub项目 [nvm-windows](https://github.com/coreybutler/nvm-windows) 下下载nvm-setup，直接安装即可。  
需要注意的是，安装的文件目录名里不要有空格和中文字符，不然容易报错或者Terminal显示乱码。  
安装cnpm
```
npm install -g cnpm --registry=https://registry.npm.taobao.org //不然node_modules 下载太慢
cnpm install hexo-cli -g //全局安装hexo
```
在我使用Windows Terminal，执行上述cnpm安装指令时，terminal 报了一个错误  
```
set-ExecutionPolicy RemoteSigned
```
这个时候需要使用管理员身份，打开PowerShell，输入
```
set-ExecutionPolicy RemoteSigned
```
再继续执行


## 恢复先前的Hexo项目
因为装机时CPU出了点问题，我排查问题的时候就重装了系统，导致磁盘里的Hexo项目没有保存下来。所幸的是OneDrive上刚好保存了我放在桌面文件夹下的Hexo项目。我将项目底下的node_modules(200+MB)删除之后，整个项目的大小大概在60MB左右，即使是这样，OneDrive也依然下载了快二十分钟。这个速度无愧于我对OneDrive的认知。  
使用cnpm安装之后，整个项目就恢复如初，和以前一样了。

## Windows Terminal
我可喜欢这个东西了，比CMD和PowerShell好看多了，而且还支持WSL和多种颜色主题，配环境爱好者狂喜。  

Windows Terminal 微软商店里直接安装就好了，方便快捷。

和VS Code 相似，Windows Terminal也有个JSON形式的配置文件。 在终端的Tab栏上的小三角，点开有个设置，设置界面左下角有一个打开JSON文件，在里面可以随意配置自己想要的界面主题，或者是快捷打开方式。  

我这里就简单配置了毛玻璃特效和在文件管理器的地址栏里输入wt打开当前文件夹目录的Terminal，配置如下：

```
"defaults": {
   // Put settings here that you want to apply to all profiles.
            "useAcrylic": true, // 启用毛玻璃
            "acrylicOpacity": 0.6, // useAcrylic 设置为 true 时，设置透明度，接受 0-1 之间的浮点值
            "startingDirectory": "." //打开当前文件夹目录的Terminal
        },
```

## Windows配置SSH

既然换了电脑，远程服务器的SSH也需要重新配置一下了  

首先先生成一个新的rsa公钥私钥，默认生成在用户目录的.ssh文件夹下

```
ssh-keygen -t rsa -c
```

然后在服务器的/root/.ssh/authorized_keys里添加id_rsa.pub里的内容。这样之后，就可以直接在Windows Terminal直接使用SSH命令连接到远程服务器(前提是安装了Open-SSH)。  

不过这时候连接服务器的命令可能是长这样：

```
ssh root@xxx.xxx.xxx.xxx
```

还需要自己记下服务器的IP地址，也太麻烦了吧。

那肯定不需要那么麻烦，还是有办法给服务器设置别名的。  

在Windows用户目录的.ssh文件夹下，创建一个config文件，注意不要有后缀名，在里面编辑这些信息：

```
Host 服务器别名
HostName 服务器IP地址
User 连接服务器的用户，比如root
Port 22 SSH端口
```

设置好之后，就不需要自己手动打IP地址连接了，用了这个方法我都可以把Putty卸载了，相见恨晚。

``` 
ssh 服务器别名
```

## 尾声

随便水了这篇文章，也是同时想看看我的Hexo Blog恢复了没有，如果恢复了的话，应该是可以在我的Github Pages上看到这篇文章。之后再研究看看如何通过Github hooks 或者Action，将文章更新消息同步推送到Telegram里面。有缘再去试看看，也不知道下次更新啥时候了，嘻嘻。

