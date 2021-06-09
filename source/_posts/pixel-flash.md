---
title: Pixel-安卓系统刷机指南
top: false
cover: false
toc: true
mathjax: true
date: 2021-06-09 16:42:52
password:
summary:
tags:
- 系统
categories:
- 安卓
---
# 拉取aosp代码
``` 
repo init -u https://android.googlesource.com/platform/manifest -b android-10.0.0_r33
-b 后面的参数可见 tag and build
repo sync -j8
repo start master --all
```
# 下载厂商私有驱动，芯片相关bin
- [查找tag对应的build](https://source.android.com/setup/start/build-numbers#source-code-tags-and-builds)如下
  
  ![tag-build对应图](https://bytedance.feishu.cn/space/api/box/stream/download/asynccode/?code=NmM0NjU1ZjMyMzJmNzIwY2NmZjgyNTM0NGZkZDdkZjdfaVoxYjhmMzE0S2JBQW04ekRQNndWNnRJWjZreVpRM3dfVG9rZW46Ym94Y25XUXpacENEc0xCZ0xLQm1tZXpURjFiXzE2MjMyMjc1MTM6MTYyMzIzMTExM19WNA)
  
- [根据build找到hardware compoent](https://developers.google.com/android/images)

  ![hardware-compoent对应图](https://bytedance.feishu.cn/space/api/box/stream/download/asynccode/?code=MzNjODQyNGEzODA2ZmU2NmQyN2NhNGZiZTRmOTJjMWVfUmlkTFQ3UEVtT05UT2YwcXp5blFZaGdUN2d5ZTkwNUpfVG9rZW46Ym94Y25CSW9QNFB6QXhzOUtQR1NSWHVDQ09lXzE2MjMyMjc2MTg6MTYyMzIzMTIxOF9WNA)

- 下载hardware compoent的两个link，解压后为两个脚本

- 进入aosp根目录，执行解压的两个脚本

- 检查是否生成vendor目录，最终会变成vendor.img

# 给手机解锁

- 手机连接上google的网络

- 开发者选项打开oem解锁

- adb reboot fastboot

- fastboot flashing unlock

- 手机确认解锁即可

# 服务器编译成dist包的方式
## 编译代码
make dist -j8
编译产物为aosp_walleye-img-eng.wenda.zip

# [下载factory软件](https://developers.google.com/android/images#walleye)

![img](https://bytedance.feishu.cn/space/api/box/stream/download/asynccode/?code=ZGY4NDk1YjVkYjAxOWNmOTVjY2ZkZmZmOGFkYWIzMGJfamVrNEloNWxZcGQ0UmhKdWRPbXNjTXdjUlkxMm5nRmxfVG9rZW46Ym94Y25hSFV5N1dybEpkYmtZTkpOQlM0SzJjXzE2MjMyMjc4MTY6MTYyMzIzMTQxNl9WNA)

替换aosp_walleye-img-eng.wenda.zip
修改脚本flash-all.sh 为fastboot -w update aosp_walleye-img-eng.wenda.zip
# 刷写手机
adb reboot fastboot
执行flash-all.sh
# mac上直接编译的方式
## 编译代码
Lunch xxx
Make -j8
## 刷写手机
Cd aosp根目录
fastboot flashall -w
 
