---
title: Airbnb Clone with React
date: 2020-08-09 22:45:45
tags: [React]
---

本文是根据Ben Awad的React教学视频逐步学习制作而成的，旨在记录自己的学习过程和心得，将陆续更新进展。

- 安装环境为Windows 10
- Postgre 12
- redis
- Typescript

## 遇到的问题

- Ben Awad的教程的环境为Mac，package.json的scripts配置与Windows不太一样

```json
"scripts": {
    "start": "set NODE_ENV=development&&nodemon --exec ts-node src/index.ts",
    "test": "set NODE_ENV=test&&jest --watch",
    "gen-schema-types": "ts-node src/scripts/createTypes.ts"
  },
```

- 教程为18年的，现在如果安装的PostgreSQL的版本较高的话，得选用新的TypeORM

```json
"typeorm": "0.2.25",
```

- PostgreSQL 第一次安装没有带数据库，重新安装一次
- yarn start的时候提示Server内的package.json里的jest版本过旧，修改package.json里的版本重新install即可
- 根据教程安装后的web app 里面没有 tsconfig.json, 即没有 typescript
- 教程使用的antd版本为3.6.2，不是现有版本4，组件用法与现在的用法不太一致，修改package.json里的版本重新安装即可

## PostgreSQL 的安装

https://ken.io/note/centos7-postgresql12-install-and-configuration 

## Redis的安装和启动

在GitHub上下载Redis.msi 直接安装

启动的话需要在Redis安装目录下，启动CMD

``` 
redis-server.exe redis-windos.conf
```

如果先前安装的时候有勾选服务的选项，就可以直接关闭小黑窗了。

可以在CMD里执行redis-cli看redis服务是否在运行。

## 开始React

### 安装React Cli

```
npm -g install create-react-app
```

然后选择合适的文件夹，在CMD里运行

```
create-react-app --scripts-version=react-scripts-ts
cd my-app/
npm start
```

上述是官方的教程，这样就有了React的环境，但是这个教程有个问题

使用这个方法创建的app里面并没有 tsconfig.json，也就是typescript的项目描述文件

在网上稍加搜索，看到了这样的操作

1. 重新创建项目

```
npm uninstall -g create-react-app // 卸载通过npm install -g create-react-app 安装的app
npx create-react-app my-app --typescript
```

2. 手动配置添加typescript

[一个Github的issue](https://github.com/lizhongzhen11/dailyGain/issues/36 )这个链接提及到如何配置

### 配置Apollo

使用GraphQL