---
title: Hello Hexo
date: 2020-05-03 20:09:26
tags: [Hexo, Fluid]
---
这是我部署在VPS上的基于Hexo框架+Fluid主题的个人博客。原本想着自己建个简单的个人博客，用什么框架好呢，看到知乎上有人推荐Hexo，以及Hexo的Fluid这个Material Design的主题很对我的胃口，就决定是它了！

Hexo是使用Git来更新页面和发表文章的静态页面，本身很适合用Github Pages来作为载体，但是我觉得Github Pages连接方面不是很稳定，而且手头刚好有闲置的VPS和域名，就想把博客移植至到VPS上，过程也很简单，相当于在VPS上建了个Git私有库。

作为第一篇博客，就在这里记录一下建站的心路历程吧！

## 搭建步骤

- Git
- Node.js
- Hexo
- Fluid主题
- Gulp压缩静态资源
- VPS环境构建:
  - Git私有库
  - 创建git用户并设置用户的SSH
  - Nginx

## 参考链接

网上关于Hexo的搭建和部署教程已经很多了，这里就放一些自己搭建时参考的教程。

- [环境搭建](https://zhuanlan.zhihu.com/p/82437065 )

- [Fluid主题](https://fluid-dev.github.io/hexo-fluid-docs/ )
- [Gulp压缩静态资源](https://www.voidking.com/dev-hexo-gulp/ )