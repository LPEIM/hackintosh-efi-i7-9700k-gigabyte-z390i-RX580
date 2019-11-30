# hackintosh-efi-i7-9700k-gigabyte-z390i-RX580

注：EFI不完整，kexts文件夹已完善。

## 电脑配置
 
| 配置 | 型号 |
| :---- | :---- |
| CPU | i7-9700k |
| 主板 | Gigabyte Z390 I AORUS PRO WIFI |
| 内存 | 海盗船ddr4 3000 16G |
| 硬盘 | 三星970 EVO 500G (For Win) |
| 硬盘 | 三星860 EVO 500G (For Mac) |
| 显卡 | 蓝宝石 RX580 8G极光版（2304sp） |
| 网卡 | BCM943602CS + m2 ssd转接板 |
| 电源 | 海盗船rm650x |
| 散热 | 安钛克海王星240ARGB水冷 |
| 机箱 | 追风者215ptg |

注：技嘉z390i主板的板载网卡接口为cnvi接口，不支持更换为黑苹果的网卡（网传，华擎和华硕的主板可直接更换板载网卡）。

解决方案：牺牲一个m2接口，用来插网卡。

## kexts文件夹

|  文件  | 文件  |
|  ----  | ----  |
| Lilu | 一个开源的内核扩展补丁驱动文件，可以为任意kext驱动提供补丁 |
| VirtualSMC | 是仿冒苹果SMC设备的驱动文件，就是欺骗苹果系统，让它相信我们的设备是Mac。不能和FakeSMC同时存在 |
| XHCI-300-series-injector | 英特尔300系列主板驱动 |
| WhateverGreen | 一款修复黑苹果AMD/NVIDIA显卡黑屏、花屏、睡眠黑评估等各种问题显卡驱动补丁，依赖于lilu.kext |
| IntelMausiEthernet | Intel有线网卡驱动程序，适用于Intel主板自带的黑苹果网卡驱动程序，支持大部分网卡型号 |
| GenericUSBXHCI | 适用于黑苹果OS X EI Capitan 10.11.x以上系统的USB3.0驱动 |
| USBInjectAll | 可以帮助黑苹果驱动你的USB设备，包括3.0的端口和摄像头等问题 |
| CPUFriend | CPU电源动态管理， 需要与CPUFriendDataProvider配合使用|
| AppleALC | 用来驱动声卡 |
| HoRNDIS | 让Mac通过Android USB tethering上网 |

CPUFriend：[https://github.com/acidanthera/CPUFriend](https://github.com/acidanthera/CPUFriend)，CPUFriendDataProvider.kext可以通过以下命令生成，

```shell
./ResourceConverter.sh --kext /System/Library/Extensions/IOPlatformPluginFamily.kext/Contents/PlugIns/X86PlatformPlugin.kext/Contents/Resources/Mac-CAD6701F7CEA0921.plist
```

## 须知

技嘉主板z390i自带蓝牙和wifi，且技嘉bios中无法关闭蓝牙。故在使用BCM943602CS时，会与板载蓝牙发生冲突，故需要屏蔽板载蓝牙。

解决方案：

1. 物理方式：拆除板载蓝牙和wifi模块。

2. 软件方式：可在Hackintool中查看，定制屏蔽对应USB口（一般连接速度为12Mbps，我的端口为14）。
