---
title: Git 使用方法小总结
date: 2020-07-06 22:28:27
tags: [Git]

---

Github由于DNS污染的原因，经常clone的速度不到10 kb/s，难以忍受。有时候要设置Git Clone的代理，又得上网搜索一番，这里就简单记录一下设置代理的过程，省去自己搜索的过程。

## 使用代理

首先得保证你有梯子能够正常访问Google，这样才可以配置Git通过代理访问，一般来说v2ray的全局模式是对git clone没有用的，git 命令并不走全局代理，需要额外在git config中配置

```
# 让所有git clone命令走代理
# socks5协议，1080端口修改成自己的本地代理端口
git config --global http.proxy ``socks5://127.0.0.1:1080`` 
git config --global https.proxy ``socks5://127.0.0.1:1080`` 

# http协议，1081端口修改成自己的本地代理端口
git config --global http.proxy ``http://127.0.0.1:1081 ``
git config --global https.proxy  ``https://127.0.0.1:1081 ``
```

以上配置会使得所有git命令走代理，包括国内的git仓库，有可能拖慢国内Git命令，甚至局域网内的操作。

因此建议仅针对Github进行配置，让Github走代理，不影响其他仓库的操作。

```
# socks5协议，1080端口修改成自己的本地代理端口
git config --global http.https://github.com.proxy socks5://127.0.0.1:1080 
git config --global https.https://github.com.proxy socks5://127.0.0.1:1080 

# http协议，1081端口修改成自己的本地代理端口
git config --global http.https://github.com.proxy ``https://127.0.0.1:1081`` 
git config --global https.https://github.com.proxy ``https://127.0.0.1:1081`` 
```

其他Git配置命令

```
# 查看所有配置
git config -l
# reset 代理设置
git config --global --unset http.proxy
git config --global --unset https.proxy
```

## Git分支合并

```
git checkout 你的分支
git merge 想要合并的分支
```

