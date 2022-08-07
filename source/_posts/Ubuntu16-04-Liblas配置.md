---
title: Ubuntu16.04 libLAS配置
date: 2020-05-24 14:29:20
tags: [Ubuntu,libLAS]
---

Ubuntu16.04这个版本虽然教程多，但是网上大多数的教程都过于老旧，在这里记录一下我的配置libLAS的过程。

## 需要安装的库

这里为我设备上还需要安装的库，不一定都适用

- CMake

- Boost 1.38.0及以上

  apt安装即可

``` Ubuntu
sudo apt-get install libboost-all-dev
```

- Geotiff

  apt安装

``` Ubuntu
sudo apt-get install libgeotiff-dev
```

## libLAS

下载地址：[libLAS](https://liblas.org/download.html)

### 解压并安装

``` Ubuntu
tar -zxvf libLAS-1.8.1-src.tar.bz2
cd liblas
mkdir makefiles
cmake ..
make
make install
/// 可能需要root权限
sudo /sbin/ldconfig
```

### 测试

``` 
lasinfo ..test/data/TO_core_last_clip.las
```

有输出点云即安装完成