---
title: 安卓代码拉取
top: false
cover: false
toc: true
mathjax: true
date: 2021-06-9 13:27:31
password:
summary:
tags:
- 博客
categories:
- 随笔
---

# 拉取aosp代码
```cpp
repo init -u https://android.googlesource.com/platform/manifest -b android-10.0.0_r33
-b 后面的参数可见 tag and build
repo sync -j8
repo start master --all
```
# 下载厂商私有驱动，芯片相关bin
[查找tag对应的build](https://source.android.com/setup/start/build-numbers#source-code-tags-and-builds "查找tag对应的build")如下
