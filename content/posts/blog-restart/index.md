---
title: 博客的重新活跃
slug: blog-restart
tags:
  - 博客
date: 2024-03-03
update: 2024-03-03
draft: false
---
记得上次更新博客，还是在上次（雾

准确地说是 2021 年的夏天，那时高考刚刚结束，出于未来课程学习、有充足的时间研究之前只是偶尔学一点的技术的需求，我拥有了一台自己的电脑。我把预装的 Windows 格式化，装上了高二以来一直想用的 Arch Linux。我也顺手记录了我的安装流程作为我的博客第一篇文章。

还记得高二那年，我终于在虚拟机上跟随 Arch Wiki 以及 B站上的好几个视频，成功安装了几次 Arch。暑假时，还拿家里 09 年的惠普迷你上网本（ Atom CPU ）安装了 Arch Linux x86。当时受到 [TheCW](https://space.bilibili.com/13081489) 的影响，我尝试了不使用流行的显示管理器和桌面环境，而使用 `startx` 来启动 `dwm` 。（根据他 23 年发布的[视频](https://www.bilibili.com/video/BV1zc411T7j7/) ，他的主力不再是 Arch Linux，而是 MacOS 了😂）

这两年半来这台主力机环境的变化也很有意思。刚安装上的几个月，我用的就是 `dwm`，但出于美观我安装了 KDE 的显示管理器，还对其和 `GRUB` 的界面进行了美化。后来由于对 C 语言的不熟悉使得对 `dwm` 的定制陷入瓶颈，就换上了更容易美化的 `i3-wm` 。没用几个月，甚至第一学期还没过完，我就换成了 KDE Plasma，并且美化成了 MacOS 风格。

22 年的寒假，为了能和几个高中同学一起联机玩游戏，我成为了原神玩家，并在大年初一和他们第一次联机。一开始是在 iPad 上游玩的，但常常能在网上看见有人说 PC 的画面更好，键鼠操作的体验也更棒，便萌生了在 Linux 环境上运行原神的想法。一开始的在 Windows 虚拟机中运行的幻想被米哈游检测虚拟环境的弹窗击碎，在网上找了一些方法，并排除了打补丁（怕封号）的方案后，将目光落在了 KVM 去虚拟化上，还找到了一篇相当翔实的 [教程](https://lantian.pub/article/modify-computer/laptop-intel-nvidia-optimus-passthrough.lantian/)。于是摩拳擦掌开始检查我的硬件是否支持，结果悲惨地发现由于 CPU 是 11 代，就不能支持这种去虚拟化的方案……遂决定安装双系统。没错，我换回 Windows 的契机之一就是游戏。还有一个契机是当时也产生了制作 MMD 的兴趣，而在 Wine 环境中 MMD 怎么也运行不起来。不仅如此，Linux 环境下的办公替代品也不是很好使，WPS 不想继续用了，Libre Office 又不太适合办公类的文档编辑，有一段时间都是在 Windows 里写作业和上交作业的。后来也证明确实要换回来，因为专业课程要用 SPSS，选了门比较雷的通识课要用 SolidWorks 机械设计，这些在 Linux 平台没有合适的替代。这个双系统方案一直用到了现在。

虽然纯 Linux 环境的使用时间不满一年，但还是学到了很多稍偏底层的系统配置。 这期间我最大的收获就是对 `systemd` 的了解，特别是使用 `systemd`配置ACPI，这在最近调整家里长期运行的 Debian 服务器配置时帮了大忙。因为知道在桌面环境加载前系统的电源管理设置没有被覆盖，所以很快找到了解决笔记本合上盖子的状态下自动登录超时会进入睡眠的问题。

---

回想博客停止活跃的两年半，我发现确实没有什么适合专门写文章的事情。我在技术方面的经历，基本上可以用上文的文字来概括。期间也进行了 `NixOS` 的安装尝试，但由于它的逻辑与现有的大部分系统都不一样，而且它的文档与 Arch 相比属于小巫见大巫，不得已中途放弃。不过我还是保留了 Github 上的配置文件仓库，希望哪天能捡起来。

那为什么又想写博文了呢？自然是想到能写的东西了。博客以长文记录作者的经历与感悟，作为一名业余的技术爱好者，只写技术相关的文字实在有些为难，所以我决定写一些其他的内容。长途旅行的游记是不错的话题，非系统的、配置起来也比较复杂的软件的使用经验也可以分享。而且，最近想到了几个尝试自己写代码的点子，有机会的话或许真的会试着去写，届时可以把心路历程记录下来。
