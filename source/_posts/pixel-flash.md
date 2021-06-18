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

![](https://bytedance.feishu.cn/space/api/box/stream/download/asynccode/?code=MTllYjY4Mjk5ZTYzMWEwMjMyMGU4OTllZjRjYmU0YWRfeFhWQ2lJbk9NNldreUVUZnhEOEpReThBM204ZUgwa2NfVG9rZW46Ym94Y25XUXpacENEc0xCZ0xLQm1tZXpURjFiXzE2MjQwMDYxNTg6MTYyNDAwOTc1OF9WNA)

- [根据build找到hardware compoent](https://developers.google.com/android/drivers#walleyeqq2a.200405.005)

![](https://bytedance.feishu.cn/space/api/box/stream/download/asynccode/?code=MmEzMTZkZTZhZWI2NDM1YzI1MDQ5ZjA2OTNhODcxMjNfSXBaOWdwUVZmU2lQcWk1U3VGa21hUDJ2Tlh1U05SOTRfVG9rZW46Ym94Y25CSW9QNFB6QXhzOUtQR1NSWHVDQ09lXzE2MjQwMDYxNTg6MTYyNDAwOTc1OF9WNA)

- 下载hardware compoent的两个link，解压生成两个脚本
- 进入aosp根目录，执行解压的两个脚本，并检查是否生成vendor目录，最终会生成vendor.img

# 解锁手机

- 手机连接上google的网络
- 开发者选项打开oem解锁

![](https://bytedance.feishu.cn/space/api/box/stream/download/asynccode/?code=MDFiNDQ4OTA5ZWMwMjBlNmQzMWExYjdmYWQ0ZWNlNjhfSXQxV0xUd3NwM3M3aXk1djdYSDEyeDdpb3V0N0l1bFdfVG9rZW46Ym94Y25yOXJMSTdJTnZnRGFnbHh6R2VtbkRjXzE2MjQwMDYxNTg6MTYyNDAwOTc1OF9WNA)

```
adb reboot fastboot 让手机进入bootloader

fastboot flashing unlock
```

# 编译刷写

## mac本地编译刷写

```
Lunch xxx

Make -j8

adb reboot fastboot 让手机进入bootloader

Cd aosp根目录

fastboot flashall -w
```

## 服务器编译成dist包进行刷写

- `make dist -j8`，得到编译产物为aosp_walleye-img-eng.wenda.zip
- [下载factory软件](https://developers.google.com/android/images#walleye)得到flash-all.sh，并修改脚本为fastboot -w update aosp_walleye-img-eng.wenda.zip

![](https://bytedance.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDg3MmMyMTU5OGI3MDk2ZDAzMWEyM2FiMjU3YzgwODdfY1pxMjA1Z1pXT2F2enM0T1RXSFJCbGIzdUNNV3ZEdmNfVG9rZW46Ym94Y25hSFV5N1dybEpkYmtZTkpOQlM0SzJjXzE2MjQwMDYxNTg6MTYyNDAwOTc1OF9WNA)

- adb reboot fastboot让手机进入bootloader
- 执行flash-all.sh刷写手机
