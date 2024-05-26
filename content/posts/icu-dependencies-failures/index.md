---
title: 记一次 icu 包依赖错误的解决
slug: icu-dependencies-failures
tags:
  - IT
  - OS
date: 2024-05-26
update: 2024-05-26
draft: false
---
今天例行对双系统 Arch Linux 进行更新。执行 `pacman -Syu` 命令后意外报错：

```
error: failed to prepare transaction (could not satisfy dependencies)
:: installing icu (75.1-1) breaks dependency 'libicui18n.so=74-64' required by electron22
:: installing icu (75.1-1) breaks dependency 'libicuuc.so=74-64' required by electron22
:: installing icu (75.1-1) breaks dependency 'libicui18n.so=74-64' required by qt5-webengine
:: installing icu (75.1-1) breaks dependency 'libicuuc.so=74-64' required by qt5-webengine
```

复制报错后在搜索引擎上搜寻，很快就找到了三天前发布在英文官方论坛上的[帖子](https://bbs.archlinux.org/viewtopic.php?pid=2173001)。看下来其实并不是什么大事，卸载掉就可以了。大概由于这两个包太旧了，而 `icu (75.1-1)` 不再对这两个包提供兼容性支持，所以删掉是最简单的解决方法。我这里的情况，`qt5-webengine` 是不被依赖的孤立包，而`electron22` 被 `motrix` 依赖。那就连带依赖删除 `qt5-webengine` 和 `motrix` ，再更新系统，更新后再装回来<span class="heimu">如果装得回来</span>。

事实上更新系统后尝试通过 AUR 或 archlinuxcn 安装 `motrix` 会报错。但我觉得 motrix 作为 aria2 的前端还算不错，就上官网下载了个 Appimage 版本的放在家目录下以备不时之需。可能以后会尝试直接使用 aria2 吧，这样还可以使用 systemd 的 unit 实现开机运行。