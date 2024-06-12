# [OpenWrt-Docker](https://github.com/SuLingGG/OpenWrt-Docker)

[![GitHub Stars](https://img.shields.io/github/stars/SuLingGG/OpenWrt-Rpi-Docker.svg?style=flat-square&label=Stars&logo=github)](https://github.com/SuLingGG/OpenWrt-Rpi-Docker/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/SuLingGG/OpenWrt-Rpi-Docker.svg?style=flat-square&label=Forks&logo=github)](https://github.com/SuLingGG/OpenWrt-Rpi-Docker/fork)
[![Docker Stars](https://img.shields.io/docker/stars/sulinggg/openwrt.svg?style=flat-square&label=Stars&logo=docker)](https://hub.docker.com/r/sulinggg/openwrt)
[![Docker Pulls](https://img.shields.io/docker/pulls/sulinggg/openwrt.svg?style=flat-square&label=Pulls&logo=docker&color=orange)](https://hub.docker.com/r/sulinggg/openwrt)

本项目旨在构建适用于树莓派 1~4 、适用于 armv6/armv7/armv8(aarch64)/x86_64(amd64) 平台设备的 OpenWrt 镜像 (每日更新)。

Github: <https://github.com/SuLingGG/OpenWrt-Docker>

DockerHub: <https://hub.docker.com/r/sulinggg/openwrt>

## 支持设备及镜像版本

本项目基于 [immortalwrt: openwrt-18.06-k5.4](https://github.com/immortalwrt/immortalwrt/tree/openwrt-18.06-k5.4)，每日上午 8 点编译 OpenWrt 镜像，镜像构建完成后将同时推送到 [DockerHub](https://hub.docker.com/r/sulinggg/openwrt) 和 阿里云镜像仓库 (上海) 。

对于国内用户，为提高镜像拉取体验，可以考虑拉取存放于阿里云镜像仓库的镜像，镜像名称及标签如下表所示:

### OpenWrt 标准镜像

OpenWrt 标准镜像为集成常用软件包的 Docker 镜像，镜像自带软件包可满足大多数情景下的使用需求。

|  支持设备/平台  |        DockerHub        |                  阿里云镜像仓库 (上海)                  |
| :-------------: | :---------------------: | :-----------------------------------------------------: |
|    树莓派 1B    |  sulinggg/openwrt:rpi1  |  registry.cn-shanghai.aliyuncs.com/suling/openwrt:rpi1  |
|    树莓派 2B    |  sulinggg/openwrt:rpi2  |  registry.cn-shanghai.aliyuncs.com/suling/openwrt:rpi2  |
| 树莓派 3B / 3B+ |  sulinggg/openwrt:rpi3  |  registry.cn-shanghai.aliyuncs.com/suling/openwrt:rpi3  |
|    树莓派 4B    |  sulinggg/openwrt:rpi4  |  registry.cn-shanghai.aliyuncs.com/suling/openwrt:rpi4  |
|      armv7      | sulinggg/openwrt:armv7  | registry.cn-shanghai.aliyuncs.com/suling/openwrt:armv7  |
|  arm8/aarch64   | sulinggg/openwrt:armv8  | registry.cn-shanghai.aliyuncs.com/suling/openwrt:armv8  |
|  x86_64/amd64   | sulinggg/openwrt:x86_64 | registry.cn-shanghai.aliyuncs.com/suling/openwrt:x86_64 |

### OpenWrt-Mini 镜像

OpenWrt-Mni 镜像为几乎未添加额外软件包的 Docker 镜像，你可以自行通过 opkg 安装你需要的软件包。

|  支持设备/平台  |        DockerHub        |                  阿里云镜像仓库 (上海)                  |
| :-------------: | :---------------------: | :-----------------------------------------------------: |
|    树莓派 1B    |  sulinggg/openwrt-mini:rpi1  |  registry.cn-shanghai.aliyuncs.com/suling/openwrt-mini:rpi1  |
|    树莓派 2B    |  sulinggg/openwrt-mini:rpi2  |  registry.cn-shanghai.aliyuncs.com/suling/openwrt-mini:rpi2  |
| 树莓派 3B / 3B+ |  sulinggg/openwrt-mini:rpi3  |  registry.cn-shanghai.aliyuncs.com/suling/openwrt-mini:rpi3  |
|    树莓派 4B    |  sulinggg/openwrt-mini:rpi4  |  registry.cn-shanghai.aliyuncs.com/suling/openwrt-mini:rpi4  |
|      armv7      | sulinggg/openwrt-mini:armv7  | registry.cn-shanghai.aliyuncs.com/suling/openwrt-mini:armv7  |
|  arm8/aarch64   | sulinggg/openwrt-mini:armv8  | registry.cn-shanghai.aliyuncs.com/suling/openwrt-mini:armv8  |
|  x86_64/amd64   | sulinggg/openwrt-mini:x86_64 | registry.cn-shanghai.aliyuncs.com/suling/openwrt-mini:x86_64 |

## 注意事项

- 其中，树莓派 2B 镜像同时适用于 2B/3B/3B+/4B 。 
- 若拉取镜像时不加任何标签，则将使用 latest 标签拉取镜像，latest 指向的镜像与树莓派 2B 镜像实际上为同一镜像。
- 镜像中软件包的集成情况基本上与 [SuLingGG/OpenWrt-Rpi](SuLingGG/OpenWrt-Rpi) 项目中相同，但在 SuLingGG/OpenWrt-Rpi 项目的基础上，去掉了一些与无线/内核特性强相关的软件包。
- 由于 Docker 容器与宿主机共享内核，所以 Docker 容器的内核特性与宿主机当前的内核特性相同。
- 本项目固件支持 opkg 安装软件包，软件源内有 7000+ 个软件包可供选择。
- (对于高级用户) 某些软件包可能依赖一些特定的内核特性，所以我不保证 opkg 软件源中的所有软件包都可以正常使用。且因为上文所述原因，在 OpenWrt 中安装 kmod 是无效的，如果有需求，请提前在宿主机中提前载入相应的内核模块，例如:

```
modprobe ip6_udp_tunnel
modprobe ip6table_nat
modprobe pppoe
modprobe tun
modprobe udp_tunnel
modprobe xt_TPROXY
```

镜像详细使用方法请参考博客文章:

「在 Docker 中运行 OpenWrt 旁路网关」

<https://mlapp.cn/376.html>

## 相关教程
通过SSH登录到你的Linux设备

**

把网卡混杂模式打开
**
根据您当前的ip查看网卡！！！
在您的liunx机子上输入查看ip 的命令 ifconfig 或 ip addr 两个命令其中的一个即可！

ip addr

或者

ifconfig

![image](https://github.com/yuzi402256/OpenWrt-Docker/assets/167555481/b3bc38c6-5eb7-48d0-aa08-493dbbb3b625)


打开网卡混合模式
sudo ip link set 文字这里填你自己的网卡名称 promisc on
##以下是我的网卡名称，每台设备可能不一样，要注意！！！！
#打开网卡混杂模式
sudo  ip link set eth0 promisc on

创建 docker 网卡
下边这行里面的一些参数也要替换

按自己的修改后
docker network create -d macvlan --subnet=192.168.0.0/24 --gateway=192.168.0.1 -o parent=eth0 macnet


图片里面有说明大家仔细看看

![image](https://github.com/yuzi402256/OpenWrt-Docker/assets/167555481/450f0150-e340-46ee-8b2a-bc65cc480bb4)

macvlan 模式会为每个容器创建一个独立的 ip 每个容器可以通过独立的 ip 进行访问

修改完成后粘贴到liunx里出现类似于图片里的这种就是成功了
![image](https://github.com/yuzi402256/OpenWrt-Docker/assets/167555481/0d8bca09-9e04-42f3-a08d-18e831025943)


OpenWrt 标准镜像
OpenWrt 标准镜像为集成常用软件包的 Docker 镜像，镜像自带软件包可满足大多数情景下的使用需求

支持设备/平台	openwrt镜像
树莓派 1B	registry.cn-shanghai.aliyuncs.com/suling/openwrt:rpi1
树莓派 2B	registry.cn-shanghai.aliyuncs.com/suling/openwrt:rpi2
树莓派 3B / 3B+	registry.cn-shanghai.aliyuncs.com/suling/openwrt:rpi3
树莓派 4B	registry.cn-shanghai.aliyuncs.com/suling/openwrt:rpi4
armv7	registry.cn-shanghai.aliyuncs.com/suling/openwrt:armv7
arm8/aarch64	registry.cn-shanghai.aliyuncs.com/suling/openwrt:armv8
x86_64/amd64	registry.cn-shanghai.aliyuncs.com/suling/openwrt:x86_64
查看自己的系统架构

uname -a



创建并启动docker 镜像

![1718210516756](https://github.com/yuzi402256/OpenWrt-Docker/assets/167555481/d17eec00-6444-4b01-9386-8d4a7d812447)
arm8/arrch64
可以先拉取镜像 docker pull registry.cn-shanghai.aliyuncs.com/suling/openwrt:armv8

docker run --restart always --name openwrt -d --network macnet --privileged sulinggg/openwrt:armv8 /sbin/init

如果是x86的
![image](https://github.com/yuzi402256/OpenWrt-Docker/assets/167555481/5c7d5295-9619-4d7d-8ba2-9f8a1a97b61e)

x86_64/amd64
docker run --restart always --name openwrt -d --network macnet --privileged sulinggg/openwrt:x86_64 /sbin/init


![image](https://github.com/yuzi402256/OpenWrt-Docker/assets/167555481/7dbbccb6-7a60-4ba6-99ff-999cc7dab90c)


修改openwrt的ip
先进入openwrt容器内
运行执行命令

docker exec -it openwrt bash 

![image](https://github.com/yuzi402256/OpenWrt-Docker/assets/167555481/672915fd-57b2-443d-af4a-38bee35a6d75)

用vi或者vim打开容器的网络配置文件

vim /etc/config/network

或者   nano /etc/config/network


看图片吧，我懒得写了
第一步：
![image](https://github.com/yuzi402256/OpenWrt-Docker/assets/167555481/bbe9e0e6-e7fb-4861-8ff0-e51865c28f0b)

完成前置步骤后就可以进入编辑阶段了，看如下图

![image](https://github.com/yuzi402256/OpenWrt-Docker/assets/167555481/bfb48177-b02e-4b34-b79c-f5b5838c6f70)

编辑修改完记得保存退出，不懂怎么操作看1图！！！！！！

**

如果你报错没法更改IP的话就可以进入下一步了
**
重启openwrt容器网卡！！！

/etc/init.d/network restart
exit

重启网络, 重启完成后便可以通过浏览器访问了
以下是我openwrt的打开地址，你填写你自己的即可
http://192.168.0.10
默认密码是 password

设置 openwrt
防火墙设置
Turbo ACC 网络加速设置

114.114.114.114,114.114.115.115,223.5.5.5,223.6.6.6,180.76.76.76,119.29.29.29,119.28.28.28,1.2.4.8,210.2.4.8,8.8.8.8,8.8.4.4,1.1.1.1
1
粘贴地址看图片
![image](https://github.com/yuzi402256/OpenWrt-Docker/assets/167555481/7f53fcf6-8d55-4209-8ed5-6ca565fc2b94)


设置地址看图片
![image](https://github.com/yuzi402256/OpenWrt-Docker/assets/167555481/d4e26d50-da47-4240-a759-432aca365926)


完成以上步骤，就恭喜您，完成了docker版旁路由的设置
