---
title: Windows编译Tengine Web Server心得
date: 2025-12-01 20:14:18
cover: https://cdn.jsdelivr.net/gh/LuccaWang404/luccawang404.github.io@refs/heads/img/IMG/2025/651e9f7cc458853aef3f17ad.png
tags: 
	- Web
	- Tengine 
	- nginx
	- 运维
---

## P1. Tengine简介

***这是Tengine[官方网站](https://tengine.taobao.org)对该软件的描述:***

> Tengine是由淘宝发起的Web服务器项目。它在Nginx的基础上，针对大访问量网站的需求，添加了很多高级功能和特性。Tengine的性能和稳定性已经在大型的网站如淘宝，天猫，优酷，全球速卖通，Lazada，阿里云等得到了很好的检验。Tengine将向通用API网关方向持续演进和发展，在HTTP应用流量入口网关的基础上，逐步支持4/7层TLS，TCP，UDP和GRPC多协议路由能力，适配不同终端和不同应用，打造全场景通用网关，持续保持Tengine业界领先地位。
>
> 从2011年12月开始，Tengine成为一个开源项目，Tengine团队在积极地开发和维护着它。Tengine团队的核心成员来自于淘宝，蚂蚁，阿里云，搜狗等互联网企业。Tengine是社区合作的成果，我们欢迎大家参与其中，贡献自己的力量。

作为一款十分强大的Web服务器软件，Tengine可以说是nginx的超级加强版。与nginx相比，Tengine更加的稳定，在高并发下有更好的性能表现，因此Tengine更适合大访问量网站的需求。
然而，通过分析源码目录我们便可得知，如此强大的软件，却有一点非常蛋疼——Linux only，即只能在Linux上通过make源代码后再make install。因此，Windows用户基本无缘使用这款神器……***吗？***

## P2. 解决方案

Windows平台上有一神器，唤作**msys2**。

![msys2命令行窗口](https://cdn.jsdelivr.net/gh/LuccaWang404/luccawang404.github.io@refs/heads/img/IMG/2025-12-01/651ec402c458853aef503367.png)

该工具提供了一个类Linux编译环境及海量工具集，让我们可以方便快捷地在Windows平台上将各种源代码编译为exe二进制可执行文件。
**因此，我们可以以此为媒介，将Tengine顺利地移植到Windows平台上。**

## P3. 理论存在，魔法开始

### I. 安装msys2

首先，你需要到各大镜像网站上下载msys2的最新安装包。
你也可以点击[**这里**](https://mirrors.cloud.tencent.com/msys2/distrib/msys2-x86_64-latest.exe)，从腾讯云的镜像站下载最新版的msys2。
下载完毕后，请参照这篇文章完成安装。
[https://blog.csdn.net/ymzhu385/article/details/121449628/](https://blog.csdn.net/ymzhu385/article/details/121449628)
如果你已安装，则可以跳过这一步。

### II. 设置编译环境

编译前，请确保你的msys2已经安装了如下套件：
`openssl-devel` `zlib-devel` `pcre-devel` `libcrypt-devel` `gcc` `msys/make`
如果没有安装，请打开msys2终端（开始→MSYS2 64bit→MSYS2 MSYS），依次执行：

```bash
pacman -Syu
pacman -S openssl-devel zlib-devel pcre-devel libcrypt-devel gcc msys/make
```

**注意：以上均为编译必须组件，缺失则会导致缺失关键函数报错！！！**

> 在执行第一条命令时，msys2可能会要求退出终端完成更新。输入y完成终端更新后，需要重新打开msys2终端以完成后续操作。

### III. 配置项目

以Tengine-2.4.0代码为例。
项目自动配置脚本`configure`有一点相当鸡肋，msys2在执行`configure`的时候，会因配置错误而将编译环境识别错误。因此，我们需要定位到39行，找到`| MSYS_*`：

```bash
38  case "$NGX_SYSTEM" in
39        MINGW32_* | MINGW64_* | MSYS_*) # ←←←这里
40        NGX_PLATFORM=win32
41        ;;
42  esac
```

***把它删掉！***

修改的代码后如下：

```bash
38  case "$NGX_SYSTEM" in
39        MINGW32_* | MINGW64_*) # ←←←删除后
40        NGX_PLATFORM=win32
41        ;;
42  esac
```

Ctrl+S保存文件，退出。

### IV.* 配置Tengine modules

> 如果你只希望使用Tengine的基础功能，请跳过此步骤。

和nginx一样，Tengine也可以通过增加modules来实现功能组件扩展。不过，Tengine的各种modules存放在项目根目录的`modules`文件夹内。
如希望添加额外扩展组件，请在后续的命令中通过以下参数来添加module。

```bash
--add-module=modules/[组件名]
```

举个栗子：

```bash
--add-module=modules/ngx_http_upstream_keepalive_module --without-http_upstream_keepalive_module
# 使用优化过的ngx_http_upstream_keepalive_module需要禁用原有的该组件
```

但是，部分组件会导致编译错误，我们需要将其从`modules`目录中移除。
当然，这部分功能也会不可避免地丢失。
以下是会导致编译错误的modules列表（****包括lua和国密扩展，因为没有对应的库***）：

+ `ngx_backtrace_module`
+ `ngx_debug_pool`
+ `ngx_debug_timer`
+ `ngx_http_lua_module`
+ `ngx_http_tfs_module`
+ `ngx_openssl_ntls`

当然，如果你希望启用全部扩展，请在移除问题组件后使用以下参数：

```bash
--add-module=modules/* --without-http_upstream_keepalive_module
```

### V. 创建Makefile配置文件&构建exe

我们可以通过上文提到的`configure`脚本创建Makefile配置文件。
在msys2终端中cd到项目根目录后，执行：

```bash
./configure --builddir=objs --prefix= --conf-path=conf/nginx.conf --pid-path=logs/nginx.pid --http-log-path=logs/access.log --error-log-path=logs/error.log --with-cc-opt="-D FD_SETSIZE=409600" --add-module=modules/* --without-http_upstream_keepalive_module
#最后的--add-module需自行根据需求添加组件，上方示例为启用全部组件
```

执行完毕后，输入：

```bash
make
```

等待程序完成构建。
构建完成的Tengine程序是`/objs/nginx.exe`。

### VI. 使用

1. 新建一个不含中文的文件夹（整个路径都最好不要有中文），将生成的`nginx.exe`移动至该文件夹内。
2. 回到根目录，将`conf` `html` `docs`文件夹复制到上述含有`nginx.exe`的文件夹内。
3. 在`nginx.exe`应用根目录新建`logs`文件夹。
4. 双击`nginx.exe`运行Tengine，根据报错从`[msys2安装目录]/usr/bin/`复制缺失的dll到Tengine应用根目录。（可能需要重复几次）
5. 运行Tengine。
6. 完成！

**最后的Tengine工作目录应该像这样：**

![完成辣](https://cdn.jsdelivr.net/gh/LuccaWang404/luccawang404.github.io@refs/heads/img/IMG/2025-12-01/651ec402c458853aef50334b.png)
**服务器发出的响应头应该是这样：**

![响应](https://cdn.jsdelivr.net/gh/LuccaWang404/luccawang404.github.io@refs/heads/img/IMG/2025-12-01/651ec402c458853aef5032fb.png)

如果一样，恭喜你，你已经将Tengine成功移植到了Windows平台上！

## 小结

这个烂活断断续续的整了两年半（真的），如今终于成功实装了这个项目，我心中百感交集。
其中，不乏收获成功的喜悦，也有见证了自己与软件共同进步的欣慰。
最后，再次感谢各位软件作者们对开源产品的不懈维护和对开源社区的卓著贡献！

## 后记
本文原于2023年发布于CSDN，后被该网站擅自设为VIP收费文章，且至今没有给我任何收益分成；故我将其从CSDN撤稿删除，转移到我于2025年底新建的个人博客上。但念及CSDN强大的SEO优化，本站必然无法与之抗衡，故我本着互联网分享精神，在CSDN上重新发布了免费的版本；倘若日后CSDN故技重施，再次将其设为收费文章，由于本人精力有限，恕我不再采取任何反制、补救措施。

本文作于我的高一时期。虽然此时我已接触IT行业五年有余，但这是我第一次分享我的技术心得，不足之处还请读者多多担待！

祝各位读者Coding顺利！

> // 2025年12月1日，王无相同学于家中 

***Copyright © 2020-2025 王无相同学，根据CC BY-SA 4.0 协议开放共享***
