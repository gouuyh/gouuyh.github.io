---
title: 关于我使用Joplin记日记的那些事
slug: journaling-with-joplin
tags:
  - IT
  - 开源软件
  - 生活
date: 2024-05-19
update: 2024-05-19
draft: false
---
[Joplin](https://joplinapp.org/) 是一款优秀的开源自由笔记软件，在各种插件的支持下，它也可以用于记录、管理日记。

## 使用 Joplin 前，我使用了哪些软件记日记？

我从去年年底开始写日记，来记录每天的所见所想。这几个月写下来，有2款开源的安卓应用是我使用了比较久的<span class="heimu">虽然最终还是放弃了</span>。
### 其他日记应用

为了获得更好的日记体验，我寻找了很多应用。最先纳入考量的是以 Obsidian 为首的各类笔记管理应用，Joplin 其实也在其中。但它们的安卓应用总有些不符合我需求的地方。先说安卓版 Joplin ，试用时它的预览版还没更新到3.0.1版本，像现在的 iOS 版本一样根本不支持插件，所以当时放弃了它。至于把 Obsidian 及其它基于文件系统的笔记管理软件 pass 了的原因，正是它们把每篇笔记以明文形式单独放在存储设备里进行管理的这一特性。毕竟日记属于比较隐私的数据，我不希望有容易的方法绕开日记软件进行访问。一些停止更新的应用也不考虑使用。
### Easy Diary

[Easy Diary](https://f-droid.org/packages/me.blog.korn123.easydiary/) 是我第一款使用时间比较长的日记应用。这款软件的优点是开箱即用，不需要额外的配置。缺点是太简洁，没有过多自定义的内容。正因如此，我在使用它时没有停止寻找更好的应用，直到找到了 jtx Board。

### jtx Board

使用 [jtx Board](https://f-droid.org/zh_Hans/packages/at.techbee.jtx/) 记日记其实是比较顺手的，2月时我还帮忙修正了一些中文翻译。这个项目的特色是基于 `iCalendar` 协议中的字段管理与同步日志、任务和笔记。它能够利用 `status` 添加标签，支持关联、筛选笔记，以及锁定特定或全部的笔记等很多便利的功能，而且界面设计也很现代、美观。但其缺点有三：一，只能导出明文的 ics 文件；二，同步方式过于冷门；三，界面上的滑动、点击有些卡手。

## 为什么还是使用了 Joplin？

上述两款软件存在一个相同的缺点：缺乏社区的支持。这也是大多数 F-Droid 应用的共性，每个项目只有几个甚至一个维护者，使用者也很少。这会导致项目更新频率不稳定，同时也可能存在安全隐患。我列了个表格来体现三款软件之间的部分差异：

|    ＼     | Easy Diary |       jtx Board       |        Joplin         |
| :------: | :--------: | :-------------------: | :-------------------: |
|   访问限制   |   PIN 码    |         生物识别          | 插件支持（PC）/生物识别（mobile） |
|  导出/备份   |  结构未知的压缩包  | ics文件（图片附件使用base64编码） |  以 Markdown 为基础的各类格式  |
|   远程同步   |     ❌      |   DAVx<sup>5</sup>    |   各类主流云盘及 WebDAV 协议   |
|   内容加密   |     ❌      |           ❌           |      插件支持对单个文件加密      |
| Markdown |     ❌      |          部分的          |          ✔️           |

选择 Joplin 是因为看中了以下四点：

#### 丰富的插件支持

作为 Obsidian 的竞品，没有插件在扩展功能怎么行呢。不过为了能够方便地开发插件，导致了一个问题：这两款软件都依赖于 **Electron**。

![是时候祭出这张图了](1648780188180.jpeg)

#### 使用数据库存储数据

虽然算不上做了什么加密措施，但至少需要比较高的门槛来找到并打开数据库。

#### 同步过程中的端到端加密

Joplin 虽然不会在本地加密，但支持将同步到远程网盘的数据加密。这样，就算他人获取我的网盘数据，也只能看到乱码。

#### Markdown语法的支持

格式文本的功能可以不用，但不能没有，就算是日记，观感也很重要。「富文本」应该是各种格式的总称，而 Markdown 似乎受到程序员偏爱成为最流行的标记语言。

一开始使用 Joplin 时其实是做好了主要在电脑上写日记的准备的。但这不意味着就不安装移动版应用，于是从 F-Droid 上下载到 3.0.1 版本的 Joplin 时，我通过检查 changelog 惊讶地发现这个版本开始加入了对插件的支持（虽然有限的插件能够正常使用是从 3.0.3 开始的）。虽然移动端仅能正常运行下列插件中的「Joplin Calendar」和「Kanban」，但也足够在手机上进行简单的编辑和浏览了。

## 怎么使用 Joplin 记日记？

Joplin 本质是一款笔记与代办事项的管理软件，想要开箱即用方便地记日记是不可能的。但像其他流行的笔记管理软件一样，Joplin 也支持使用各种社区开发的插件来扩展软件的功能。

### 核心插件：Journal

[Journal](https://github.com/leenzhu/joplin-plugin-journal) 插件是使用Joplin写日记的核心。它的功能与Obsidian的日记插件类似，用于创建标题为日期的笔记作为当天的日记。它有更丰富的定制选项，比如自定义标题模板和 `Month Name` / `Weekday Name` 。我是这么自定义的：

Note Name Template:

```
Journal/{{year}}/{{monthName}}/{{year}}-{{month}}-{{day}}-{{weekdayName}}
```

Month Name:

```
01-一月,02-二月,03-三月,04-四月,05-五月,06-六月,07-七月,08-八月,09-九月,10-十月,11-十一月,12-十二月
```

Weekday Name：

```
日,月,火,水,木,金,土
```

以5月19日为例，日记的笔记本路径如下：

```
Journal/2024/05-五月/2024-05-19-日
```

能从标题得到时间信息，还能用文件夹按时间分类，还是很一目了然的。

### 辅助插件一：Joplin Calendar

[Joplin Calendar](https://github.com/rsandz/joplin-calendar) 也能够对标Obsidian的日历插件，但功能不如后者，不能直接点击日期打开或创建对应的日记。在插件设置中取消勾选「Show Modified Notes in Note List」，并开启「Show Related Notes in Note List」，能提升一些观感。

### 辅助插件二：App Locker

Joplin 的桌面版本原生不支持访问限制，但通过插件 [App Locker](https://github.com/ladyrank/joplin-plugin-app-locker) 能够提供简单的软件内锁屏功能（不过不能盖住四周，也不能通过调整高级设置中的 CSS 样式来调整）。这个插件只能提供一块不透明的布罢了，实际上我们依然可以操作任务栏，比如修改选项设置。

### 辅助插件三：Note encryption

既然 App Locker 不能真正保护日记的安全，那就让 [Note encryption](https://github.com/ZhangTe/joplin-plugin-encrypt-notes) 来弥补这个空缺。可以用它来对特定的日记进行加密，每个日记也可以设置不同的密码（如果记得住的话）。

### 辅助插件四：Random Note Reloaded 

在有了核心插件快速创建日记、各种辅助插件增强月度总览、日记安全之后，还缺少一个用于回顾历史日记的插件。市面上不少日记软件都会推送类似于「去年的今天」的日记，Joplin虽然没有这样专用的插件，但[随机笔记](https://github.com/marph91/joplin-random-note-reloaded)插件能够简单实现这个功能。想起来了就点一下按钮打开一篇过去的笔记，也算是回顾历史日记吧。

### 其他辅助插件

这一节将简要列出增强 Joplin 功能的通用插件。

[Note Tabs](https://github.com/benji300/joplin-note-tabs) 能够提供类似浏览器标签页的笔记显示体验。将它的布局调整到编辑器上方或下方会有更好的效果。

[Note Link System](https://github.com/ylc395/joplin-plugin-note-link-system) 主要是提供反链功能，可以用来把两篇日记关联起来。

### 外部编辑器

Joplin 有一个比较好的功能，就是允许我们用自己最喜欢的编辑器来写东西。虽然但是，我并没有找到符合我要求的编辑器……因为「Markdown 所见即所得」与「轻量小巧」是不可兼得的，同时时下流行的几款代码编辑器对 Markdown 语法的自动格式补全支持不够，我最终选择了「MarkText」这款基于 **Electron** 的 Markdown 编辑器。<span class="heimu">真的不想再在电脑上装更多的 Electron 了啊啊啊啊啊啊 ╧═╧╰（`□′╰）</span>

### 另一套方案：Plugin Bundle

[Plugin Bundle](https://github.com/SeptemberHX/joplin-plugin-bundle) 是几个插件（[Outline](https://github.com/cqroot/joplin-outline) / [Inline Todo](https://github.com/CalebJohn/joplin-inline-todo) / [Daily Note](https://github.com/liamcain/obsidian-calendar-plugin) / [History Panel](https://github.com/alondmnt/joplin-plugin-history-panel)）的捆绑插件，但对于记日记而言，「Daily Note」才是核心插件，它的灵感来源于 [Obsidian的日历插件](https://github.com/liamcain/obsidian-calendar-plugin)。这个插件能够同时替代「Journal」和「Joplin Calendar」，尽管可定制性更低，也不支持暗色模式，但至少能像在 Obsidian 中一样写日记了。我没有采用这个方案<span class="heimu">，因为把已有的100多篇已经格式化了标题的笔记重命名一遍挺麻烦</span>。

***

先记录到这里，可能有遗漏的地方，等想起来或者回顾时候发现了再补上吧。