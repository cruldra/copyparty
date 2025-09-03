<img src="https://github.com/9001/copyparty/raw/hovudstraum/docs/logo.svg" width="250" align="right"/>

### 💾🎉 copyparty

使用[*任何*](#browser-support)网络浏览器将几乎任何设备变成支持可恢复上传/下载的文件服务器

* 服务器只需要Python（2或3），所有依赖项都是可选的
* 🔌 协议：[http](#the-browser) // [webdav](#webdav-server) // [ftp](#ftp-server) // [tftp](#tftp-server) // [smb/cifs](#smb-server)
* 📱 [安卓应用](#android-app) // [iPhone快捷指令](#ios-shortcuts)

👉 **[开始使用](#quickstart)！** 或访问 **[只读演示服务器](https://a.ocv.me/pub/demo/)** 👀 运行在我地下室的nuc上

📷 **截图：** [浏览器](#the-browser) // [上传](#uploading) // [撤销](#unpost) // [缩略图](#thumbnails) // [搜索](#searching) // [文件搜索](#file-search) // [zip下载](#zip-downloads) // [markdown查看器](#markdown-viewer)

🎬 **视频：** [上传](https://a.ocv.me/pub/demo/pics-vids/up2k.webm) // [命令行上传](https://a.ocv.me/pub/demo/pics-vids/u2cli.webm) // [竞速传输](https://a.ocv.me/pub/g/nerd-stuff/cpp/2024-0418-race-the-beam.webm) // 👉 **[功能展示](https://a.ocv.me/pub/demo/showcase-hq.webm)** ([youtube](https://www.youtube.com/watch?v=15_-hgsX2V0))

挪威制造 🇳🇴


## 目录

* 顶部
    * [快速开始](#quickstart) - 只需运行 **[copyparty-sfx.py](https://github.com/9001/copyparty/releases/latest/download/copyparty-sfx.py)** -- 就是这样！🎉
        * [在家使用](#at-home) - 让它可以通过互联网访问
        * [在服务器上](#on-servers) - 你可能还需要这些，特别是在服务器上
    * [功能特性](#features) - 另请参阅[与类似软件的比较](./docs/versus.md)
    * [用户评价](#testimonials) - 用户反馈的小集合
* [动机](#motivations) - 项目目标/理念
    * [注意事项](#notes) - 一般注意事项
* [错误](#bugs) - 大致按遇到的可能性排序
    * [不是我的错误](#not-my-bugs) - 这里也是同样的顺序
* [重大变更](#breaking-changes) - 升级说明
* [常见问题](#FAQ) - "经常"被问到的问题
* [账户和卷](#accounts-and-volumes) - 每个文件夹、每个用户的权限
    * [遮蔽](#shadowing) - 隐藏特定的子文件夹
    * [点文件](#dotfiles) - unix风格的隐藏文件/文件夹
* [浏览器](#the-browser) - 使用网络浏览器访问copyparty服务器
    * [标签页](#tabs) - UI中的主要标签页
    * [热键](#hotkeys) - 浏览器有以下热键
    * [导航面板](#navpane) - 在面包屑导航或导航面板之间切换
    * [缩略图](#thumbnails) - 按`g`或`田`切换网格视图而不是文件列表
    * [zip下载](#zip-downloads) - 将文件夹（或文件选择）下载为`zip`或`tar`文件
    * [上传](#uploading) - 将文件/文件夹拖入网络浏览器进行上传
        * [文件搜索](#file-search) - 将文件拖入浏览器还可以让你查看它们是否存在于服务器上
        * [撤销](#unpost) - 撤销/删除意外上传
        * [自毁](#self-destruct) - 上传可以设置生存期
        * [竞速传输](#race-the-beam) - 在文件仍在上传时下载文件（[演示视频](http://a.ocv.me/pub/g/nerd-stuff/cpp/2024-0418-race-the-beam.webm)）
        * [传入文件](#incoming-files) - 控制面板显示所有传入文件的预计到达时间
    * [文件管理器](#file-manager) - 剪切/粘贴、重命名和删除文件/文件夹（如果你有权限）
    * [分享](#shares) - 通过创建临时链接分享文件或文件夹
    * [批量重命名](#batch-rename) - 选择一些文件并按`F2`打开重命名UI
    * [RSS订阅](#rss-feeds) - 使用RSS阅读器监控文件夹
    * [最近上传](#recent-uploads) - 列出所有最近的上传
    * [媒体播放器](#media-player) - 播放几乎所有音频格式
        * [播放列表](#playlists) - 创建和播放[m3u8](https://en.wikipedia.org/wiki/M3U)播放列表
        * [创建播放列表](#creating-a-playlist) - 使用独立媒体播放器或copyparty
        * [音频均衡器](#audio-equalizer) - 和[动态范围压缩器](https://en.wikipedia.org/wiki/Dynamic_range_compression)
        * [修复安卓上不可靠的播放](#fix-unreliable-playback-on-android) - 由于手机/应用设置
    * [文本文件查看器](#textfile-viewer) - 实时流式传输日志文件等（[演示](https://a.ocv.me/pub/demo/logtail/)）
    * [markdown查看器](#markdown-viewer) - 有*两个*编辑器
        * [markdown变量](#markdown-vars) - 带有服务器端变量扩展的动态文档
    * [其他技巧](#other-tricks)
    * [搜索](#searching) - 按大小、日期、路径/名称、mp3标签等搜索...
* [服务器配置](#server-config) - 使用参数或配置文件，或两者混合
    * [零配置](#zeroconf) - 在局域网上宣布启用的服务（[图片](https://user-images.githubusercontent.com/241032/215344737-0eae8d98-9496-4256-9aa8-cd2f6971810d.png)）
        * [mdns](#mdns) - 局域网域名和功能宣布器
        * [ssdp](#ssdp) - windows资源管理器宣布器
    * [二维码](#qr-code) - 打印二维码[(截图)](https://user-images.githubusercontent.com/241032/194728533-6f00849b-c6ac-43c6-9359-83e454d11e00.png)以便快速访问
    * [ftp服务器](#ftp-server) - 可以使用`--ftp 3921`启动FTP服务器
    * [webdav服务器](#webdav-server) - 支持读写
        * [从Windows连接到webdav](#connecting-to-webdav-from-windows) - 使用GUI
    * [tftp服务器](#tftp-server) - 可以使用`--tftp 3969`启动TFTP服务器（读/写）
    * [smb服务器](#smb-server) - 不安全、慢、不推荐用于广域网
    * [浏览器用户体验](#browser-ux) - 调整UI
    * [opengraph](#opengraph) - discord和社交媒体嵌入
    * [文件去重](#file-deduplication) - 启用基于符号链接的上传去重
    * [文件索引](#file-indexing) - 启用音乐搜索、上传撤销和更好的去重
        * [排除模式](#exclude-patterns) - 节省一些时间
        * [文件系统守卫](#filesystem-guards) - 避免遍历到其他文件系统
        * [定期重新扫描](#periodic-rescan) - 文件系统监控
    * [上传规则](#upload-rules) - 使用卷标志设置上传规则
    * [压缩上传](#compress-uploads) - 文件可以在上传时自动压缩
    * [chmod和chown](#chmod-and-chown) - 每个卷的文件系统权限和所有权
    * [其他标志](#other-flags)
    * [数据库位置](#database-location) - 在卷内（`.hist/up2k.db`，默认）或其他地方
    * [音频文件元数据](#metadata-from-audio-files) - 设置`-e2t`在上传时索引标签
    * [文件解析器插件](#file-parser-plugins) - 提供自定义解析器来索引额外的标签
    * [事件钩子](#event-hooks) - 在上传、重命名等时触发程序（[示例](./bin/hooks/)）
        * [zeromq](#zeromq) - 事件钩子可以发送zeromq消息
        * [上传事件](#upload-events) - 更旧、更强大的方法（[示例](./bin/mtag/)）
    * [处理器](#handlers) - 用插件重新定义行为（[示例](./bin/handlers/)）
    * [IP认证](#ip-auth) - 基于IP范围（CIDR）的自动登录
        * [限制到IP](#restrict-to-ip) - 将用户限制到某些IP范围（CIDR）
    * [身份提供者](#identity-providers) - 用oauth等替换copyparty密码
        * [通用头部认证](#generic-header-auth) - 其他通过头部认证的方式
    * [用户可更改密码](#user-changeable-passwords) - 如果允许，用户可以更改自己的密码
    * [使用云作为存储](#using-the-cloud-as-storage) - 连接到aws s3存储桶等
    * [对Google隐藏](#hiding-from-google) - 告诉搜索引擎你不想被索引
    * [主题](#themes)
    * [完整示例](#complete-examples)
    * [监听端口80和443](#listen-on-port-80-and-443) - 成为*真正的*网络服务器
    * [反向代理](#reverse-proxy) - 在其他网站旁边运行copyparty
        * [真实IP](#real-ip) - 教copyparty如何查看客户端IP
        * [反向代理性能](#reverse-proxy-performance)
    * [永久cloudflare隧道](#permanent-cloudflare-tunnel) - 如果你有域名并想快速让copyparty上线
    * [prometheus](#prometheus) - 可以启用指标/统计
    * [其他极其特定的功能](#other-extremely-specific-features) - 你永远不会找到这些的用途
        * [自定义MIME类型](#custom-mimetypes) - 更改文件扩展名的关联
        * [GDPR合规](#GDPR-compliance) - 想象专业使用copyparty...
        * [功能开关](#feature-chickenbits) - 有问题的功能？撕掉它
        * [功能增强](#feature-beefybits) - 在你的操作系统/环境上强制启用有已知问题的功能
* [软件包](#packages) - 聚会可能比你想象的更近
    * [arch软件包](#arch-package) - `pacman -S copyparty`（在[arch linux extra](https://archlinux.org/packages/extra/any/copyparty/)中）
    * [fedora软件包](#fedora-package) - 尚不存在
    * [homebrew公式](#homebrew-formulae) - `brew install copyparty ffmpeg`
    * [nix软件包](#nix-package) - `nix profile install github:9001/copyparty`
    * [nixos模块](#nixos-module)
* [浏览器支持](#browser-support) - 简而言之：是的
* [客户端示例](#client-examples) - 使用非浏览器客户端与copyparty交互
    * [文件夹同步](#folder-sync) - 与copyparty同步文件夹
    * [挂载为驱动器](#mount-as-drive) - 将远程copyparty服务器作为本地文件系统
* [安卓应用](#android-app) - 一键上传到copyparty
* [iOS快捷指令](#iOS-shortcuts) - 没有iPhone应用，但是
* [性能](#performance) - 默认设置通常很好 - 期望`8 GiB/s`下载，`1 GiB/s`上传
    * [客户端](#client-side) - 上传文件时
* [安全性](#security) - 有一个[discord服务器](https://discord.gg/25J8CdTT6G)
    * [陷阱](#gotchas) - 可能意外的行为
    * [cors](#cors) - 跨站请求配置
    * [文件密钥](#filekeys) - 防止文件名暴力破解
        * [目录密钥](#dirkeys) - 在卷中分享特定文件夹
    * [密码哈希](#password-hashing) - 你可以哈希密码
    * [https](#https) - HTTP和HTTPS都被接受
* [从崩溃中恢复](#recovering-from-crashes)
    * [客户端崩溃](#client-crashes)
        * [firefox白屏](#firefox-wsod) - firefox 87在上传期间可能崩溃
* [HTTP API](#HTTP-API) - 参见[开发说明](./docs/devnotes.md#http-api)
* [依赖项](#dependencies) - 强制依赖项
    * [可选依赖项](#optional-dependencies) - 安装这些以启用额外功能
        * [依赖项开关](#dependency-chickenbits) - 防止加载可选依赖项
    * [可选GPL内容](#optional-gpl-stuff)
* [sfx](#sfx) - 自包含"二进制文件"（推荐！）
    * [copyparty.exe](#copypartyexe) - 下载[copyparty.exe](https://github.com/9001/copyparty/releases/latest/download/copyparty.exe)（win8+）或[copyparty32.exe](https://github.com/9001/copyparty/releases/latest/download/copyparty32.exe)（win7+）
    * [zipapp](#zipapp) - 另一个紧急替代方案，[copyparty.pyz](https://github.com/9001/copyparty/releases/latest/download/copyparty.pyz)
* [在安卓上安装](#install-on-android)
* [在iOS上安装](#install-on-iOS)
* [报告错误](#reporting-bugs) - 包含上下文的想法，以及提交位置
* [开发说明](#devnotes) - 构建说明等，参见[./docs/devnotes.md](./docs/devnotes.md)


## 快速开始

只需运行 **[copyparty-sfx.py](https://github.com/9001/copyparty/releases/latest/download/copyparty-sfx.py)** -- 就是这样！🎉

> ℹ️ sfx是一个[自解压器](https://github.com/9001/copyparty/issues/270)，它将嵌入的`tar.gz`解压到`$TEMP` -- 如果这看起来太可怕，你可以使用性能稍差的[zipapp](#zipapp)

* 或通过[pypi](https://pypi.org/project/copyparty/)安装：`python3 -m pip install --user -U copyparty`
* 或如果你无法安装python，可以使用[copyparty.exe](#copypartyexe)代替
* 或在[arch](#arch-package) ╱ [NixOS](#nixos-module) ╱ [通过nix](#nix-package)上安装
* 或如果你在安卓上，[在termux中安装copyparty](#install-on-android)
* 或者iPhone或iPad？[在iOS的a-Shell中安装](#install-on-iOS)
* 或者你有[synology nas / dsm](./docs/synology-dsm.md)
* 或如果你安装了[uv](https://docs.astral.sh/uv/)，运行`uv tool run copyparty`
* 或如果你的电脑有问题且其他都不工作，[试试pyz](#zipapp)
* 或如果你的操作系统死了，试试[可启动闪存驱动器/cd-rom](https://a.ocv.me/pub/stuff/edcd001/enterprise-edition/)
* 或如果你还不信任copyparty并想稍微隔离它，那么...
  * ...也许[prisonparty](./bin/prisonparty.sh)来创建一个小的[chroot](https://wiki.archlinux.org/title/Chroot)（非常便携），
  * ...或[bubbleparty](./bin/bubbleparty.sh)用[bubblewrap](https://github.com/containers/bubblewrap)包装它（更好）
* 或如果你更喜欢[使用docker](./scripts/docker/) 🐋 你也可以这样做
  * docker内置了所有依赖项，所以跳过这一步：

通过安装一些推荐的依赖项来启用缩略图（图像/音频/视频）、媒体索引和音频转码：

* **Alpine：** `apk add py3-pillow ffmpeg`
* **Debian：** `apt install --no-install-recommends python3-pil ffmpeg`
* **Fedora：** rpmfusion + `dnf install python3-pillow ffmpeg --allowerasing`
* **FreeBSD：** `pkg install py39-sqlite3 py39-pillow ffmpeg`
* **MacOS：** `port install py-Pillow ffmpeg`
* **MacOS**（替代）：`brew install pillow ffmpeg`
* **Windows：** `python -m pip install --user -U Pillow`
  * 手动安装[python](https://www.python.org/downloads/windows/)和[ffmpeg](#optional-dependencies)；不要使用`winget`或`Microsoft Store`（它会破坏$PATH）
  * copyparty.exe自带`Pillow`，只需要[ffmpeg](#optional-dependencies)用于媒体标签/视频缩略图
* 参见[可选依赖项](#optional-dependencies)以启用更多功能

不带参数运行copyparty（例如在Windows上双击它）将给每个人对当前文件夹的读/写访问权限；你可能需要[账户和卷](#accounts-and-volumes)

或查看[一些使用示例](#complete-examples)获取灵感，或[完整的Windows示例](./docs/examples/windows.md)

一些推荐的选项：
* `-e2dsa`启用一般[文件索引](#file-indexing)
* `-e2ts`启用音频元数据索引（需要FFprobe或Mutagen）
* `-v /mnt/music:/music:r:rw,foo -a foo:bar`将`/mnt/music`共享为`/music`，任何人都可以`r`ead，用户`foo`可以读写，密码`bar`
  * 将`:r:rw,foo`替换为`:r,foo`以使文件夹只对`foo`可读，其他人都不行
  * 参见[账户和卷](#accounts-and-volumes)（或`--help-accounts`）了解语法和其他权限


### 在家使用

通过启动[cloudflare快速隧道](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/do-more-with-tunnels/trycloudflare/)使其可以通过互联网访问：

首先下载[cloudflared](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/downloads/)，然后用`cloudflared tunnel --url http://127.0.0.1:3923`启动隧道

隧道启动时，它会显示一个URL，你可以分享这个URL让任何人浏览你的存储或上传文件给你

但如果你有域名，那么你可能想跳过随机自动生成的URL，而是制作一个[永久cloudflare隧道](#permanent-cloudflare-tunnel)

由于人们将通过cloudflare连接，运行copyparty时使用`--xff-hdr cf-connecting-ip`来正确检测客户端IP


### 在服务器上

你可能还需要这些，特别是在服务器上：

* [contrib/systemd/copyparty.service](contrib/systemd/copyparty.service)将copyparty作为systemd服务运行（参见内部指南）
* [contrib/systemd/prisonparty.service](contrib/systemd/prisonparty.service)在chroot中运行它（额外安全）
* [contrib/openrc/copyparty](contrib/openrc/copyparty)在Alpine / Gentoo上运行copyparty
* [contrib/rc/copyparty](contrib/rc/copyparty)在FreeBSD上运行copyparty
* [nixos模块](#nixos-module)在NixOS主机上运行copyparty
* [contrib/nginx/copyparty.conf](contrib/nginx/copyparty.conf)在nginx后面[反向代理](#reverse-proxy)（更好的https）

记住打开你想要的端口；这里是一个包含copyparty提供的所有功能的完整示例：
```
firewall-cmd --permanent --add-port={80,443,3921,3923,3945,3990}/tcp  # --zone=libvirt
firewall-cmd --permanent --add-port=12000-12099/tcp  # --zone=libvirt
firewall-cmd --permanent --add-port={69,1900,3969,5353}/udp  # --zone=libvirt
firewall-cmd --reload
```
（69:tftp，1900:ssdp，3921:ftp，3923:http/https，3945:smb，3969:tftp，3990:ftps，5353:mdns，12000:被动ftp）


## 功能特性

另请参阅[与类似软件的比较](./docs/versus.md)

* 后端功能
  * ☑ IPv6 + unix套接字
  * ☑ [多进程](#performance)（真正的多线程）
  * ☑ 卷（挂载点）
  * ☑ [账户](#accounts-and-volumes)
  * ☑ [ftp服务器](#ftp-server)
  * ☑ [tftp服务器](#tftp-server)
  * ☑ [webdav服务器](#webdav-server)
  * ☑ [smb/cifs服务器](#smb-server)
  * ☑ [二维码](#qr-code)快速访问
  * ☑ [upnp / zeroconf / mdns / ssdp](#zeroconf)
  * ☑ [事件钩子](#event-hooks) / 脚本运行器
  * ☑ [反向代理支持](https://github.com/9001/copyparty#reverse-proxy)
  * ☑ 跨平台（Windows、Linux、Macos、Android、iOS、FreeBSD、arm32/arm64、ppc64le、s390x、risc-v/riscv64）
* 上传
  * ☑ 基础：纯multipart，支持ie6
  * ☑ [up2k](#uploading)：js、可恢复、多线程
    * **无文件大小限制！** 即使在Cloudflare上
  * ☑ stash：简单的PUT文件投递器
  * ☑ 文件名随机化器
  * ☑ 只写文件夹
  * ☑ [撤销](#unpost)：撤销/删除意外上传
  * ☑ [自毁](#self-destruct)（服务器端或客户端指定）
  * ☑ [竞速传输](#race-the-beam)（几乎像点对点）
  * ☑ 符号链接/丢弃重复项（内容匹配）
* 下载
  * ☑ 浏览器中的单个文件
  * ☑ [文件夹作为zip/tar文件](#zip-downloads)
  * ☑ [FUSE客户端](https://github.com/9001/copyparty/tree/hovudstraum/bin#partyfusepy)（只读）
* 浏览器
  * ☑ [导航面板](#navpane)（目录树侧边栏）
  * ☑ 文件管理器（剪切/粘贴、删除、[批量重命名](#batch-rename)）
  * ☑ 音频播放器（带[操作系统媒体控制](https://user-images.githubusercontent.com/241032/215347492-b4250797-6c90-4e09-9a4c-721edf2fb15c.png)和opus/mp3转码）
    * ☑ 将视频文件作为音频播放（在服务器上转换）
    * ☑ 创建和播放[m3u8播放列表](#playlists)
  * ☑ 带webm播放器的图像画廊
  * ☑ 带语法高亮的[文本文件浏览器](#textfile-viewer)
    * ☑ 增长文件的实时流式传输（日志文件等）
  * ☑ [缩略图](#thumbnails)
    * ☑ ...使用Pillow、pyvips或FFmpeg的图像
    * ☑ ...使用rawpy的RAW图像
    * ☑ ...使用FFmpeg的视频
    * ☑ ...使用FFmpeg的音频（频谱图）
    * ☑ 缓存驱逐（最大年龄；可能最终会有最大大小）
  * ☑ 多语言UI（英语、挪威语、中文，[添加你自己的](./docs/rice/#translations)）
  * ☑ SPA（上传时浏览）
* 服务器索引
  * ☑ [按内容定位文件](#file-search)
  * ☑ 按名称/路径/日期/大小搜索
  * ☑ [按ID3标签等搜索](#searching)
* 客户端支持
  * ☑ [文件夹同步](#folder-sync)（仅单向；永远不会支持完全同步）
  * ☑ [curl友好](https://user-images.githubusercontent.com/241032/215322619-ea5fd606-3654-40ad-94ee-2bc058647bb2.png)
  * ☑ [opengraph](#opengraph)（discord嵌入）
* markdown
  * ☑ [查看器](#markdown-viewer)
  * ☑ 编辑器（当然为什么不呢）
  * ☑ [变量](#markdown-vars)

PS：缺少什么？将你的任何疯狂想法作为[功能请求](https://github.com/9001/copyparty/issues/new?assignees=9001&labels=enhancement&template=feature_request.md)或[讨论](https://github.com/9001/copyparty/discussions/new?category=ideas)发布 🤙


## 用户评价

用户反馈的小集合

`足够好`，`出人意料地正确`，`认证的好软件`，`就是能用`，`为什么`，`哇，这比nextcloud更好`

* UI просто ужасно. Если буду описывать детально не смогу удержаться в рамках приличий


# 动机

项目目标/理念

* 反向linux哲学 -- 做所有的事情，并做得*还可以*
  * 快速插入式服务，在紧急情况下获得大量功能
  * 一些[替代方案](./docs/versus.md)可能更适合你
* 随处运行，支持一切
  * 尽可能多的网络浏览器和python版本
    * 每个浏览器至少应该能够浏览、下载、上传文件
    * 成为在古老机器之间传输东西的良好紧急解决方案
  * 最小依赖
    * 但添加额外功能的可选依赖是可以的
    * 一切都是纯文本使得可以校对恶意代码
  * 无需准备/设置，只需运行sfx（这也是纯文本）
* 适应性强、可塑、可破解
  * 无构建步骤；修改js/python而不需要node.js或类似的东西

致富特别*不是*动机，但如果你想捐赠，请查看我的[github个人资料](https://github.com/9001)关于我的FOSS项目的一般捐赠（也谢谢！）


## 注意事项

一般注意事项：
* 纸质打印受深色/浅色模式影响！使用浅色模式打印彩色，深色模式打印灰度
  * 因为目前没有浏览器正确实现媒体查询来做到这一点orz

浏览器特定：
* iPhone/iPad：使用Firefox下载文件
* Android-Chrome：增加"并行上传"以获得更高速度（android错误）
* Android-Firefox：选择文件需要一段时间（他们对☝️的修复）
* Desktop-Firefox：~~如果你的文件很大可能会使用GB的RAM~~ *现在似乎没问题了*
* Desktop-Firefox：[可能阻止你拔出USB闪存驱动器](https://bugzilla.mozilla.org/show_bug.cgi?id=1792598)直到你访问`about:memory`并点击`最小化内存使用`

服务器操作系统特定：
* RHEL8 / Rocky8：你可以使用`/usr/libexec/platform-python`运行copyparty

服务器注意事项：
* 支持pypy，但如果启用数据库，常规cpython更快


# 错误

大致按遇到的可能性排序

* 一般：
  * `--th-ff-jpg`可能修复某些FFmpeg版本上的视频缩略图（macos，一些linux）
  * `--th-ff-swr`可能修复某些FFmpeg版本上的音频缩略图
  * 如果`up2k.db`（文件系统索引）在samba共享或网络磁盘上，如果共享断开一段时间，你会得到不可预测的行为
    * 使用`--hist`或`hist`卷标志（`-v [...]:c,hist=/tmp/foo`）将数据库和缩略图放在本地磁盘上
    * 或者，如果你只想移动数据库（而不是缩略图），则使用`--dbpath`或`dbpath`卷标志
  * 所有卷必须在启动时存在/可用；否则up2k（特别是mtp）会变得奇怪
  * 可能还有更多，请告诉我

* python 3.4及更旧版本（包括2.7）：
  * 许多罕见和令人兴奋的边缘情况，因为[python还没有处理EINTR](https://peps.python.org/pep-0475/)
    * 从copyparty下载可能突然失败，但上传*应该*没问题

* Windows上的python 2.7：
  * 无法使用`-e2d`索引非ascii文件名
  * 无法处理带有mojibake的文件名

如果你有新的令人兴奋的错误要分享，请参阅[报告错误](#reporting-bugs)


## 不是我的错误

这里也是同样的顺序

* [Chrome问题1317069](https://bugs.chromium.org/p/chromium/issues/detail?id=1317069) -- 如果你尝试通过拖拽包含符号链接的文件夹到浏览器中上传，符号链接的文件不会被上传

* [Chrome问题1352210](https://bugs.chromium.org/p/chromium/issues/detail?id=1352210) -- 纯文本http在文件哈希方面可能比https更快（但也极其CPU密集）

* [Chrome问题383568268](https://issues.chromium.org/issues/383568268) -- webworkers中的文件读取器可能OOM/崩溃浏览器标签
  * copyparty有一个似乎工作得足够好的解决方案

* [Firefox问题1790500](https://bugzilla.mozilla.org/show_bug.cgi?id=1790500) -- 上传约4000个小文件后整个浏览器可能崩溃

* Android：由于[电池使用设置](#fix-unreliable-playback-on-android)，音乐播放随机停止

* iPhones：音量控制不工作，因为[苹果不想要它](https://developer.apple.com/library/archive/documentation/AudioVideo/Conceptual/Using_HTML5_Audio_Video/Device-SpecificConsiderations/Device-SpecificConsiderations.html#//apple_ref/doc/uid/TP40009523-CH5-SW11)
  * `AudioContext`可能永远不会是一个可行的解决方案，因为苹果引入新问题的速度比修复当前问题的速度更快

* iPhones：歌曲切换期间音乐音量像过山车一样
  * 我对此无能为力，因为`AudioContext`在safari中仍然有问题

* iPhones：预加载功能（在媒体播放器选项标签中）可能在每首歌结束前20秒造成微小的音频故障，但禁用它可能会导致更糟糕的iOS错误出现
  * 只是一种预感，但禁用预加载可能导致播放完全停止，或可能搞乱蓝牙扬声器
  * 试图添加关于此的工具提示，但看起来苹果破坏了我的工具提示

* iPhones：预加载的awo文件使safari在播放开始时记录MEDIA_ERR_NETWORK错误，但歌曲播放得很好，所以无所谓
  * awo，opus-weba，是苹果对opus支持的新尝试，取代了技术上限制为cbr opus的opus-caf

* iPhones：预加载另一个awo文件可能导致播放停止
  * 可以通过在`mp.onpreload`中使用`mp.au.play()`在某种程度上缓解，但这可能在safari中遇到竞争条件，导致同时并行播放同一个音频对象两次...

* Windows：如果名称以`.`结尾，无法访问文件夹
  * python或windows错误

* Windows：msys2-python 3.8.6在up2k中离开作用域互斥锁时偶尔抛出`RuntimeError: release unlocked lock`
  * 这是msys2错误，常规windows版本的python没问题

* VirtualBox：在VM中运行且up2k数据库在vboxsf中时，sqlite抛出`Disk I/O Error`
  * 使用`--hist`或`hist`卷标志（`-v [...]:c,hist=/tmp/foo`）将数据库和缩略图放在vm内部
    * 或者，如果你只想移动数据库（而不是缩略图），则使用`--dbpath`或`dbpath`卷标志
  * 在mergerfs上也会发生，所以把数据库放在别处

* Ubuntu：从某些文件夹拖拽文件到firefox或chrome是不可能的
  * 由于snap安全策略 -- 查看`snap connections firefox`的允许列表，`removable-media`显然允许所有`/mnt`和`/media`


# 重大变更

升级说明

* `1.9.16`（2023-11-04）：
  * `--stats`/prometheus：`cpp_bans`重命名为`cpp_active_bans`，那个+`cpp_uptime`是仪表
* `1.6.0`（2023-01-29）：
  * http-api：delete/move现在是`POST`而不是`GET`
  * 除了`GET`和`HEAD`之外的所有内容都必须通过[cors验证](#cors)
* `1.5.0`（2022-12-03）：大于128 GiB的文件的[新块大小公式](https://github.com/9001/copyparty/commit/54e1c8d261df)
  * **用户：** 如果你使用[cli上传器](https://github.com/9001/copyparty/blob/hovudstraum/bin/u2c.py)，请升级到最新版本
  * **开发者：** 更新第三方up2k客户端（如果那些甚至存在的话）


# 常见问题

"经常"被问到的问题

* CopyParty？
  * 不！名称要么是copyparty（全小写）要么是Copyparty -- 毕竟它是[一个词](https://en.wiktionary.org/wiki/copyparty) :>

* 我可以更改🌲旋转松树加载动画吗？
  * [是的...](https://github.com/9001/copyparty/tree/hovudstraum/docs/rice#boring-loader-spinner) :-(

* 是否可以阻止对文件夹的读取访问，除非你知道里面特定文件的确切URL？
  * 是的，使用[`g`权限](#accounts-and-volumes)，参见那里的示例
  * 你也可以用linux文件系统权限做到这一点；`chmod 111 music`将使访问`music`文件夹内的文件和文件夹成为可能，但不能列出直接内容 -- 也适用于其他软件，不仅仅是copyparty

* 我可以通过在URL中包含密码来链接某人到受密码保护的卷/文件吗？
  * 是的，通过在末尾添加`?pw=hunter2`；如果URL中已经有参数，则用`&`替换`?`，意味着它在末尾附近包含`?`
    * 如果你启用了`--usernames`，则改为`?pw=username:password`

* 如何阻止`.hist`文件夹在我的硬盘上到处出现？
  * 默认情况下，在每个卷内创建一个`.hist`文件夹用于文件系统索引、缩略图、音频转码和markdown文档历史。使用`--hist`全局选项或`hist`卷标志将其移动到其他地方；参见[数据库位置](#database-location)

* 如果我给copyparty一个URL，我可以让它下载文件到我的服务器吗？
  * 是的，使用[钩子](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/wget.py)

* firefox拒绝通过https连接，说"安全连接失败"或"SEC_ERROR_BAD_SIGNATURE"，但通常的"接受风险并继续"按钮没有显示
  * firefox已损坏其证书存储；通过退出firefox修复此问题，然后在你的firefox配置文件文件夹中找到并删除名为`cert9.db`的文件

* 当我尝试访问网站时，服务器一直说`thank you for playing`
  * 你因恶意流量被禁止了！如果这是错误发生的，并且你正在运行反向代理和/或类似cloudflare的东西，请参阅[real-ip](#real-ip)了解如何修复

* copyparty似乎认为我在使用http，即使URL是https
  * 你的反向代理没有发送`X-Forwarded-Proto: https`头；这可能是因为你的反向代理本身感到困惑。确保没有中间件（如cloudflare）在流量到达你的入口点之前终止https

* 缩略图损坏（你得到一个彩色方块，上面写着文件类型）
  * 你需要安装`FFmpeg`或`Pillow`；参见[缩略图](#thumbnails)

* 缩略图损坏（一些图像出现，但其他文件只是得到一个空白框，和/或损坏图像占位符）
  * 可能是由于反向代理搞乱请求URL并剥离查询参数（`?th=w`），所以检查你的URL重写规则
  * 也可能是由于反向代理和/或CDN中的错误缓存设置，所以确保没有设置忽略查询字符串
  * 也可能是由于行为不当的隐私相关浏览器扩展，所以尝试禁用那些

* 我想学习python和/或编程，正在考虑在那种情况下查看copyparty源代码
  * ```bash
     _|  _      __   _  _|_
    (_| (_)     | | (_)  |_
    ```


# 账户和卷

每个文件夹、每个用户的权限 - 如果你的设置变得复杂，考虑制作[配置文件](./docs/example.conf)而不是使用参数
* 更容易管理，你可以使用`systemctl reload copyparty`在运行时修改配置，或更方便地使用控制面板中的`[reload cfg]`按钮（如果用户在任何卷中有`a`/admin）
  * 对`[global]`配置部分的更改需要重启才能生效

可以使用`--help-accounts`查看快速摘要

使用参数配置账户/卷：
* `-a usr:pwd`添加账户`usr`，密码`pwd`
* `-v .::r`将当前文件夹`.`添加为webroot，任何人都可以`r`ead
  * 语法是`-v src:dst:perm:perm:...`，即本地路径、url路径和一个或多个要设置的权限
  * 向多个账户授予相同权限：  
    `-v .::r,usr1,usr2:rw,usr3,usr4` = usr1/2只读，3/4读写

权限：
* `r`（读取）：浏览文件夹内容、下载文件、下载为zip/tar、查看文件密钥/目录密钥
* `w`（写入）：上传文件、移动/复制文件*到*此文件夹
* `m`（移动）：*从*此文件夹移动文件/文件夹
* `d`（删除）：删除文件/文件夹
* `.`（点）：用户可以要求在目录列表中显示点文件
* `g`（获取）：只下载文件，无法查看文件夹内容或zip/tar
* `G`（upget）：与`g`相同，除了上传者可以看到他们自己的[文件密钥](#filekeys)（参见下面示例中的`fk`）
* `h`（html）：与`g`相同，除了文件夹返回其index.html，文件密钥对index.html不是必需的
* `a`（管理员）：可以查看上传时间、上传者IP、配置重载
* `A`（"全部"）：与`rwmda.`相同（读/写/移动/删除/管理员/点文件）

示例：
* 添加名为u1、u2、u3的账户，密码为p1、p2、p3：`-a u1:p1 -a u2:p2 -a u3:p3`
* 使文件夹`/srv`成为文件系统的根，任何人只读：`-v /srv::r`
* 使文件夹`/mnt/music`在`/music`可用，u1和u2只读，u3读写：`-v /mnt/music:music:r,u1,u2:rw,u3`
  * 访问webroot的未授权用户可以看到`music`文件夹存在，但无法打开它
* 使文件夹`/mnt/incoming`在`/inc`可用，u1只写，u2读移动：`-v /mnt/incoming:inc:w,u1:rm,u2`
  * 访问webroot的未授权用户可以看到`inc`文件夹存在，但无法打开它
  * `u1`可以打开`inc`文件夹，但无法查看内容，只能上传新文件到它
  * `u2`可以浏览它并将文件*从*`/inc`移动到`u2`有写访问权限的任何文件夹
* 使文件夹`/mnt/ss`在`/i`可用，u1读写，其他人只获取，并启用文件密钥：`-v /mnt/ss:i:rw,u1:g:c,fk=4`
  * `c,fk=4`将`fk`（[文件密钥](#filekeys)）卷标志设置为4，意味着每个文件获得一个4字符访问密钥
  * `u1`可以上传文件、浏览文件夹并查看生成的文件密钥
  * 其他用户无法浏览文件夹，但如果他们有带文件密钥的完整文件URL，可以访问文件
  * 将`g`权限替换为`wg`将让匿名用户上传文件，但看不到访问它所需的文件密钥
  * 将`g`权限替换为`wG`将让匿名用户上传文件，作为回报接收一个工作的直接链接

如果你想向所有已登录的用户授予访问权限，组`acct`将始终包含所有已知用户，例如`-v /mnt/music:music:r,@acct`

任何试图暴力破解密码的人都会根据`--ban-pw`被禁止；默认是1小时内9次失败尝试禁止24小时

如果你想使用配置文件而不是命令行参数（好！），那么这里是作为配置文件的相同示例；将其保存为`foobar.conf`并像这样使用：`python copyparty-sfx.py -c foobar.conf`

* 你也可以`PRTY_CONFIG=foobar.conf python copyparty-sfx.py`（在docker等中方便）

```yaml
[accounts]
  u1: p1  # 创建账户"u1"，密码"p1"
  u2: p2  #  （注意注释前必须有
  u3: p3  #   两个空格在#号前）

[groups]
  g1: u1, u2  # 创建一个组

[/]     # 这个URL将映射到...
  /srv  # ...服务器文件系统上的这个文件夹
  accs:
    r: *  # 每个人只读，不需要账户

[/music]       # 在这个URL创建另一个卷，
  /mnt/music   # 映射到这个文件夹
  accs:
    r: u1, u2  # 只有这些账户可以读取，
    r: @g1     # （完全相同，只是用组代替）
    r: @acct   # （或者，所有已登录的用户）
    rw: u3     # 只有u3可以读写

[/inc]
  /mnt/incoming
  accs:
    w: u1   # u1可以上传但不能查看/下载任何文件，
    rm: u2  # u2可以浏览+将文件移出此卷

[/i]
  /mnt/ss
  accs:
    rw: u1  # u1可以读写，
    g: *    # 如果知道URL，每个人都可以访问文件
  flags:
    fk: 4   # 每个文件URL将有一个4字符密码
```


## 遮蔽

通过在特定子文件夹上挂载另一个卷来隐藏它们

例如`-v /mnt::r -v /var/empty:web/certs:r`将服务器文件夹`/mnt`挂载为webroot，但另一个卷挂载在`/web/certs` -- 所以访问者只能看到`/mnt`和`/mnt/web`的内容（在URL`/`和`/web`），但看不到`/mnt/web/certs`，因为URL`/web/certs`映射到`/var/empty`

上面这一节的示例配置文件可能更好地解释这一点；第一个卷`/`映射到`/srv`，这意味着http://127.0.0.1:3923/music会尝试读取服务器文件系统上的`/srv/music`，但由于在`/music`有另一个卷映射到`/mnt/music`，它会转到`/mnt/music`

> ℹ️ 这也适用于单个文件，因为文件也可以是卷


## 点文件

通过以点开头的名称实现unix风格的隐藏文件/文件夹

如果知道名称，任何人都可以访问这些，但它们通常不会出现在目录列表中

如果指定了全局选项`-ed`，或卷有卷标志`dots`，或用户有权限`.`，客户端可以请求在目录列表中查看点文件

除非上述之一为真，**并且**设置了全局选项/卷标志`dotsrch`，否则点文件不会出现在搜索结果中

> 即使用户有查看点文件的权限，除非设置了`--see-dots`，和/或用户在设置标签中启用了`dotfiles`选项，否则它们默认隐藏

配置文件示例，其中以两种不同方式给出查看点文件的相同权限，仅供参考：

```yaml
[/foo]
  /srv/foo
  accs:
    r.: ed   # 用户"ed"在此卷中有读访问权限+点访问权限；
             # 点文件在列表中可见，但在搜索中不可见
  flags:
    dotsrch  # 点文件现在也会出现在搜索结果中
    dots     # 让每个人在此卷中查看点文件的另一种方式
```
# 浏览器

使用网络浏览器访问copyparty服务器

![copyparty-browser-fs8](https://user-images.githubusercontent.com/241032/192042695-522b3ec7-6845-494a-abdb-d1c0d0e23801.png)


## 标签页

UI中的主要标签页
* `[🔎]` 按大小、日期、路径/名称、mp3标签等[搜索](#searching)...
* `[🧯]` [撤销](#unpost)：撤销/删除意外上传
* `[🚀]`和`[🎈]`是[上传器](#uploading)
* `[📂]` mkdir：创建目录
* `[📝]` new-md：创建新的markdown文档
* `[📟]` send-msg：发送到服务器日志或如果`--urlform save`则发送到文本文件
* `[🎺]` 音频播放器配置选项
* `[⚙️]` 一般客户端配置选项


## 热键

浏览器有以下热键（始终是qwerty）
* `?` 显示热键帮助
* `B` 切换面包屑导航/[导航面板](#navpane)
* `I/K` 上一个/下一个文件夹
* `M` 父文件夹（或收起当前）
* `V` 在导航面板中切换文件夹/文本文件
* `G` 切换列表/[网格视图](#thumbnails) -- 与右下角的`田`相同
* `T` 切换缩略图/图标
* `ESC` 关闭各种东西
* `ctrl-K` 删除选定的文件/文件夹
* `ctrl-X` 剪切选定的文件/文件夹
* `ctrl-C` 复制选定的文件/文件夹到剪贴板
* `ctrl-V` 粘贴（移动/复制）
* `Y` 下载选定的文件
* `F2` [重命名](#batch-rename)选定的文件/文件夹
* 当选择了文件/文件夹时（在非网格视图中）：
  * `Up/Down` 移动光标
  * shift+`Up/Down` 选择并移动光标
  * ctrl+`Up/Down` 移动光标并滚动视口
  * `Space` 切换文件选择
  * `Ctrl-A` 切换全选
* 当打开文本文件时：
  * `I/K` 上一个/下一个文本文件
  * `S` 切换打开文件的选择
  * `M` 关闭文本文件
* 当播放音频时：
  * `J/L` 上一首/下一首歌
  * `U/O` 向后/向前跳过10秒
  * `0..9` 跳转到0%..90%
  * `P` 播放/暂停（也开始播放文件夹）
  * `Y` 下载文件
* 当查看图像/播放视频时：
  * `J/L, Left/Right` 上一个/下一个文件
  * `Home/End` 第一个/最后一个文件
  * `F` 切换全屏
  * `S` 切换选择
  * `R` 顺时针旋转（shift=逆时针）
  * `Y` 下载文件
  * `Esc` 关闭查看器
  * 视频：
    * `U/O` 向后/向前跳过10秒
    * `0..9` 跳转到0%..90%
    * `P/K/Space` 播放/暂停
    * `M` 静音
    * `C` 继续播放下一个视频
    * `V` 循环整个文件
    * `[` 循环范围（开始）
    * `]` 循环范围（结束）
* 当导航面板打开时：
  * `A/D` 调整树宽度
* 在[网格视图](#thumbnails)中：
  * `S` 切换多选
  * shift+`A/D` 缩放
* 在markdown编辑器中：
  * `^s` 保存
  * `^h` 标题
  * `^k` 自动格式化表格
  * `^u` 跳转到下一个unicode字符
  * `^e` 切换编辑器/预览
  * `^up, ^down` 跳转段落


## 导航面板

在面包屑导航或导航面板之间切换

点击`🌲`或按`B`热键在面包屑路径（默认）或导航面板（树浏览器侧边栏）之间切换

* `[+]`和`[-]`（或热键`A`/`D`）调整大小
* `[🎯]` 跳转到当前打开的文件夹
* `[📃]` 在显示文件夹和文本文件之间切换
* `[📌]` 在停靠面板中显示所有父文件夹的名称
* `[a]` 切换随着深入自动加宽
* `[↵]` 切换自动换行
* `[👀]` 悬停时显示全名（如果自动换行关闭）


## 缩略图

按`g`或`田`切换网格视图而不是文件列表，`t`切换图标/缩略图
* 可以使用`--grid`全局设为默认，或使用卷标志`grid`按卷设置
* 通过在链接中添加`?imgs`启用，或使用`?imgs=0`禁用

![copyparty-thumbs-fs8](https://user-images.githubusercontent.com/241032/129636211-abd20fa2-a953-4366-9423-1c88ebb96ba9.png)

它使用Pillow / pyvips / FFmpeg处理静态图像，使用FFmpeg处理视频文件，所以你可能想要`--no-thumb`或者只是`--no-vthumb`，这取决于你的用户有多危险
* pyvips比Pillow快3倍，Pillow比FFmpeg快3倍
* 使用卷标志`dthumb`禁用特定卷的所有缩略图，或使用`dvthumb` / `dathumb` / `dithumb`仅禁用视频/音频/图像
* 在Windows上安装FFmpeg，请参阅[可选依赖项](#optional-dependencies)

音频文件使用FFmpeg转换为频谱图，除非你使用`--no-athumb`（一些FFmpeg构建可能需要`--th-ff-swr`）

具有以下名称的图像（参见`--th-covers`）成为它们所在文件夹的缩略图：`folder.png`、`folder.jpg`、`cover.png`、`cover.jpg`
* 顺序很重要，所以如果文件夹中同时存在`cover.png`和`folder.jpg`，它会选择第一个匹配的`--th-covers`条目（`folder.jpg`）
* 如果你启用[文件索引](#file-indexing)，它还会尝试这些名称作为点文件（`.folder.jpg`等），然后回退到文件夹中的第一张图片（如果有任何图片的话）

启用`multiselect`让你点击文件来选择它们，然后shift-点击另一个文件进行范围选择
* `multiselect`主要用于手机/平板电脑，但`[⚙️] settings`标签中的`sel`选项更适合桌面使用，允许通过CTRL-点击选择和SHIFT-点击范围选择，所有这些都不影响常规点击
  * `sel`选项可以使用`--gsel`全局设为默认，或使用卷标志`gsel`按卷设置

要显示`/icons/exe.png`和`/icons/elf.gif`分别作为所有`.exe`和`.elf`文件的缩略图，这样做：`--ext-th=exe=/icons/exe.png --ext-th=elf=/icons/elf.gif`
* 可选地作为每个映射的单独卷标志；参见下面的配置文件示例
* 支持的图像格式是[jpg, png, gif, webp, ico](https://developer.mozilla.org/en-US/docs/Web/Media/Guides/Formats/Image_types)
  * 小心svg；如果你在同一页面上显示太多唯一的svg文件，chrome会崩溃（限制大约是250个） -- 但是显示同样的几个svg文件数千次是可以的

配置文件示例：

```yaml
[global]
  no-thumb   # 禁用所有缩略图和音频转码
  no-vthumb  # 只禁用视频缩略图

[/music]
  /mnt/nas/music
  accs:
    r: *     # 每个人都可以读取
  flags:
    dthumb   # 禁用所有缩略图和音频转码
    dvthumb  # 只禁用视频缩略图
    ext-th:  exe=/ico/exe.png  # /ico/exe.png是*.exe的缩略图
    ext-th:  elf=/ico/elf.gif  # ...而/ico/elf.gif用于*.elf
    th-covers:  folder.png,folder.jpg,cover.png,cover.jpg  # 默认值
```


## zip下载

将文件夹（或文件选择）下载为`zip`或`tar`文件

在`[⚙️] config`标签中选择你想要的存档类型：

| 名称 | url后缀 | 描述 |
|--|--|--|
| `tar` | `?tar` | 纯gnutar，与`curl \| tar -xv`配合很好 |
| `pax` | `?tar=pax` | pax格式tar，面向未来，不那么快 |
| `tgz` | `?tar=gz` | gzip压缩的gnu-tar（慢），用于`curl \| tar -xvz` |
| `txz` | `?tar=xz` | 带xz / lzma压缩的gnu-tar（非常慢） |
| `zip` | `?zip` | 到处都能用，win7及更旧版本上文件名有问题 |
| `zip_dos` | `?zip=dos` | 传统cp437（无unicode）修复有问题的文件名 |
| `zip_crc` | `?zip=crc` | cp437，早期计算crc32，用于真正古老的软件 |

* gzip默认级别是`3`（0=快，9=最佳），使用`?tar=gz:9`更改
* xz默认级别是`1`（0=快，9=最佳），使用`?tar=xz:9`更改
* bz2默认级别是`2`（1=快，9=最佳），使用`?tar=bz2:9`更改
* 隐藏文件（[点文件](#dotfiles)）被排除，除非账户被允许列出它们
  * `up2k.db`和`dir.txt`总是被排除
* bsdtar支持流式解压：`curl foo?zip | bsdtar -xv`
  * 很好，因为copyparty的zip在小文件上比tar更快
    * 但`?tar`对大文件更好，特别是如果总计超过4 GiB
* `zip_crc`下载时间会更长，因为服务器必须读取每个文件两次
  * 这只是为了支持MS-DOS PKZIP v2.04g（1993年10月）及更旧版本
    * 你实际上是如何访问copyparty的

你也可以通过在浏览器中点击文件或文件夹来压缩选择，这会在右下角弹出选择编辑器和zip按钮

![copyparty-zipsel-fs8](https://user-images.githubusercontent.com/241032/129635374-e5136e01-470a-49b1-a762-848e8a4c9cdc.png)

酷技巧：通过附加url参数`?tar&opus`或`?tar&mp3`下载文件夹，在添加到存档之前将所有音频文件（除了aac|m4a|mp3|ogg|opus|wma）转码为opus/mp3
* 如果你距离起飞还有5分钟，意识到你的手机上没有音乐，但你的服务器只有flac文件，下载这些会耗尽你所有的数据+反正也没有足够的时间，这非常有用
* url参数`&j` / `&w`产生jpeg/webm缩略图/频谱图而不是原始音频/视频/图像（`&p`用于音频波形）
  * 也可以用来预生成缩略图；与`--th-maxage=9999999`或`--th-clean=0`结合使用


## 上传

将文件/文件夹拖入网络浏览器进行上传

拖放是推荐的方式，但你也可以：

* 在文件资源管理器中选择一些文件（不是文件夹）并在浏览器窗口内按CTRL-V
* 使用[命令行上传器](https://github.com/9001/copyparty/tree/hovudstraum/bin#u2cpy)
* 使用[curl, sharex, ishare, ...](#client-examples)上传

通过拖放或CTRL-V上传文件时，这会启动使用`up2k`的上传；有两个基于浏览器的上传器可用：
* `[🎈] bup`，基础上传器，支持自netscape 4.0以来的几乎每个浏览器
* `[🚀] up2k`，好的/花哨的那个

注意：你可以使用`[🧯]` [撤销](#unpost)来撤销/删除你自己的上传（这也是你中止未完成上传的地方，但你必须先刷新页面）

up2k有几个优势：
* 你可以将文件夹拖入浏览器（文件递归添加）
* 文件以块处理，每个块都有校验和
  * 如果上传被网络问题中断，会自动恢复
  * 如果你重启浏览器或电脑，上传会恢复，只需再次上传相同的文件
  * 服务器检测任何损坏；客户端重新上传受影响的块
  * 客户端不会上传服务器上已经存在的任何内容
  * 没有文件大小限制，即使代理限制请求大小（例如Cloudflare）
* 在某些互联网连接上（主要是美国的）比ftp/scp/tarpipe速度高得多，这要归功于并行连接
* 文件的最后修改时间戳被保留

> 在有人上传时重启/升级copyparty是完全安全的！  
> 所有已知的up2k客户端都会很好地恢复 💪

参见[up2k](./docs/devnotes.md#up2k)了解它如何工作的详细信息，或观看[演示视频](https://a.ocv.me/pub/demo/pics-vids/#gf-0f6f5c0d)

![copyparty-upload-fs8](https://user-images.githubusercontent.com/241032/129635371-48fc54ca-fa91-48e3-9b1d-ba413e4b68cb.png)

**专业提示：** 你可以使用[contrib/plugins/minimal-up2k.js](contrib/plugins/minimal-up2k.js)避免吓跑用户，它使界面看起来[更简单](https://user-images.githubusercontent.com/241032/118311195-dd6ca380-b4ef-11eb-86f3-75a3ff2e1332.png)

**专业提示：** 如果你在`[⚙️] settings`标签中启用`favicon`（通过在文本框中输入内容），浏览器标签中的图标将指示上传进度 -- 另外，`[🔔]`和/或`[🔊]`开关启用上传完成时的可见和/或可听通知

up2k UI是精致直观体验的缩影：
* "parallel uploads"指定同时上传多少个块
* `[🏃]` 在一个文件上传时，其他文件的分析应该继续
* `[🥔]` 为慢速设备显示更简单的UI以便更快上传
* `[🛡️]` 决定何时覆盖服务器上的现有文件
  * `🛡️` = 从不（改为生成新文件名）
  * `🕒` = 如果服务器文件更旧则覆盖
  * `♻️` = 如果文件不同则总是覆盖
* `[🎲]` 在上传期间生成随机文件名
* `[🔎]` 在上传和[文件搜索](#file-search)模式之间切换
  * 如果你通过拖拽将文件添加到浏览器中，请忽略`[🔎]`

然后是下面的标签页，
* `[ok]` 是成功完成的文件
* `[ng]` 是失败/被拒绝的文件（已存在，...）
* `[done]` 显示`[ok]`和`[ng]`的组合列表，按时间顺序
* `[busy]` 当前正在哈希、等待上传或上传的文件
  * 加上来自`[done]`和`[que]`的最多3个条目作为上下文
* `[que]` 是所有仍在队列中的文件

注意，由于up2k必须读取每个文件两次，在某些极端情况下`[🎈] bup`理论上可以快2倍（文件比你的RAM大，结合比你的硬盘读取速度更快的互联网连接，或者如果你从cuo2duo上传）

如果你正在恢复大量上传并想跳过已经完成的文件的哈希，你可以在`[⚙️] config`标签中启用`turbo`，但请阅读该按钮上的工具提示

如果服务器在施加请求大小限制的代理后面，你可以使用服务器选项`--u2sz`配置up2k偷偷溜到限制以下（默认是96 MiB以支持Cloudflare）

如果你想默认用新上传替换服务器上的现有文件，使用`--u2ow 2`运行（只有在用户有删除权限时才有效，仍然可以在UI中用`🛡️`禁用）


### 文件搜索

将文件拖入浏览器还可以让你查看它们是否存在于服务器上

![copyparty-fsearch-fs8](https://user-images.githubusercontent.com/241032/129635361-c79286f0-b8f1-440e-aaf4-6e929428fac9.png)

当你将文件拖放到浏览器中时，你会看到两个拖放区：`Upload`和`Search`

> 在手机上？在点击大黄色搜索按钮选择文件之前，将`[🔎]`开关切换为绿色

文件将在客户端进行哈希，每个哈希发送到服务器，服务器检查该文件是否存在于某处

如果文件存在，它们进入`[ok]`（你会得到它所在位置的链接），否则它们进入`[ng]`
* 文件搜索与上传器结合的主要原因是代码太意大利面条了，无法分离到其他地方，现在不再是这种情况，但现在我也太喜欢这个想法了


### 撤销

使用UI中的`[🧯]`标签撤销/删除意外上传

![copyparty-unpost-fs8](https://user-images.githubusercontent.com/241032/129635368-3afa6634-c20f-418c-90dc-ec411f3b3897.png)

即使你没有常规的移动/删除访问权限，你也可以撤销，但只能撤销在过去`--unpost`秒内上传的文件（默认12小时），服务器必须使用`-e2d`运行

配置文件示例：

```yaml
[global]
  e2d            # 启用up2k数据库（记住上传）
  unpost: 43200  # 12小时（默认）
```


### 自毁

上传可以设置生存期，之后它们过期/自毁

该功能必须使用`lifetime` [上传规则](#upload-rules)按卷启用，该规则设置文件在服务器上停留时间的上限

客户端可以使用[up2k ui](#uploading)指定更短的过期时间 -- 相关选项在导航到启用了`lifetimes`的文件夹时变得可见 -- 或使用`life` [上传修饰符](./docs/devnotes.md#write)

客户端指定自定义过期时间将影响允许撤销的时间跨度，所以请关注up2k ui中的估计


### 竞速传输

在文件仍在上传时下载文件（[演示视频](http://a.ocv.me/pub/g/nerd-stuff/cpp/2024-0418-race-the-beam.webm)） -- 这几乎像点对点

需要使用up2k上传文件（这是默认的拖放上传器），或者使用命令行程序


### 传入文件

控制面板显示所有传入文件的预计到达时间，但只显示上传到你有读取权限的卷中的文件

![copyparty-cpanel-upload-eta-or8](https://github.com/user-attachments/assets/fd275ffa-698c-4fca-a307-4d2181269a6a)


## 文件管理器

剪切/粘贴、重命名和删除文件/文件夹（如果你有权限）

文件选择：点击行上的某处（不是链接本身），然后：
* `space` 切换
* `up/down` 移动
* `shift-up/down` 移动并选择
* `ctrl-shift-up/down` 也滚动
* shift-点击另一行进行范围选择

* 剪切：选择一些文件并按`ctrl-x`
* 复制：选择一些文件并按`ctrl-c`
* 粘贴：在另一个文件夹中按`ctrl-v`
* 重命名：`F2`

你可以跨浏览器标签复制/移动文件（在一个标签中剪切/复制，在另一个标签中粘贴）


## 分享

通过创建临时链接分享文件或文件夹

在服务器设置中启用时（`--shr`），点击右下角的`share`按钮分享你当前所在的文件夹，或者：
* 先选择一个文件夹来分享那个文件夹
* 选择一个或多个文件来只分享那些文件

此功能是考虑到[身份提供者](#identity-providers)而制作的 -- 配置你的反向代理跳过IdP对给定URL前缀的访问控制，并使用它来安全地分享特定文件/文件夹而无需通常的认证检查

创建分享时，创建者可以选择以下任何选项：

* 密码保护
* 在一定时间后过期；`0`或空白表示无限
* 允许访问者上传（如果创建分享的用户有写权限）

半故意的限制：

* 过期分享的清理只有在设置了全局选项`e2d`和/或服务器上至少有一个卷有卷标志`e2d`时才有效
* 只分享来自同一卷的文件夹；如果你分享的文件夹包含其他卷，那些卷的内容将不可用
* 如果你在创建受密码保护的分享后更改[密码哈希](#password-hashing)设置，那个分享将停止工作
* 与[IdP卷在关闭时被遗忘](https://github.com/9001/copyparty/blob/hovudstraum/docs/idp.md#idp-volumes-are-forgotten-on-shutdown)相关，任何指向用户IdP卷的分享在重启后将不可用，直到该用户在重启后发出第一个请求
* 没有"首次访问后删除"选项，因为很棘手
  * 当链接某些东西到discord（例如）时，它会被他们的爬虫访问，那会算作一次点击
  * 除非请求者的IP被允许X分钟，否则浏览器无法恢复中断的下载（参考：棘手）

指定`--shr /foobar`启用此功能；然后创建一个名为`foobar`的顶级虚拟文件夹，所有分享都将从那里提供

* 你可以随意命名，`foobar`只是一个例子
* 如果你使用配置文件，在`[global]`部分内放入`shr: /foobar`

用户可以在控制面板中删除自己的分享，特权用户列表（`--shr-adm`）被允许查看和/或删除服务器上的任何分享

分享过期后，它在控制面板中保持可见`--shr-rt`分钟（默认是1天），所有者可以通过在那里延长过期时间来恢复它

**安全注意：** 使用此功能并不意味着你可以跳过[账户和卷](#accounts-and-volumes)部分 -- 你仍然需要限制对你不打算与未认证用户分享的卷的访问！仅在反向代理中使用规则限制对`/share`文件夹的访问是不够的。


## 批量重命名

选择一些文件并按`F2`打开重命名UI

![batch-rename-fs8](https://user-images.githubusercontent.com/241032/128434204-eb136680-3c07-4ec7-92e0-ae86af20c241.png)

按钮的快速说明，  
* `[✅ apply rename]` 确认并开始重命名
* `[❌ cancel]` 中止并关闭重命名窗口
* `[↺ reset]` 将任何文件名更改恢复到原始名称
* `[decode]` 对文件名进行URL解码，修复像`&amp;`和`%20`这样的东西
* `[advanced]` 切换高级模式

高级模式：基于规则重命名文件以决定新名称，基于原始名称（正则表达式），或基于从文件收集的标签（艺术家/标题/...），或两者的混合

在高级模式中，  
* `[case]` 切换大小写敏感的正则表达式
* `regex` 是应用于原始文件名的正则表达式模式；任何不匹配的文件将被跳过
* `format` 是新文件名，从正则表达式捕获组和/或文件标签中取值
  * 非常松散地基于foobar2000语法
* `presets` 让你保存重命名规则以供以后使用

可用函数：
* `$lpad(text, length, pad_char)`
* `$rpad(text, length, pad_char)`

所以，

假设你有一个名为[`meganeko - Eclipse - 07 Sirius A.mp3`](https://www.youtube.com/watch?v=-dtb0vDPruI)的文件（顺便说一下，绝对精彩的专辑），标签是：`Album:Eclipse`，`Artist:meganeko`，`Title:Sirius A`，`tn:7`

你可以只使用正则表达式重命名它：
* `regex` = `(.*) - (.*) - ([0-9]{2}) (.*)`
* `format` = `(3). (1) - (4)`
* `output` = `07. meganeko - Sirius A.mp3`

或者你可以只使用标签：
* `format` = `$lpad((tn),2,0). (artist) - (title).(ext)`
* `output` = `7. meganeko - Sirius A.mp3`

或者两者混合：
* `regex` = ` - ([0-9]{2}) `
* `format` = `(1). (artist) - (title).(ext)`
* `output` = `07. meganeko - Sirius A.mp3`

你可以在格式字段中使用的元数据键是文件浏览器表头中的那些（用`-mte`和`-mtp`收集的任何内容）


## RSS订阅

使用RSS阅读器监控文件夹，可选递归

必须使用卷标志`rss`按卷启用或使用`--rss`全局启用

订阅包含iTunes元数据，用于播客阅读器如[AntennaPod](https://antennapod.org/)

订阅示例：https://cd.ocv.me/a/d2/d22/?rss&fext=mp3

URL参数：

* `pw=hunter2` 用于密码认证
  * 如果你启用了`--usernames`，则改为`pw=username:password`
* `recursive` 也包括子文件夹
* `title=foo` 更改订阅标题（默认：文件夹名称）
* `fext=mp3,opus` 只包括mp3和opus文件（默认：全部）
* `nf=30` 只显示前30个结果（默认：250）
* `sort=m` 按mtime（文件最后修改时间）排序，最新的在前（默认）
  * `u` = 上传时间；注意：非上传文件的上传时间为`0`
  * `n` = 文件名
  * `a` = 文件大小
  * 大写 = 反向排序；`M` = 最旧的文件在前


## 最近上传

通过点击控制面板中的"显示最近上传"列出所有最近的上传

如果访问者有管理员权限，将显示上传者IP和上传时间

* 全局选项`--ups-when`使上传时间对所有用户可见，而不仅仅是管理员

* 全局选项`--ups-who`（卷标志`ups_who`）指定谁获得访问权限（0=没有人，1=管理员，2=每个人），默认=2

注意[🧯 撤销](#unpost)功能更适合查看*你自己的*最近上传，因为它包括撤销/删除它们的选项

配置文件示例：

```yaml
[global]
  ups-when    # 每个人都可以看到上传时间
  ups-who: 1  # 但只有管理员可以看到列表，
              # 所以ups-when不生效
```


## 媒体播放器

播放几乎所有音频格式（如果服务器安装了FFmpeg用于按需转码）

以下音频格式通常总是可播放的，即使没有FFmpeg：`aac|flac|m4a|mp3|ogg|opus|wav`

一些亮点：
* 操作系统集成；从手机锁屏控制播放（[windows](https://user-images.githubusercontent.com/241032/233213022-298a98ba-721a-4cf1-a3d4-f62634bc53d5.png) // [iOS](https://user-images.githubusercontent.com/241032/142711926-0700be6c-3e31-47b3-9928-53722221f722.png) // [android](https://user-images.githubusercontent.com/241032/233212311-a7368590-08c7-4f9f-a1af-48ccf3f36fad.png)）
* 在搜索栏中显示音频波形
* 不是完全无缝但可以非常接近（参见下面的设置+均衡器）；足以按预期享受无缝专辑
* 视频可以作为音频播放，不浪费视频带宽

点击音频文件旁边的`play`链接，或复制链接目标来[分享它](https://a.ocv.me/pub/demo/music/Ubiktune%20-%20SOUNDSHOCK%202%20-%20FM%20FUNK%20TERRROR!!/#af-1fbfba61&t=18)（可选地带有开始播放的时间戳，就像那个例子一样）

打开`[🎺]`媒体播放器设置标签来配置它，
* "开关"：
  * `[🔁]` 永远重复一首歌
  * `[🔀]` 随机播放每个文件夹内的文件
  * `[preload]` 在即将结束时开始加载下一首曲目，减少歌曲之间的静音
  * `[full]` 通过下载整个下一个文件进行完整预加载；对不可靠的连接好，对慢连接不好
  * `[~s]` 切换搜索栏波形显示
  * `[/np]` 启用按钮将正在播放的信息复制为irc消息
  * `[📻]` 启用按钮用选定的歌曲创建[m3u播放列表](#playlists)
  * `[os-ctl]` 使从设备锁屏控制音频播放成为可能（启用[mediasession](https://developer.mozilla.org/en-US/docs/Web/API/MediaSession)）
  * `[seek]` 允许使用锁屏控制搜索（在某些设备上有问题）
  * `[art]` 在锁屏上显示专辑封面
  * `[🎯]` 保持正在播放的歌曲滚动到视图中（在将播放器用作任务栏停靠时很好）
  * `[⟎]` 缩小播放控制
* "按钮"：
  * `[uncache]` 可能修复由于浏览器缓存中的坏文件而无法正确播放的歌曲
* "文件夹结束时"：
  * `[loop]` 保持循环文件夹
  * `[next]` 播放到下一个文件夹
* "转码"：
  * `[flac]` 将`flac`和`wav`文件转换为opus（如果浏览器支持）或mp3
  * `[aac]` 将`aac`和`m4a`文件转换为opus（如果浏览器支持）或mp3
  * `[oth]` 将所有其他已知格式转换为opus（如果浏览器支持）或mp3
    * `aac|ac3|aif|aiff|alac|alaw|amr|ape|au|dfpwm|dts|flac|gsm|it|m4a|mo3|mod|mp2|mp3|mpc|mptm|mt2|mulaw|ogg|okt|opus|ra|s3m|tak|tta|ulaw|wav|wma|wv|xm|xpk`
* "转码为"：
  * `[opus]` 在需要转码时产生`opus`（在Android和PC上的最佳选择）
  * `[awo]` 是`weba`文件中的`opus`，对iPhone好（iOS 17.5及更新版本），但Apple仍在修复一些状态混乱错误，截至iOS 18.2.1
  * `[caf]` 是`caf`文件中的`opus`，对iPhone好（iOS 11到17），技术上不被Apple支持但大部分工作
  * `[mp3]` -- 神话、传说、平庸音质的不朽大师，绝对在任何地方都能工作
  * `[flac]` -- 无损但压缩，用于静电耳机的局域网和/或光纤播放
  * `[wav]` -- 无损且未压缩，用于连接到非常旧设备的静电耳机的局域网和/或光纤播放
    * `flac`和`wav`必须使用`--allow-flac` / `--allow-wav`启用以允许花费磁盘空间
* "tint"减少播放栏的对比度


### 播放列表

创建和播放[m3u8](https://en.wikipedia.org/wiki/M3U)播放列表 -- 参见示例[文本](https://a.ocv.me/pub/demo/music/?doc=example-playlist.m3u)和[播放器](https://a.ocv.me/pub/demo/music/#m3u=example-playlist.m3u)

点击扩展名为`m3u`或`m3u8`的文件（例如`mixtape.m3u`或`touhou.m3u8`），你会得到两个选择：播放/编辑

播放列表可以包括服务器上任何地方文件夹中的歌曲，但不支持文件密钥/目录密钥，所以听众必须有对文件的读取权限或获取权限


### 创建播放列表

使用独立媒体播放器或copyparty

你可以使用foobar2000、deadbeef，几乎任何独立播放器都应该工作 -- 但你可能需要编辑播放列表中的文件路径，使它们适合服务器URL

或者，你可以使用copyparty本身创建播放列表：

* 打开`[🎺]`媒体播放器设置标签并启用`[📻]`创建播放列表功能 -- 这在右下角托盘中添加两个新按钮，`[📻add]`和`[📻copy]`，当你听音乐或选择一些音频文件时出现

* 在播放歌曲时（或选择一些歌曲时）点击`📻add`按钮，它们将被添加到"列表"中（你还看不到它）

* 随时点击`📻copy`将播放列表发送到剪贴板
  * 如果你愿意，你可以继续添加更多歌曲
  * 如果你想清空播放列表并从头开始，只需刷新页面

* 创建一个新的文本文件，命名为`something.m3u`并在那里粘贴播放列表


### 音频均衡器

和[动态范围压缩器](https://en.wikipedia.org/wiki/Dynamic_range_compression)

也可以总体提升音量，或增加/减少立体声宽度（像[crossfeed](https://www.foobar2000.org/components/view/foo_dsp_meiercf)只是更差）

有减少歌曲之间暂停的方便副作用，所以无缝专辑在启用均衡器时播放得更好（只需使其平坦）

在iPhone / iPad上不可用，因为AudioContext目前在iOS（15.7.8）上破坏后台音频播放


### 修复安卓上不可靠的播放

由于手机/应用设置，安卓手机可能在省电模式启动时随机停止播放音乐，特别是在专辑结束时 -- 你可以通过在用于音乐流的浏览器的[应用设置](https://user-images.githubusercontent.com/241032/235262121-2ffc51ae-7821-4310-a322-c3b7a507890c.png)中[禁用省电](https://user-images.githubusercontent.com/241032/235262123-c328cca9-3930-4948-bd18-3949b9fd3fcf.png)来修复它（最好是专用的）


## 文本文件查看器

实时流式传输日志文件等（[演示](https://a.ocv.me/pub/demo/logtail/)），终端颜色也能工作

点击文本文件旁边的`-txt-`打开查看器，它有以下工具栏按钮：

* `✏️ edit` 打开文本文件编辑器
* `📡 follow` 开始监控文件的更改，实时流式传输新行
  * 类似于`tail -f`
  * 通过在文本查看器URL中添加`&tail`[直接链接](https://a.ocv.me/pub/demo/logtail/?doc=lipsum.txt&tail)到启用了跟踪的文件


## markdown查看器

有*两个*编辑器

![copyparty-md-read-fs8](https://user-images.githubusercontent.com/241032/115978057-66419080-a57d-11eb-8539-d2be843991aa.png)

有一个内置的内联可点击缩略图扩展；
* 通过在文档中某处添加`<!-- th -->`启用它
* 使用`!th[l](your.jpg)`添加缩略图，其中`l`表示左对齐（`r` = 右对齐）
* 带有`---`的单行清除浮动/内联
* 在文件列表下方显示README.md的情况下，缩略图将在画廊查看器中打开

其他注意事项，
* 文档预览有最大宽度，打印时与A4纸相同


### markdown变量

带有服务器端变量扩展的动态文档，用`{{self.ip}}`替换客户端IP，或用`{{srv.htime}}`替换服务器当前时间

参见[./srv/expand/](./srv/expand/)了解用法和示例


## 其他技巧

* 你可以通过在URL中添加时间戳来链接音频文件中的特定时间戳，例如在`.../#af-c8960dab`后添加`&20` / `&20s` / `&1m20` / `&t=1:20`

* 启用音频均衡器可以帮助在某些浏览器（chrome）中使无缝专辑完全无缝，所以考虑将所有值设为零并保持开启

* 通过在URL中添加`?ls=t`获得纯文本文件列表，或使用`?ls=v`获得紧凑的彩色列表（用于unix终端）
* 如果你使用媒体热键切换歌曲并厌倦了看到Windows不让你禁用的OSD弹出窗口，考虑[./contrib/media-osd-bgone.ps1](contrib/#media-osd-bgoneps1)

* 点击左下角的`π`打开javascript提示符进行调试

* 名为`.prologue.html` / `.epilogue.html`的文件将在目录列表之前/之后渲染，除非使用`--no-logues`

* 名为`descript.ion` / `DESCRIPT.ION`的文件被解析并显示在文件列表中，如果非标准则作为结语

* 名为`README.md` / `readme.md`的文件将在目录列表后渲染，除非使用`--no-readme`（但`.epilogue.html`优先）

  * `PREADME.md` / `preadme.md`显示在目录列表上方，除非使用`--no-readme`或`.prologue.html`

* `README.md`和`*logue.html`可以包含占位符值，在嵌入目录列表之前在服务器端替换；参见`--help-exp`


## 搜索

按大小、日期、路径/名称、mp3标签等搜索...

![copyparty-search-fs8](https://user-images.githubusercontent.com/241032/129635365-c0ff2a9f-0ee5-4fc3-8bb6-006033cf67b8.png)

使用`-e2dsa`启动时，copyparty将扫描/索引你的所有文件。这避免了上传时的重复，也使卷可以通过web-ui搜索：
* 通过`size`/`date`/`directory-path`/`filename`进行搜索查询，或...
* 拖放本地文件查看服务器上是否存在相同内容，参见[文件搜索](#file-search)

路径/名称查询是空格分隔的，AND在一起，单词用`-`前缀否定，例如：
* path: `shibayan -bossa` 找到所有文件夹包含`shibayan`但过滤掉路径中任何地方存在`bossa`的结果
* name: `demetori styx` 给你[好东西](https://www.youtube.com/watch?v=zGh0g14ZJ8I&list=PL3A147BD151EE5218&index=9)

`raw`字段允许更复杂的内容，如`( tags like *nhato* or tags like *taishi* ) and ( not tags like *nhato* or not tags like *taishi* )`，它找到nhato或taishi的所有歌曲，排除合作（糟糕的例子，你为什么要这样做）

为了让上面的例子工作，添加命令行参数`-e2ts`也扫描/索引音乐文件的标签，这带我们到：


# 服务器配置

使用参数或配置文件，或两者混合：
* 配置文件（`-c some.conf`）可以设置额外的命令行参数；参见[./docs/example.conf](docs/example.conf)和[./docs/example2.conf](docs/example2.conf)
* `kill -s USR1`（与`systemctl reload copyparty`相同）从配置文件重新加载账户和卷而不重启
  * 或如果用户在任何卷中有`a`/admin，点击控制面板中的`[reload cfg]`按钮
  * 对`[global]`配置部分的更改需要重启才能生效

**注意：** 尽管这个readme很庞大，但还有很多未记录的功能。使用`--help`运行copyparty查看所有可用的全局选项；所有这些都可以在配置文件的`[global]`部分使用，`--help-flags`中列出的所有内容都可以在卷中用作卷标志。
* 如果在docker/podman中运行，试试：`docker run --rm -it copyparty/ac --help`
* 或查看：https://ocv.me/copyparty/helptext.html
* 或如果你更喜欢纯文本，https://ocv.me/copyparty/helptext.txt


## 零配置

在局域网上宣布启用的服务（[图片](https://user-images.githubusercontent.com/241032/215344737-0eae8d98-9496-4256-9aa8-cd2f6971810d.png)） -- `-z`启用[mdns](#mdns)和[ssdp](#ssdp)

* `--z-on` / `--z-off` 将功能限制到某些网络

配置文件示例：

```yaml
[global]
  z      # 启用所有零配置功能（mdns，ssdp）
  zm     # 只启用mdns（什么都不做，因为我们已经有z了）
  z-on: 192.168.0.0/16, 10.1.2.0/24  # 限制到某些子网
```


### mdns

局域网域名和功能宣布器

使用[多播dns](https://en.wikipedia.org/wiki/Multicast_DNS)给copyparty一个域名，局域网上的任何机器都可以使用它来访问

所有启用的服务（[webdav](#webdav-server)，[ftp](#ftp-server)，[smb](#smb-server)）将出现在支持mDNS的文件管理器中（KDE，gnome，macOS，...）

如果机器的主机名是`partybox`，域名将是`partybox.local`，除非`--name`指定其他内容

web-UI将在http://partybox.local:3923/可用

* 如果你想去掉`:3923`以便可以使用http://partybox.local/，那么参见[监听端口80和443](#listen-on-port-80-and-443)


### ssdp

windows资源管理器宣布器

使用[ssdp](https://en.wikipedia.org/wiki/Simple_Service_Discovery_Protocol)使copyparty出现在局域网上所有机器的windows文件资源管理器中

双击图标打开"连接"页面，解释如何将copyparty挂载为本地文件系统

如果copyparty没有出现在windows资源管理器中，使用`--zsv`查看原因：

* 也许发现多播是从与服务器子网不相交的IP发送的


## 二维码

打印二维码（[截图](https://user-images.githubusercontent.com/241032/194728533-6f00849b-c6ac-43c6-9359-83e454d11e00.png)）以便快速访问，在不断更改子网的安卓热点上的手机之间很棒

* `--qr` 启用它
* `--qrs` 使用https而不是http
* `--qrl lootbox/?pw=hunter2` 附加到url，链接到带密码`hunter2`的`lootbox`文件夹
* `--qrz 1` 强制1x缩放而不是自动缩放以适应终端大小
  * 1x可能在某些终端/字体上渲染不正确，但2x应该总是工作
* `--qr-pin 1` 使二维码粘在控制台底部（永远不会滚动消失）
* `--qr-file qr.txt:1:2` 将小二维码写入`qr.txt`
* `--qr-file qr.txt:2:2` 将大二维码写入`qr.txt`
* `--qr-file qr.svg:1:2` 将矢量图形二维码写入`qr.svg`
* `--qr-file qr.png:8:4:333333:ffcc55` 写入8x放大的黄色灰色背景`qr.png`
* `--qr-file qr.png:8:4::ffffff` 写入8x放大的白色透明背景`qr.png`

如果启用了[mdns](#mdns)，它使用服务器主机名，否则它将使用你的外部ip（默认路由），除非`--qri`指定特定的ip前缀或域名


## ftp服务器

可以使用`--ftp 3921`启动FTP服务器，和/或使用`--ftps`进行显式TLS（ftpes）

* 基于[pyftpdlib](https://github.com/giampaolo/pyftpdlib)
* 需要专用端口（不能与HTTP/HTTPS API共享）
* 上传不可恢复 -- 如有必要删除并重新开始
* 默认在主动模式下运行，你可能想要`--ftp-pr 12000-13000`
  * 如果你同时启用`ftp`和`ftps`，端口范围将被分成两半
  * 一些较旧的软件（debian-stable上的filezilla）无法在TLS下使用被动模式
* 使用任何用户名+你的密码登录，或将密码放在用户名字段中
  * 除非你启用了`--usernames`

一些推荐的FTP / FTPS客户端；`wark` = 示例密码：
* https://winscp.net/eng/download.php
* https://filezilla-project.org/ 在主动模式下与ftps有点困难，但其他方面都很好
* https://rclone.org/ 使用`tls=false explicit_tls=true`进行FTPS
* `lftp -u k,wark -p 3921 127.0.0.1 -e ls`
* `lftp -u k,wark -p 3990 127.0.0.1 -e 'set ssl:verify-certificate no; ls'`
* `curl ftp://127.0.0.1:3921/`（纯文本ftp）
* `curl --ssl-reqd ftp://127.0.0.1:3990/`（加密ftps）

配置文件示例，将FTP限制为只使用端口3921和12000-12099，所以所有这些端口都必须在防火墙中打开：

```yaml
[global]
  ftp: 3921
  ftp-pr: 12000-12099
```


## webdav服务器

支持读写，支持winXP及更高版本、macos、nautilus/gvfs ... 一个[直接从操作系统文件资源管理器访问copyparty](#mount-as-drive)的好方法

点击控制面板中的[连接](http://127.0.0.1:3923/?hc)按钮查看windows、linux、macos的连接说明

一般用法：
* 使用任何用户名+你的密码登录，或将密码放在用户名字段中（密码字段可以为空/任何内容）
  * 除非你启用了`--usernames`

在macos上，从finder连接：
* [Go] -> [Connect to Server...] -> http://192.168.123.1:3923/

为了向webdav客户端授予完全写访问权限，必须设置卷标志`daw`，账户也必须有删除访问权限（否则客户端将不被允许替换现有文件的内容，这是webdav的工作方式）

> 注意：如果你启用了[IdP认证](#identity-providers)，那可能会对某些/大多数webdav客户端造成问题；参见[IdP文档中的webdav部分](https://github.com/9001/copyparty/blob/hovudstraum/docs/idp.md#connecting-webdav-clients)


### 从Windows连接到webdav

使用GUI（winXP或更高版本）：
* 右键点击[我的电脑] -> [映射网络驱动器] -> 文件夹：`http://192.168.123.1:3923/`
  * 仅在winXP上，点击`Sign up for online storage`超链接并在那里放入URL
  * 建议将密码作为用户名提供；密码字段可以是任何内容或空
    * 除非你启用了`--usernames`

Windows内置的webdav客户端有以下错误列表；你可以通过使用rclone连接来避免所有这些：
* win7+在重启后重新认证时实际上不会将密码发送到服务器，除非你首先尝试使用错误密码登录，然后切换到正确密码
  * 或者只需将密码输入用户名字段来完全绕过它
* 连接到允许匿名读取的文件夹将使写入变得不可能，因为windows决定它不需要登录
  * 解决方法：连接两次；首先到需要认证的文件夹，然后到你实际想要的文件夹，并保持两者都挂载
  * 或设置服务器选项`--dav-auth`强制所有webdav客户端进行密码认证
* win7+可能为每个文件打开新的tcp连接，有时忘记关闭它们，最终需要重启
  * 可能与网卡相关（??），在e1000e上的win10-ltsc上发生，但在virtio上不发生
* windows无法访问包含无效unicode或禁止字符（`<>:"/\|?*`）的文件名或以`.`结尾的名称的文件夹
* winxp无法显示*某个范围*之外的unicode字符
  * latin-1没问题，平假名不行（即使在日语xp上作为shift-jis也不行）


## tftp服务器

可以使用`--tftp 3969`启动TFTP服务器（读/写）（你可能想要[ftp](#ftp-server)，除非你*实际上*在与90年代的硬件通信（在这种情况下我们绝对应该一起玩一段时间））

> 这使得这成为第一个使用copyparty更新的RTX DECT基站 🎉

* 基于[partftpy](https://github.com/9001/partftpy)
* 没有账户；从世界可读文件夹读取，写入世界可写，在世界可删除中覆盖
* 需要专用端口（不能与HTTP/HTTPS API共享）
  * 以root身份运行（或见下文）使用规范推荐的端口`69`（不错）
* 可以从预定义端口范围回复（对防火墙有好处）
* 只支持二进制/八位字节/图像传输模式（没有netascii）
* **不**支持[RFC 7440](https://datatracker.ietf.org/doc/html/rfc7440)，所以在WAN上会极其缓慢
  * 假设默认blksize（512），期望100BASE-T上1100 KiB/s，wifi上400-500 KiB/s，坏wifi上200

大多数客户端期望在端口69上找到TFTP，但在linux和macos上你需要是root才能监听那个端口。或者，监听3969并在服务器上使用NAT将69转发到那个端口；
* 在linux上：`iptables -t nat -A PREROUTING -i eth0 -p udp --dport 69 -j REDIRECT --to-port 3969`

一些推荐的TFTP客户端：
* curl（跨平台，读/写）
  * get：`curl --tftp-blksize 1428 tftp://127.0.0.1:3969/firmware.bin`
  * put：`curl --tftp-blksize 1428 -T firmware.bin tftp://127.0.0.1:3969/`
* windows：`tftp.exe`（你可能已经有了）
  * `tftp -i 127.0.0.1 put firmware.bin`
* linux：`tftp-hpa`，`atftp`
  * `atftp --option "blksize 1428" 127.0.0.1 3969 -p -l firmware.bin -r firmware.bin`
  * `tftp -v -m binary 127.0.0.1 3969 -c put firmware.bin`


## smb服务器

不安全、慢、不推荐用于广域网，使用`--smb`启用只读或`--smbw`启用读写

点击控制面板中的[连接](http://127.0.0.1:3923/?hc)按钮查看windows、linux、macos的连接说明

依赖项：`python3 -m pip install --user -U impacket==0.11.0`
* 更新版本的impacket希望能正常工作，但有猴子补丁，所以可能不行

一些特定于SMB/CIFS的**重大警告**，按重要性递减：
* 不完全确信只读就是只读
* smb后端没有完全与vfs集成，意味着可能有安全问题（路径遍历）。请使用`--smb-port`（见下文）和[prisonparty](./bin/prisonparty.sh)或[bubbleparty](./bin/bubbleparty.sh)
  * 账户密码按预期按卷工作，账户权限（读/写/移动/删除）也是如此，但必须给出`--smbw`以允许从smb进行写访问
  * [遮蔽](#shadowing)可能按预期工作，但不保证
* 与密码哈希或`--usernames`不兼容

一些小问题，
* 客户端在大文件夹中只能看到前约400个文件；
  * 这最初是由于[impacket#1433](https://github.com/SecureAuthCorp/impacket/issues/1433)，在impacket-0.12中修复，所以你可以用`--smb-nwa-1`禁用解决方法，但然后你会得到不可接受的糟糕性能
* 服务器配置的热重载（`/?reload=cfg`）不包括`[global]`部分（命令行参数）
* 只监听第一个IPv4 `-i`接口（默认 = :: = 0.0.0.0 = 全部）
* 登录在winxp上不工作，但匿名访问可以 -- 从copyparty配置中删除所有账户以使其工作
  * win10及以后不允许匿名连接/没有账户
* 仅python3
* 慢（windows内置的webdav支持快5倍，rclone-webdav快30倍）
  * 这些数字特定于copyparty的smb服务器（因为它很糟糕）；其他smb服务器应该与webdav类似

已知客户端错误：
* 仅在win7上，`--smb1`比smb2（默认）快得多，因为它在smb2上不断重新扫描文件夹
  * 但是smb1有问题，在win10及以后默认不启用
* windows无法访问包含无效unicode或禁止字符（`<>:"/\|?*`）的文件名或以`.`结尾的名称的文件夹

smb协议监听TCP端口445，这在linux和macos上是特权端口，需要以root身份运行copyparty。但是，这可以通过使用`--smb-port 3945`监听另一个端口，然后在服务器上使用NAT将流量从445转发到那里来避免；
* 在linux上：`iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 445 -j REDIRECT --to-port 3945`

使用以下之一进行认证：
* 用户名`$username`，密码`$password`
* 用户名`$password`，密码`k`


## 浏览器用户体验

调整UI

* 使用`--sort`全局设置默认排序顺序或使用`sort`卷标志按卷设置；指定一个或多个逗号分隔的列进行排序，并在列名前加`-`进行反向排序
  * 你可以使用的列名在目录列表中悬停在列标题上时作为工具提示可见，例如`href ext sz ts tags/.up_at tags/Circle tags/.tn tags/Artist tags/Title`
  * 要按音乐顺序（专辑、曲目、艺术家、标题）排序，以文件名作为后备，你可以`--sort tags/Circle,tags/.tn,tags/Artist,tags/Title,href`
  * 要按上传日期排序，首先使用`-e2d -mte +.up_at`启用在列表中显示上传日期，然后`--sort tags/.up_at`

参见[./docs/rice](./docs/rice)了解更多，包括如何向html `<head>`标签添加内容（css/`<meta>`/...），或添加你自己的翻译


## opengraph

discord和社交媒体嵌入

可以使用`--og`全局启用或使用卷标志`og`按卷启用

注意这会禁用热链接，因为opengraph规范要求这样做；要偷偷绕过这个故意限制，你可以按用户代理选择性启用opengraph，例如`--og-ua '(Discord|Twitter|Slack)bot'`（或卷标志`og_ua`）

你也可以通过在url后附加`?raw`来热链接文件

> 警告：如果你计划使用WebDAV，那么必须配置`--og-ua` / `og_ua`

如果你想完全用你自己的jinja2模板替换copyparty响应，将模板文件路径给`--og-tpl`或卷标志`og_tpl`（`HttpCli`的所有成员都可以通过`this`对象获得）


## 文件去重

使用`--dedup`全局启用基于符号链接的上传去重或使用卷标志`dedup`按卷启用

默认情况下，当有人尝试上传服务器上已经存在的文件时，上传将被礼貌地拒绝，服务器将把现有文件复制到上传本来要去的地方

如果你使用`--dedup`启用去重，那么它将创建符号链接而不是完整副本，从而减少磁盘空间使用

* 相反，如果你的服务器连接到s3-glacier或类似的读取昂贵的存储，并且你不能使用`--safe-dedup=1`因为你有其他软件篡改你的文件，所以你想完全禁用重复数据检测，那么你可以全局指定`--no-clone`或`noclone`作为卷标志

**警告：** 启用去重时，你也应该：
* 使用`-e2dsa`或卷标志`e2dsa`启用索引（参见下面的[文件索引](#file-indexing)部分）；强烈推荐
* ...和/或`--hardlink-only`使用基于硬链接的去重而不是符号链接；参见下面的解释
* ...和/或`--reflink`使用CoW/reflink基础去重（比硬链接安全得多，但依赖于操作系统/文件系统）

如果你只启用去重而不启用上述任何一个，重命名/删除文件将不安全；如果你启用索引，那么也做硬链接就不是*必要的*（但你可能仍然想要）

默认情况下，去重基于符号链接（符号链接）；这些是指向文件最近完整副本的指针的小文件

你可以选择使用硬链接而不是软链接，全局使用`--hardlink-only`或卷标志`hardlinkonly`，你可以选择使用`--reflink`或卷标志`reflink`使用reflinks

使用reflinks（CoW，写时复制）的优势：
* 完全安全（当你的文件系统正确支持时）；任一文件都可以被编辑或删除而不影响其他副本
* 只有linux 5.3或更新版本，只有python 3.14或更新版本，只有某些文件系统（btrfs可能可以，也许xfs也行，但zfs有错误）

使用硬链接的优势：
* 硬链接与其他软件更兼容；它们的行为完全像常规文件
* 你可以使用其他文件管理器安全地移动和重命名文件
  * 符号链接需要由copyparty管理以确保目标保持正确

使用符号链接的优势（默认）：
* 每个符号链接可以有自己的最后修改时间戳，但所有硬链接共享一个时间戳
* 符号链接使其他软件更明显地知道文件不是常规文件，所以这可能不那么危险
  * 硬链接看起来像常规文件，所以其他软件可能假设它们可以安全编辑而不影响其他副本

**警告：** 如果你编辑去重文件的内容，那么你也会编辑该文件的所有其他副本！这对硬链接特别令人惊讶，因为它们看起来像常规文件，但同一个文件存在于多个位置

全局选项`--xlink` / 卷标志`xlink`额外启用跨卷去重，但这可能有问题，不推荐

配置文件示例：

```yaml
[global]
  e2dsa  # 启动时扫描和索引文件系统
  dedup  # 所有卷的基于符号链接的去重

[/media]
  /mnt/nas/media
  flags:
    hardlinkonly  # 此卷使用硬链接而不是符号链接
```


## 文件索引

启用音乐搜索、上传撤销和更好的去重

文件索引依赖于两个数据库表，up2k文件树（`-e2d`）和元数据标签（`-e2t`），存储在`.hist/up2k.db`中。配置可以通过参数、卷标志或两者混合完成。

通过参数：
* `-e2d` 在上传时启用文件索引
* `-e2ds` 也在启动时扫描可写文件夹中的新文件
* `-e2dsa` 也扫描所有挂载的卷（包括只读的）
* `-e2t` 在上传时启用元数据索引
* `-e2ts` 也扫描所有还没有标签的文件中的标签
* `-e2tsr` 也删除所有现有标签，进行完全重新索引
* `-e2v` 在启动时验证文件完整性，比较数据库中的哈希
* `-e2vu` 用文件系统中的新哈希修补数据库
* `-e2vp` 恐慌并杀死copyparty

相同的参数可以设置为卷标志，除了`d2d`、`d2ds`、`d2t`、`d2ts`、`d2v`用于禁用：
* `-v ~/music::r:c,e2ds,e2tsr` 在启动时对所有内容进行完全重新索引
* `-v ~/music::r:c,d2d` 禁用**所有**索引，即使任何`-e2*`开启
* `-v ~/music::r:c,d2t` 禁用所有`-e2t*`（标签），不影响`-e2d*`
* `-v ~/music::r:c,d2ds` 禁用启动扫描；只索引新上传
* `-v ~/music::r:c,d2ts` 相同，除了只影响标签

注意：
* 上传时间可以通过启用`.up_at`元数据键在文件列表中显示，全局使用`-e2d -mte +.up_at`或按卷使用卷标志`e2d,mte=+.up_at`（对目录列表会有约17%的性能影响）
* `e2tsr`可能总是过度的，因为`e2ds`/`e2dsa`会捕获任何文件修改，`e2ts`然后会重新索引那些，除非有新的copyparty版本带有新解析器且发布说明另有说明

配置文件示例（顺便说一下，这些选项是推荐的）：

```yaml
[global]
  e2dsa  # 启动时扫描和索引所有卷中的所有文件
  e2ts   # 检查新发现或上传的文件的媒体标签
```

### 排除模式

为了节省一些时间，你可以提供一个正则表达式模式，用于文件路径只按文件名/路径/大小/最后修改时间索引（而不是文件内容的哈希），通过设置`--no-hash '\.iso$'`或卷标志`:c,nohash=\.iso$`，这有以下后果：
* 初始索引要快得多，特别是当卷在网络磁盘上时
* 使[文件搜索](#file-search)变得不可能
* 如果有人上传相同的文件内容，上传不会被检测为重复，所以不会被符号链接或拒绝

类似地，你可以使用`--no-idx [...]`和`:c,noidx=\.iso$`完全忽略文件/文件夹

注意：`no-idx`和/或`no-hash`阻止这些文件的去重

* 在macos上运行时，所有常见的苹果元数据文件默认被排除

如果你全局设置`--no-hash [...]`，你可以使用标志`:c,nohash=`为特定卷启用哈希

要从搜索结果中排除某些文件路径，使用`--srch-excl`或卷标志`srch_excl`而不是`--no-idx`，例如`--srch-excl 'password|logs/[0-9]'`

配置文件示例：

```yaml
[/games]
  /mnt/nas/games
  flags:
    noidx: \.iso$  # 跳过索引iso文件
    srch_excl: password|logs/[0-9]  # 过滤搜索结果
```

### 文件系统守卫

使用`--xdev` / 卷标志`:c,xdev`避免遍历到其他文件系统，例如跳过任何指向另一个硬盘的符号链接或绑定挂载

和/或你可以`--xvol` / `:c,xvol`忽略所有离开卷顶级目录的符号链接，但仍然允许指向其他地方的绑定挂载

* 如果符号链接指向用户具有相同访问级别的另一个卷，则`xvol`允许符号链接

这些选项会降低性能；不太可能的最坏情况估计是目录列表减少14%，下载为tar减少35%

从copyparty v1.7.0开始，这些选项也阻止运行时的文件访问 -- 在以前的版本中，它只是索引器的提示

### 定期重新扫描

文件系统监控；如果copyparty不是在你的文件系统上做事情的唯一软件，你可能想启用定期重新扫描以保持索引最新

参数`--re-maxage 60`将每60秒重新扫描所有卷，与卷标志`:c,scan=60`相同，按卷指定

重新扫描期间上传被禁用，所以当有写活动（上传、重命名、...）时，重新扫描将被`--db-act`（默认10秒）延迟

注意：文件夹缩略图在文件系统索引期间选择，所以定期重新扫描可以用来在图像上传/删除时保持它们准确（或使用控制面板中的`reload`按钮手动重新扫描）

配置文件示例：

```yaml
[global]
  re-maxage: 3600

[/pics]
  /mnt/nas/pics
  flags:
    scan: 900
```


## 上传规则

使用卷标志设置上传规则，一些示例：

* `:c,sz=1k-3m` 设置允许的文件大小在1 KiB和3 MiB之间（后缀：`b`、`k`、`m`、`g`）
* `:c,df=4g` 如果之后剩余磁盘空间少于4 GiB则阻止上传
* `:c,vmaxb=1g` 如果之后总卷大小超过1 GiB则阻止上传
* `:c,vmaxn=4k` 如果之后卷包含超过4096个文件则阻止上传
* `:c,nosub` 不允许上传到子目录；与`rotn`和`rotf`配合很好：
* `:c,rotn=1000,2` 将上传移动到子文件夹，每个文件夹最多1000个文件后创建新文件夹，两级深（必须至少1）
* `:c,rotf=%Y/%m/%d/%H` 强制文件按该日期格式上传到子文件夹结构中
  * 如果有人上传到`/foo/bar`，路径会被重写为例如`/foo/bar/2021/08/06/23`
  * 但实际值不被验证，只是结构，所以上传者可以选择任何符合格式字符串的值
    * 只是为了避免up2k中的额外复杂性，它已经够乱了
* `:c,lifetime=300` 当上传的文件变成5分钟时删除它们

你也可以设置按IP和按卷应用的事务限制，但这些假设`-j 1`（默认），否则限制会偏离，例如`-j 4`会允许你设置的限制的1x到4x之间的任何地方，取决于客户端被路由到哪个处理节点

* `:c,maxn=250,3600` 允许每个IP在1小时内250个文件（按卷跟踪）
* `:c,maxb=1g,300` 允许每个IP在5分钟内总共1 GiB（按卷跟踪）

注意：
* `vmaxb`和`vmaxn`需要`e2ds`卷标志或`-e2dsa`全局选项

配置文件示例：

```yaml
[/inc]
  /mnt/nas/uploads
  accs:
    w: *    # 任何人都可以在这里上传
    rw: ed  # 只有用户"ed"可以读写
  flags:
    e2ds       # 许多这些需要文件系统索引：
    sz: 1k-3m  # 只有在此范围内的文件大小才接受上传
    df: 4g     # 可用磁盘空间不能低于此值
    vmaxb: 1g  # 卷永远不能超过1 GiB
    vmaxn: 4k  # ...或4000个文件，以先到者为准
    nosub      # 必须上传到顶级文件夹
    lifetime: 300   # 上传在5分钟后被删除
    maxn: 250,3600  # 每个IP可以在1小时内上传250个文件
    maxb: 1g,300    # 每个IP可以在5分钟内上传1 GiB
```


## 压缩上传

文件可以在上传时自动压缩，要么根据用户请求（如果配置允许）要么由服务器配置强制

* 卷标志`gz`允许gz压缩
* 卷标志`xz`允许lzma压缩
* 卷标志`pk` **强制**压缩所有文件
* url参数`pk`请求使用服务器默认算法压缩
* url参数`gz`或`xz`请求使用特定算法压缩
* url参数`xz`请求xz压缩

需要注意的事情，
* `gz`和`xz`参数接受一个可选参数，压缩级别（范围0到9）
* `pk`卷标志接受可选参数`ALGORITHM,LEVEL`，然后将强制用于所有上传，例如`gz,9`或`xz,0`
* 默认压缩是gzip级别9
* 除了up2k之外的所有上传方法都支持
* 文件将在压缩后被索引，所以重复检测和文件搜索不会按预期工作

一些示例，
* `-v inc:inc:w:c,pk=xz,0`  
  名为inc的文件夹，在inc共享，每个人只写，强制xz压缩级别0
* `-v inc:inc:w:c,pk`  
  相同的只写inc，但强制gz压缩（默认）而不是xz
* `-v inc:inc:w:c,gz`  
  如果客户端上传到`/inc?pk`或`/inc?gz`或`/inc?gz=4`，允许（但不强制）gz压缩


## chmod和chown

按卷的文件系统权限和所有权

默认情况下：
* 所有文件夹都是chmod 755
* 文件通常是chmod 644（umask定义）
* 用户/组是copyparty运行的任何用户/组

这可以按卷配置：
* 卷标志`chmod_f`设置文件权限；默认=`644`（通常）
* 卷标志`chmod_d`设置目录权限；默认=`755`
* 卷标志`uid`设置所有者用户ID
* 卷标志`gid`设置所有者组ID

注意：
* `gid`只能设置为copyparty进程所属的组之一
* `uid`只能在copyparty以root身份运行时设置（我欣赏你的信任）


## 其他标志

* `:c,magic`启用无名上传的文件类型检测，与`--magic`相同
  * 需要https://pypi.org/project/python-magic/ `python3 -m pip install --user -U python-magic`
  * 在windows上改为获取这个`python3 -m pip install --user -U python-magic-bin`


## 数据库位置

在卷内（`.hist/up2k.db`，默认）或其他地方

copyparty在每个卷内创建一个名为`.hist`的子文件夹，在那里存储数据库、缩略图和其他一些东西

这可以使用`--hist`参数或`hist=`卷标志或两者混合保存在单个地方：
* `--hist ~/.cache/copyparty -v ~/music::r:c,hist=-`设置`~/.cache/copyparty`作为放置卷信息的默认地方，但`~/music`获得常规的`.hist`子文件夹（`-`恢复默认行为）

默认情况下，`-e2d`和`-e2t`的按卷`up2k.db` sqlite3数据库根据`--hist`选项存储在缩略图旁边，但全局选项`--dbpath`和/或卷标志`dbpath`可以用来将数据库放在其他地方

如果你的存储后端不可靠（NFS或坏硬盘），你可以指定一个或多个"地标"在做任何数据库相关的事情之前寻找。地标是总是期望存在于卷内的文件。这避免了在停机事件中的虚假文件系统重新扫描。每行一个地标（见下面的示例）

注意：
* 强烈建议将hist文件夹放在SSD上以获得性能
* markdown编辑总是存储在本地`.hist`子目录中
* 在windows上，卷标志路径是cyglike，所以`/c/temp`意味着`C:\temp`，但对`--hist`使用常规路径
  * 你也可以对卷使用cygpaths，`-v C:\Users::r`和`-v /c/users::r`都工作

配置文件示例：

```yaml
[global]
  hist: ~/.cache/copyparty  # 默认将db/thumbs/等放在这里

[/pics]
  /mnt/nas/pics
  flags:
    hist: -  # 恢复默认（/mnt/nas/pics/.hist/）
    hist: /mnt/nas/cache/pics/  # 可以是绝对路径
    landmark: me.jpg  # /mnt/nas/pics/me.jpg必须可读以启用db
    landmark: info/a.txt^=ok  # 这个文本文件必须以"ok"开头
```


## 音频文件元数据

设置`-e2t`在上传时索引标签

`-mte`决定哪些标签要索引并在浏览器中显示（以及显示顺序），这可以按卷更改：
* `-v ~/music::r:c,mte=title,artist`索引并显示*title*后跟*artist*

如果你从`mte`添加/删除标签，你需要运行一次`-e2tsr`来重建数据库，否则只有新文件会受到影响

但是，与其使用`-mte`，`-mth`是在浏览器中隐藏标签的更好方法：这些标签默认不会显示，但它们仍然被索引并变得可搜索，用户可以选择在`[⚙️] config`面板中取消隐藏它们

`-mtm`可以用来添加或重新定义元数据映射，假设你有带有`foo`和`bar`标签的媒体文件，你想让它们在浏览器中显示为`qux`（如果两者都存在则优先`foo`），那么做`-mtm qux=foo,bar`，现在你可以`-mte artist,title,qux`

以`.`开头的标签如`.bpm`和`.dur`（ation）表示数值

参见[mtag.py](https://github.com/9001/copyparty/blob/hovudstraum/copyparty/mtag.py)中美丽混乱的字典以获得默认映射（应该涵盖mp3、opus、flac、m4a、wav、aif）

`--no-mutagen`禁用Mutagen并改用FFprobe，它...
* 比Mutagen慢约20倍
* 捕获一些Mutagen不捕获的标签
  * 旋律键、视频分辨率、帧率、pixfmt
* 避免将任何GPL代码拉入copyparty
* 更重要的是在传入文件上运行FFprobe，如果你的FFmpeg有cve这很糟糕

`--mtag-to`设置标签扫描超时；非常高的默认值（60秒）以迎合zfs和其他随机冻结的文件系统。像10这样的较低值通常是安全的，允许更快地处理棘手的文件


## 文件解析器插件

提供自定义解析器来索引额外的标签，也参见[./bin/mtag/README.md](./bin/mtag/README.md)

copyparty可以调用外部程序使用`mtp`（作为参数或卷标志）收集文件的额外元数据，有60秒的默认超时，默认只分析包含音频的文件（见下面的ay/an/ad）

* `-mtp .bpm=~/bin/audio-bpm.py`将执行`~/bin/audio-bpm.py`，音频文件作为参数1来提供`.bpm`标签，如果音频元数据中不存在
* `-mtp key=f,t5,~/bin/audio-key.py`使用`~/bin/audio-key.py`获取`key`标签，替换任何现有的元数据标签（`f,`），如果超过5秒则中止（`t5,`）
* `-v ~/music::r:c,mtp=.bpm=~/bin/audio-bpm.py:c,mtp=key=f,t5,~/bin/audio-key.py`两者作为按卷配置，哇这变得丑陋了

*但等等，还有更多！* `-mtp`也可以用于非音频文件，使用`a`标志：`ay`只做音频文件（默认），`an`只做非音频文件，或`ad`做所有文件（d表示不关心）
* "音频文件"顺便说一下也意味着视频，只要有音频流
* `-mtp ext=an,~/bin/file-ext.py`运行`~/bin/file-ext.py`来获取`ext`标签，只有当文件不是音频时（`an`）
* `-mtp arch,built,ver,orig=an,eexe,edll,~/bin/exe.py`运行`~/bin/exe.py`来获取windows二进制文件的属性，只有当文件不是音频（`an`）且文件扩展名是exe或dll时
* 如果你想链式解析器，使用`p`标志设置处理顺序
  * `-mtp foo=p1,~/a.py`在`-mtp foo=p2,~/b.py`之前运行，并将到目前为止检测到的所有标签作为json转发到b.py的stdin
* 选项`c0`禁用stdout/stderr的捕获，所以copyparty根本不会从进程接收任何标签 -- 相反，被调用的程序可以自由地向控制台打印任何内容，只是使用copyparty作为启动器
  * `c1`只捕获stdout，`c2`只捕获stderr，`c3`（默认）两者都捕获
* 如果超时，你可以控制解析器如何被杀死，选项`kt`杀死整个进程树（默认），`km`只杀死主进程，或`kn`让它继续运行直到copyparty终止

如果某些东西不工作，尝试`--mtag-v`获取详细的错误消息

配置文件示例；注意`mtp`是累加选项，所以所有mtp选项都会生效：

```yaml
[/music]
  /mnt/nas/music
  flags:
    mtp: .bpm=~/bin/audio-bpm.py  # 用脚本分配".bpm"（数值）
    mtp: key=f,t5,~/bin/audio-key.py  # 强制/覆盖，5秒超时
    mtp: ext=an,~/bin/file-ext.py  # 只在非音频文件上运行
    mtp: arch,built,ver,orig=an,eexe,edll,~/bin/exe.py  # 只有exe/dll
```


## 事件钩子

在上传、重命名等时触发程序（[示例](./bin/hooks/)）

你可以在事件发生之前和/或之后设置钩子，目前你可以钩子上传、移动/重命名和删除

有一堆标志和东西，参见`--help-hooks`

如果你想编写自己的钩子，参见[开发说明](./docs/devnotes.md#event-hooks)


### zeromq

事件钩子可以发送zeromq消息而不是运行程序

每次上传文件时发送0mq消息，

* `--xau zmq:pub:tcp://*:5556`向任何/所有连接的SUB客户端发送PUB
* `--xau t3,zmq:push:tcp://*:5557`向恰好一个连接的PULL客户端发送PUSH
* `--xau t3,j,zmq:req:tcp://localhost:5555`向连接的REP客户端发送REQ

PUSH和REQ示例有`t3`（3秒后超时），因为如果没有客户端可以交谈，它们会阻塞

* REQ示例做`t3,j`发送扩展的上传信息作为json而不是只是文件系统路径

如果你需要接收消息的东西，参见[zmq-recv.py](https://github.com/9001/copyparty/blob/hovudstraum/bin/zmq-recv.py)

配置文件示例；注意钩子是累加选项，所以所有xau选项都会生效：

```yaml
[global]
  xau: zmq:pub:tcp://*:5556`  # 向任何/所有连接的SUB客户端发送PUB
  xau: t3,zmq:push:tcp://*:5557`  # 向恰好一个连接的PULL客户端发送PUSH
  xau: t3,j,zmq:req:tcp://localhost:5555`  # 向连接的REP客户端发送REQ
```


### 上传事件

更旧、更强大的方法（[示例](./bin/mtag/)）：

```
-v /mnt/inc:inc:w:c,e2d,e2t,mte=+x1:c,mtp=x1=ad,kn,/usr/bin/notify-send
```

那是命令行示例；这里是配置文件示例：

```yaml
[/inc]
  /mnt/inc
  accs:
    w: *
  flags:
    e2d, e2t  # 启用上传文件及其标签的索引
    mte: +x1
    mtp: x1=ad,kn,/usr/bin/notify-send
```

所以文件系统位置`/mnt/inc`在`/inc`共享，每个人只写，将`x1`附加到要索引的标签列表（`mte`），并使用`/usr/bin/notify-send`为任何文件类型（`ad`）"提供"标签`x1`，禁用超时杀死（`kn`）

那会运行命令`notify-send`，上传文件的路径作为第一个也是唯一的参数（所以在linux上它会在屏幕上显示通知）

注意这比新的[事件钩子](#event-hooks)复杂得多，但这种方法有以下优势：
* 非阻塞和多线程；不会阻碍其他上传
* 你可以访问来自FFmpeg和其他mtp解析器的标签
* 只在新的唯一文件上触发，不是重复

注意它会占用解析线程，所以fork任何昂贵的东西（或设置`kn`让copyparty为你fork） -- 另一方面，如果你想故意排队/单线程，你可以将它与`--mtag-mt 1`结合

作为参考，如果你要使用事件钩子来做这个，它会是这样的：`-e2d --xau notify-send,hello,--`


## 处理器

用插件重新定义行为（[示例](./bin/handlers/)）

用完全不同的东西替换404和403错误（目前就这些）

至于客户端的东西，有[修改UI/UX的插件](./contrib/plugins/)


## IP认证

基于IP范围（CIDR）的自动登录，使用全局选项`--ipu`

例如，如果IP以`192.168.123`开头的每个人都应该自动登录为用户`spartacus`，那么你可以指定`--ipu=192.168.123.0/24=spartacus`作为命令行选项，或将此放入配置文件：

```yaml
[global]
  ipu: 192.168.123.0/24=spartacus
```

重复选项以映射额外的子网

**小心这个！** 如果你有反向代理，那么你绝对想确保你正确配置了[real-ip](#real-ip)，并且最好将反向代理的IP空映射以防万一；所以如果你的反向代理从`172.24.27.9`发送请求，那会是`--ipu=172.24.27.9/32=`


### 限制到IP

将用户限制到某些IP范围（CIDR），使用全局选项`--ipr`

例如，如果用户`spartacus`如果不是从以`192.168.123`或`172.16`开头的IP连接就应该被拒绝，那么你可以指定`--ipr=192.168.123.0/24,172.16.0.0/16=spartacus`作为命令行选项，或将此放入配置文件：

```yaml
[global]
  ipr: 192.168.123.0/24,172.16.0.0/16=spartacus
```

重复选项以映射额外的用户


## 身份提供者

用oauth等替换copyparty密码

你可以禁用内置的基于密码的登录系统，而是用单独的软件（身份提供者）替换它，然后处理用户的认证/授权；这使得可以用passkeys / fido2 / webauthn / yubikey / ldap / active directory / oauth / 许多其他单点登录装置登录

* 常规配置定义的用户将用作不包含有效（受信任）IdP用户名头的请求的后备

* 如果你的IdP服务器很慢，考虑`--idp-cookie`并让带有cookie `cppws`的请求绕过IdP；为聚会添加的实验性基于会话的功能

一些流行的身份提供者是[Authelia](https://www.authelia.com/)（基于配置文件）和[authentik](https://goauthentik.io/)（基于GUI，更复杂）

有一个[docker-compose示例](./docs/examples/docker/idp-authelia-traefik)，希望是一个好的起点（或者如果你是DIY类型，参见[./docs/idp.md](./docs/idp.md)）

copyparty配置选项的更完整示例[看起来像这样](./docs/examples/docker/idp/copyparty.conf)

但如果你只想让用户更改自己的密码，那么你可能想要[用户可更改密码](#user-changeable-passwords)


### 通用头部认证

其他通过头部认证的方式

如果你有一个添加带有用户标识符的头的中间件，例如tailscale的`Tailscale-User-Login: alice.m@forest.net`，那么你可以通过定义该映射`--idp-hm-usr '^Tailscale-User-Login^alice.m@forest.net^alice'`或以下配置文件自动认证为`alice`：

```yaml
[global]
  idp-hm-usr: ^Tailscale-User-Login^alice.m@forest.net^alice
```

重复整个`idp-hm-usr`选项以添加更多映射


## 用户可更改密码

如果允许，用户可以在控制面板中更改自己的密码

* 与[身份提供者](#identity-providers)不兼容

* 必须用`--chpw`启用，因为账户共享是一个流行的用例

  * 如果你想启用该功能但拒绝特定账户列表的密码更改，你可以用`--chpw-no name1,name2,name3,...`做到

* 要执行密码重置，编辑服务器配置并在那里给用户另一个密码，然后做[配置重载](#server-config)或服务器重启

* 自定义密码保存在文件系统路径`--chpw-db`的文本文件中，默认是copyparty配置文件夹中的`chpw.json`

  * 如果你运行多个有不同用户的copyparty实例，你*几乎肯定*想为每个实例指定单独的数据库

  * 如果启用了[密码哈希](#password-hashing)，数据库中的密码也被哈希

    * ...这意味着如果你更改密码哈希设置，所有用户定义的密码都会被遗忘


## 使用云作为存储

连接到aws s3存储桶等

没有内置支持，但你可以使用FUSE软件如[rclone](https://rclone.org/) / [geesefs](https://github.com/yandex-cloud/geesefs) / [JuiceFS](https://juicefs.com/en/)首先将你的云存储挂载为本地磁盘，然后让copyparty使用该磁盘（中的文件夹）作为卷

如果copyparty无法访问rclone/geesefs/JuiceFS提供的本地文件夹（例如如果它看起来不可见），那么你可能需要使用`--allow-other`运行rclone和/或在`/etc/fuse.conf`中启用`user_allow_other`

你可能会用默认配置获得不错的速度，但很可能限制为每个文件使用一个TCP连接，所以上传客户端无法并行发送多个块

> 在[v1.13.5](https://github.com/9001/copyparty/releases/tag/v1.13.5)之前，建议使用卷标志`sparse`强制允许多个块并行；这会将上传速度从`1.5 MiB/s`提高到超过`80 MiB/s`，但有引发S3或JuiceFS中潜在错误的风险。但v1.13.5添加了块拼接，所以这现在可能不那么重要了。相反，`nosparse` *可能*现在在某些情况下提高性能。请尝试所有三个选项（默认、`sparse`、`nosparse`），因为最佳选择取决于你的网络条件和软件堆栈（FUSE驱动程序和云服务器）

有人还测试了geesefs与[gocryptfs](https://nuetzlich.net/gocryptfs/)的组合，结果令人惊讶地好，在千兆线路上获得60 MiB/s的上传速度，但JuiceFS使用其内置加密以80 MiB/s获胜

你可以通过为`--iobuf` / `--s-rd-sz` / `--s-wr-sz`指定更大的值来提高性能

> 如果你已经试验过这个并做出了有趣的观察，请分享你的发现，这样我们可以添加一个带有具体建议的部分 :-)


## 对Google隐藏

告诉搜索引擎你不想被索引，要么使用老式的[robots.txt](https://www.robotstxt.org/robotstxt.html)要么通过copyparty设置：

* `--no-robots`全局添加HTTP（`X-Robots-Tag`）和HTML（`<meta>`）头部，带有`noindex, nofollow`
* 卷标志`[...]:c,norobots`对单个卷做同样的事情
* 卷标志`[...]:c,robots`允许该卷的搜索引擎爬取，即使全局设置了`--no-robots`

另外，`--force-js`禁用纯HTML文件夹列表，使*某些*搜索引擎更难解析 -- 注意理解javascript的爬虫（如google）不会受到影响


## 主题

你可以用`--theme 2`更改默认主题，并通过修改`browser.css`或向`--css-browser`提供你自己的css来添加你自己的主题，然后通过增加`--themes`告诉copyparty它们存在

<table><tr><td width="33%" align="center"><a href="https://user-images.githubusercontent.com/241032/165864907-17e2ac7d-319d-4f25-8718-2f376f614b51.png"><img src="https://user-images.githubusercontent.com/241032/165867551-fceb35dd-38f0-42bb-bef3-25ba651ca69b.png"></a>
0. 经典深色</td><td width="33%" align="center"><a href="https://user-images.githubusercontent.com/241032/168644399-68938de5-da9b-445f-8d92-b51c74b5f345.png"><img src="https://user-images.githubusercontent.com/241032/168644404-8e1a2fdc-6e59-4c41-905e-ba5399ed686f.png"></a>
2. 扁平pm-monokai</td><td width="33%" align="center"><a href="https://user-images.githubusercontent.com/241032/165864901-db13a429-a5da-496d-8bc6-ce838547f69d.png"><img src="https://user-images.githubusercontent.com/241032/165867560-aa834aef-58dc-4abe-baef-7e562b647945.png"></a>
4. vice</td></tr><tr><td align="center"><a href="https://user-images.githubusercontent.com/241032/165864905-692682eb-6fb4-4d40-b6fe-27d2c7d3e2a7.png"><img src="https://user-images.githubusercontent.com/241032/165867555-080b73b6-6d85-41bb-a7c6-ad277c608365.png"></a>
1. 经典浅色</td><td align="center"><a href="https://user-images.githubusercontent.com/241032/168645276-fb02fd19-190a-407a-b8d3-d58fee277e02.png"><img src="https://user-images.githubusercontent.com/241032/168645280-f0662b3c-9764-4875-a2e2-d91cc8199b23.png"></a>
3. 扁平浅色
</td><td align="center"><a href="https://user-images.githubusercontent.com/241032/165864898-10ce7052-a117-4fcf-845b-b56c91687908.png"><img src="https://user-images.githubusercontent.com/241032/165867562-f3003d45-dd2a-4564-8aae-fed44c1ae064.png"></a>
5. <a href="https://blog.codinghorror.com/a-tribute-to-the-windows-31-hot-dog-stand-color-scheme/">热狗摊</a></td></tr></table>

HTML标签的类名根据选定的主题设置，用于设置颜色作为css变量++

* 每个主题*通常*有一个深色主题（偶数）和一个浅色主题（奇数），成对显示
* 第一个主题（主题0和1）是`html.a`，第二个主题（2和3）是`html.b`
* 如果选择了浅色主题，设置`html.y`，否则设置`html.z`
* 所以如果选择了第二个主题的深色版本，你使用`html.b`、`html.z`、`html.bz`中的任何一个来指定规则

参见[./copyparty/web/browser.css](./copyparty/web/browser.css)的顶部，那里设置了颜色变量，底部附近有布局特定的东西

如果你想更改字体，参见[./docs/rice/](./docs/rice/)


## 完整示例

* 参见[在windows上运行](./docs/examples/windows.md)获取花哨的windows设置

  * 或使用下面的任何示例，如果你使用exe版本，只需将`python copyparty-sfx.py`替换为`copyparty.exe`

* 允许任何人下载或上传文件到当前文件夹：  
  `python copyparty-sfx.py`

  * 使用`-e2dsa -e2ts`启用搜索和音乐索引

  * 使用`--ftp 3921`在端口3921上启动FTP服务器

  * 使用`-z`在局域网上宣布它，这样它出现在windows/Linux文件管理器中

* 任何人都可以上传，但没有人可以看到任何文件（甚至上传者）：  
  `python copyparty-sfx.py -e2dsa -v .::w`

  * 使用`--df 4`在剩余磁盘空间少于4 GiB时阻止上传

  * 使用`--xau bin/hooks/notify.py`在新上传时显示弹出窗口

* 任何人都可以上传，并为他们做的每次上传接收"秘密"链接：  
  `python copyparty-sfx.py -e2dsa -v .::wG:c,fk=8`

* 任何人都可以浏览（`r`），只有`kevin`（密码`okgo`）可以上传/移动/删除（`A`）文件：  
  `python copyparty-sfx.py -e2dsa -a kevin:okgo -v .::r:A,kevin`

* 只读音乐服务器：  
  `python copyparty-sfx.py -v /mnt/nas/music:/music:r -e2dsa -e2ts --no-robots --force-js --theme 2`
  
  * ...带bpm和key扫描  
    `-mtp .bpm=f,audio-bpm.py -mtp key=f,audio-key.py`
  
  * ...带`kevin`的读写文件夹，密码是`okgo`  
    `-a kevin:okgo -v /mnt/nas/inc:/inc:rw,kevin`
  
  * ...带磁盘日志  
    `-lo log/cpp-%Y-%m%d-%H%M%S.txt.xz`


## 监听端口80和443

成为*真正的*网络服务器，人们可以通过只访问你的IP或域名而不指定端口来访问

**如果你在windows上，** 那么你只需要添加命令行参数`-p 80,443`就完成了！很好

**如果你在macos上，** 抱歉，我不知道

**如果你在Linux上，** 你有以下4个选项：

* **选项1：** 设置[反向代理](#reverse-proxy) -- 如果你在合适的无头服务器上运行，这个很有意义，因为这样你也能获得真正的HTTPS

* **选项2：** NAT到端口3923 -- 这很麻烦，因为你需要每次重启时都这样做，确切的命令可能取决于你的linux发行版：
  ```bash
    iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-port 3923
    iptables -t nat -A PREROUTING -p tcp --dport 443 -j REDIRECT --to-port 3923
    ```

* **选项3：** 禁用阻止使用80和443的[安全策略](https://www.w3.org/Daemon/User/Installation/PrivilegedPorts.html)；这*可能*没问题：
  ```
  setcap CAP_NET_BIND_SERVICE=+eip $(realpath $(which python))
  python copyparty-sfx.py -p 80,443
  ```

* **选项4：** 以root身份运行copyparty（请不要）


## 反向代理

在现有网络服务器（如nginx、caddy或apache）上与其他网站一起运行copyparty

你可以：
* 给copyparty自己的域名或子域名（推荐）
* 或进行基于位置的代理，使用`--rp-loc=/stuff`告诉copyparty它挂载在哪里 -- 有轻微的性能成本和更高的错误几率
  * 如果copyparty说`incorrect --rp-loc or webserver config; expected vpath starting with [...]`，这可能是因为网络服务器从请求URL中剥离了代理位置 -- 参见下面apache示例中的`ProxyPass`

当在反向代理后面运行时（这包括像cloudflare这样的服务），正确配置real-ip很重要，因为许多功能依赖于知道客户端的IP。最好/最安全的方法是配置你的反向代理，使其给copyparty一个只包含客户端真实IP地址的头部，然后设置`--xff-hdr theHeaderName --rproxy 1`，但或者，如果你想/需要让copyparty处理这个，注意红色和黄色的日志消息，它们解释如何做到这一点。基本上，日志会说：

> 设置`--xff-hdr`为要从中读取IP的http头部名称（通常是`x-forwarded-for`，但cloudflare使用`cf-connecting-ip`），然后`--xff-src`为反向代理的IP，这样copyparty会信任xff-hdr。如果头部只包含一个IP（正确的），你还需要配置`--rproxy`为`1`，或者如果它包含多个IP，则为*负值*；`-1`是最右边和最受信任的IP（最近的代理，所以通常不是正确的），`-2`是第二近的跳，等等

注意，特别是`--rp-loc`除非你正确配置上述内容，否则根本不会工作

一些反向代理（如[Caddy](https://caddyserver.com/)）可以自动为你获取有效的https/tls证书，一些支持HTTP/2和QUIC，这*可能*是一个不错的速度提升，取决于很多因素
* **警告：** nginx-QUIC（HTTP/3）仍然是实验性的，可能使上传变得更慢，所以现在推荐HTTP/1.1
* 根据服务器/客户端，HTTP/1.1也可能比HTTP/2快5倍

为了提高安全性（和10%的性能提升），考虑使用`-i unix:770:www:/dev/shm/party.sock`监听unix套接字（权限`770`意味着只有组`www`的成员可以访问它）

示例网络服务器/反向代理配置：

* [apache配置](contrib/apache/copyparty.conf)
* caddy uds：`caddy reverse-proxy --from :8080 --to unix///dev/shm/party.sock`
* caddy tcp：`caddy reverse-proxy --from :8081 --to http://127.0.0.1:3923`
* [haproxy配置](contrib/haproxy/copyparty.conf)
* [lighttpd子域名](contrib/lighttpd/subdomain.conf) -- 整个域名/子域名
* [lighttpd子路径](contrib/lighttpd/subpath.conf) -- 基于位置（不是最优的，但如果你需要的话）
* [nginx配置](contrib/nginx/copyparty.conf) -- 推荐
* [traefik配置](contrib/traefik/copyparty.yaml)


### 真实IP

教copyparty如何查看客户端IP，当在反向代理、WAF或其他保护服务（如cloudflare）后面运行时

如果你（也许其他人）一直收到说`thank you for playing`的消息，那么你因恶意流量被禁止了。这个禁令适用于copyparty*认为*识别可疑客户端的IP地址 -- 所以，根据你的设置，你可能需要告诉copyparty在哪里找到正确的IP

对于大多数常见设置，服务器日志中应该有一个有用的消息解释要做什么，但如果你想了解更多，参见[docs/xff.md](docs/xff.md)，包括一个快速hack来**让它工作**（这**不**推荐，但嘿...）


### 反向代理性能

大多数反向代理支持使用uds/unix套接字（`/dev/shm/party.sock`，更快/推荐）或使用tcp（`127.0.0.1`）连接到copyparty

copyparty监听uds / unix套接字 / unix域套接字，反向代理连接到那个：

| index.html   | 上传        | 下载        | 软件     |
| ------------ | ----------- | ----------- | -------- |
| 28'900 req/s | 6'900 MiB/s | 7'400 MiB/s | 无代理   |
| 18'750 req/s | 3'500 MiB/s | 2'370 MiB/s | haproxy |
|  9'900 req/s | 3'750 MiB/s | 2'200 MiB/s | caddy |
| 18'700 req/s | 2'200 MiB/s | 1'570 MiB/s | nginx |
|  9'700 req/s | 1'750 MiB/s | 1'830 MiB/s | apache |
|  9'900 req/s | 1'300 MiB/s | 1'470 MiB/s | lighttpd |

当反向代理连接到`127.0.0.1`时（基本和/或老式方式），速度稍差：

| index.html   | 上传        | 下载        | 软件     |
| ------------ | ----------- | ----------- | -------- |
| 21'200 req/s | 5'700 MiB/s | 6'700 MiB/s | 无代理   |
| 14'500 req/s | 1'700 MiB/s | 2'170 MiB/s | haproxy |
| 11'100 req/s | 2'750 MiB/s | 2'000 MiB/s | traefik |
|  8'400 req/s | 2'300 MiB/s | 1'950 MiB/s | caddy |
| 13'400 req/s | 1'100 MiB/s | 1'480 MiB/s | nginx |
|  8'400 req/s | 1'000 MiB/s | 1'000 MiB/s | apache |
|  6'500 req/s | 1'270 MiB/s | 1'500 MiB/s | lighttpd |

总结，`haproxy > caddy > traefik > nginx > apache > lighttpd`，尽可能使用uds（traefik还不支持）

* 如果这些结果是胡说八道，因为我的配置示例很糟糕，请提交更正！


## 永久cloudflare隧道

如果你有域名并想快速让copyparty上线，要么从CGNAT后面的家用PC，要么从没有现有[反向代理](#reverse-proxy)设置的服务器，一种方法是创建[Cloudflare隧道](https://developers.cloudflare.com/cloudflare-one/connections/connect-networks/get-started/)（以前称为"Argo隧道"）

我建议制作`本地管理的隧道`以获得更多控制，但如果你更喜欢制作`远程管理的隧道`，那么目前是这样的：

* `cloudflare仪表板` » `零信任` » `网络` » `隧道` » `创建隧道` » `cloudflared` » 选择一个酷的`子域名`并将`路径`留空，使用`服务类型` = `http`和`URL` = `127.0.0.1:3923`

* 如果你想只运行隧道而不安装它，跳过`cloudflared service install BASE64`步骤，改为做`cloudflared --no-autoupdate tunnel run --token BASE64`

注意：由于人们将通过cloudflare连接，如[真实IP](#real-ip)中提到的，你应该使用`--xff-hdr cf-connecting-ip`运行copyparty以正确检测客户端IP

配置文件示例：

```yaml
[global]
  xff-hdr: cf-connecting-ip
```


## prometheus

可以在URL `/.cpr/metrics`为grafana / prometheus / 等启用指标/统计（openmetrics 1.0.0）

必须用`--stats`启用，因为它稍微减少启动时间，你可能也想要`-e2dsa`

端点只能由`admin`账户访问，意味着以下示例命令行中`rwmda`中的`a`：`python3 -m copyparty -a ed:wark -v /mnt/nas::rwmda,ed --stats -e2dsa`

按照设置`node_exporter`的指南，除了让它从copyparty读取；下面是示例`/etc/prometheus/prometheus.yml`

```yaml
scrape_configs:
  - job_name: copyparty
    metrics_path: /.cpr/metrics
    basic_auth:
      password: wark
    static_configs:
      - targets: ['192.168.123.1:3923']
```

目前以下指标可用，
* `cpp_uptime_seconds` 自上次copyparty重启以来的时间
* `cpp_boot_unixtime_seconds` 相同但作为绝对时间戳
* `cpp_active_dl` 活动下载数
* `cpp_http_conns` 打开的http(s)连接数
* `cpp_http_reqs` 处理的http(s)请求数
* `cpp_sus_reqs` 403/422/恶意请求数
* `cpp_active_bans` 当前被禁IP数
* `cpp_total_bans` 自上次重启以来被禁IP数

除非指定`--nos-vst`，否则这些可用：
* `cpp_db_idle_seconds` 自上次数据库活动（上传/重命名/删除）以来的时间
* `cpp_db_act_seconds` 相同但作为绝对时间戳
* `cpp_idle_vols` 空闲/就绪的卷数
* `cpp_busy_vols` 忙碌/索引的卷数
* `cpp_offline_vols` 离线/不可用的卷数
* `cpp_hashing_files` 排队等待哈希/索引的文件数
* `cpp_tagq_files` 排队等待元数据扫描的文件数
* `cpp_mtpq_files` 排队等待基于插件分析的文件数

这些只按卷可用：
* `cpp_disk_size_bytes` 总硬盘大小
* `cpp_disk_free_bytes` 可用硬盘空间

这些按卷和`total`可用：
* `cpp_vol_bytes` 卷中所有文件的大小
* `cpp_vol_files` 文件数
* `cpp_dupe_bytes` 去重可能节省的磁盘空间
* `cpp_dupe_files` 重复文件数
* `cpp_unf_bytes` 当前未完成/传入的上传

一些指标有额外的要求才能正确工作，
* `cpp_vol_*`需要`e2ds`卷标志或`-e2dsa`全局选项

以下选项可用于禁用一些指标：
* `--nos-hdd`禁用`cpp_disk_*`，可以防止启动硬盘
* `--nos-vol`禁用`cpp_vol_*`，减少服务器启动时间
* `--nos-vst`禁用卷状态，将最坏情况prometheus查询时间减少0.5秒
* `--nos-dup`禁用`cpp_dupe_*`，减少prometheus查询造成的服务器负载
* `--nos-unf`禁用`cpp_unf_*`，没有特定目的

注意：如果使用`-j`启用多进程，以下指标计算不正确：`cpp_http_conns`、`cpp_http_reqs`、`cpp_sus_reqs`、`cpp_active_bans`、`cpp_total_bans`


## 其他极其特定的功能

你永远不会找到这些的用途：


### 自定义MIME类型

更改文件扩展名的关联

使用命令行参数，你可以做类似`--mime gif=image/jif`和`--mime ts=text/x.typescript`的事情（可以多次指定）

在配置文件中，这与以下相同：

```yaml
[global]
  mime: gif=image/jif
  mime: ts=text/x.typescript
```

使用`--mimes`运行copyparty列出所有默认映射


### GDPR合规

想象专业使用copyparty... **TINLA/IANAL；欧盟法律非常令人困惑**

* 记住禁用日志记录，或配置日志轮转到可接受的时间框架，使用`-lo cpp-%Y-%m%d.txt.xz`或类似

* 如果启用数据库运行（推荐），那么使用`--forget-ip 43200`让它在一段时间后忘记上传者IP
  * 不要设置得太低；在这生效后，[撤销](#unpost)文件不再可能

* 如果你实际上*是*律师，那么我愿意接受反馈，会很有趣


### 功能开关

有问题的功能？撕掉它，通过设置以下任何环境变量来禁用其相关的铃声或哨声，

| 环境变量             | 它的作用 |
| -------------------- | ------------ |
| `PRTY_NO_DB_LOCK`    | 不锁定会话/分享数据库以独占访问 |
| `PRTY_NO_IFADDR`     | 通过用ctypes戳你的操作系统来禁用ip/nic发现 |
| `PRTY_NO_IMPRESO`    | 不尝试使用`importlib.resources`加载js/css文件 |
| `PRTY_NO_IPV6`       | 禁用一些ipv6支持（自windows 2000以来应该不必要） |
| `PRTY_NO_LZMA`       | 禁用传入上传的流式xz压缩 |
| `PRTY_NO_MP`         | 禁用python `multiprocessing`模块的所有使用（实际多线程，解析器/缩略图生成器的cpu计数） |
| `PRTY_NO_SQLITE`     | 禁用所有数据库相关功能（文件索引，元数据索引，大多数文件去重逻辑） |
| `PRTY_NO_TLS`        | 禁用原生HTTPS支持；如果你仍然想接受HTTPS连接，那么TLS现在必须由反向代理终止 |
| `PRTY_NO_TPOKE`      | 禁用systemd-tmpfilesd避免器 |

示例：`PRTY_NO_IFADDR=1 python3 copyparty-sfx.py`


### 功能增强

在你的操作系统/环境上强制启用有已知问题的功能，通过设置以下任何环境变量，也亲切地称为`fuckitbits`或`hail-mary-bits`

| 环境变量                 | 它的作用 |
| ------------------------ | ------------ |
| `PRTY_FORCE_MP`          | 在MacOS和其他破损平台上强制启用多进程（真正的多线程） |
| `PRTY_FORCE_MAGIC`       | 在Windows上使用[magic](https://pypi.org/project/python-magic/)（你会段错误） |


# 软件包

聚会可能比你想象的更近

如果下面没有提到你的发行版/操作系统，[«在服务器上»](#on-servers)部分可能有一些提示


## arch软件包

`pacman -S copyparty`（在[arch linux extra](https://archlinux.org/packages/extra/any/copyparty/)中）

它带有[systemd服务](./contrib/systemd/copyparty@.service)以及[用户服务](./contrib/systemd/copyparty-user.service)，并期望在`/etc/copyparty/copyparty.conf`或`~/.config/copyparty/copyparty.conf`中找到[配置文件](./contrib/systemd/copyparty.example.conf)

安装后，启动系统服务或用户服务并导航到http://127.0.0.1:3923获取进一步说明（除非你已经编辑了配置文件，在这种情况下你可以开始了，可能）


## fedora软件包

还不存在；有传言说它正在被打包！关注这个空间...


## homebrew公式

`brew install copyparty ffmpeg` -- https://formulae.brew.sh/formula/copyparty

应该在所有mac（intel和apple silicon）和所有相关macos版本上工作

homebrew软件包由homebrew团队维护（谢谢！）


## nix软件包

`nix profile install github:9001/copyparty`

需要[启用flake](https://nixos.wiki/wiki/Flakes)的nix安装

一些推荐的依赖项默认启用；如果你想添加/删除一些功能/依赖项，[覆盖软件包](https://github.com/9001/copyparty/blob/hovudstraum/contrib/package/nix/copyparty/default.nix#L3-L22)

选择`ffmpeg-full`而不是`ffmpeg-headless`主要是因为我们需要`withWebp`（`withOpenmpt`也很好），能够使用缓存构建感觉比当时优化大小更重要 -- 如果你不同意，欢迎PR 👍


## nixos模块

对于[启用flake](https://nixos.wiki/wiki/Flakes)的NixOS安装：

```nix
{
  # 将copyparty flake添加到你的输入
  inputs.copyparty.url = "github:9001/copyparty";

  # 确保copyparty是outputs函数的允许参数
  outputs = { self, nixpkgs, copyparty }: {
    nixosConfigurations.yourHostName = nixpkgs.lib.nixosSystem {
      modules = [
        # 加载copyparty NixOS模块
        copyparty.nixosModules.default
        ({ pkgs, ... }: {
          # 添加copyparty覆盖以向模块公开软件包
          nixpkgs.overlays = [ copyparty.overlays.default ];
          # （可选）全局安装软件包
          environment.systemPackages = [ pkgs.copyparty ];
          # 配置copyparty模块
          services.copyparty.enable = true;
        })
      ];
    };
  };
};
}
```

如果你在配置中不使用flake，你可以使用其他依赖管理工具，如[npins](https://github.com/andir/npins)、[niv](https://github.com/nmattia/niv)，甚至普通的[`fetchTarball`](https://nix.dev/manual/nix/stable/language/builtins#builtins-fetchTarball)，像这样：

```nix
{ pkgs, ... }:

let
  # npins示例，根据你的设置调整。copyparty应该是下载的仓库的路径
  # 对于niv，只需将npins文件夹导入替换为sources.nix文件
  copyparty = (import ./npins).copyparty;

  # 或使用fetchTarball：
  copyparty = fetchTarball "https://github.com/9001/copyparty/archive/hovudstraum.tar.gz";
in

{
  # 加载copyparty NixOS模块
  imports = [ "${copyparty}/contrib/nixos/modules/copyparty.nix" ];

  # 添加copyparty覆盖以向模块公开软件包
  nixpkgs.overlays = [ (import "${copyparty}/contrib/package/nix/overlay.nix") ];
  # （可选）全局安装软件包
  environment.systemPackages = [ pkgs.copyparty ];
  # 配置copyparty模块
  services.copyparty.enable = true;
}
```

NixOS上的copyparty通过`services.copyparty`选项配置，例如：
```nix
services.copyparty = {
  enable = true;
  # 直接映射到copyparty配置[global]部分的值。
  # 参见`copyparty --help`了解可用选项
  settings = {
    i = "0.0.0.0";
    # 使用列表设置多个值
    p = [ 3210 3211 ];
    # 使用布尔值设置二进制标志
    no-reload = true;
    # 使用'false'将不做任何事情，在生成配置时省略值
    ignored-flag = false;
  };

  # 创建用户
  accounts = {
    # 指定账户名作为键
    ed = {
      # 提供包含密码的文件路径，将其保留在/nix/store之外
      # 必须可被copyparty服务用户读取
      passwordFile = "/run/keys/copyparty/ed_password";
    };
    # 或一次性完成两者
    k.passwordFile = "/run/keys/copyparty/k_password";
  };

  # 创建卷
  volumes = {
    # 在"/"（webroot）创建卷，它将
    "/" = {
      # 共享"/srv/copyparty"的内容
      path = "/srv/copyparty";
      # 参见`copyparty --help-accounts`了解可用选项
      access = {
        # 每个人都获得读访问权限，但
        r = "*";
        # 用户"ed"和"k"获得读写权限
        rw = [ "ed" "k" ];
      };
      # 参见`copyparty --help-flags`了解可用选项
      flags = {
        # "fk"启用文件密钥（upget权限所必需）（4字符长）
        fk = 4;
        # 每60秒扫描新文件
        scan = 60;
        # 卷标志"e2d"启用上传数据库
        e2d = true;
        # "d2t"禁用多媒体解析器（以防上传是恶意的）
        d2t = true;
        # 如果路径匹配*.iso则跳过哈希文件内容
        nohash = "\.iso$";
      };
    };
  };
  # 你可以增加进程的打开文件限制
  openFilesLimit = 8192;
};
```

/run/keys/copyparty/的passwordFile例如可以由[agenix](https://github.com/ryantm/agenix)生成，或者如果可以接受的话，你可以直接将其转储到nix存储中


# 浏览器支持

简而言之：是的

![copyparty-ie4-fs8](https://user-images.githubusercontent.com/241032/118192791-fb31fe00-b446-11eb-9647-898ea8efc1f7.png)

`ie` = internet-explorer，`ff` = firefox，`c` = chrome，`iOS` = iPhone/iPad，`Andr` = Android

| 功能            | ie6 | ie9  | ie10 | ie11 | ff 52 | c 49 | iOS | Andr |
| --------------- | --- | ---- | ---- | ---- | ----- | ---- | --- | ---- |
| 浏览文件        | 是  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| 缩略图视图      |  -  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| 基础上传器      | 是  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| up2k            |  -  |  -   | `*1` | `*1` |  是   | 是   | 是  | 是   |
| 创建目录        | 是  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| 发送消息        | 是  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| 设置排序顺序    |  -  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| zip选择         |  -  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| 文件搜索        |  -  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| 文件重命名      |  -  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| 文件剪切/粘贴   |  -  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| 撤销上传        |  -  |  -   | 是   | 是   |  是   | 是   | 是  | 是   |
| 导航面板        |  -  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| 图像查看器      |  -  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| 视频播放器      |  -  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| markdown编辑器  |  -  |  -   | `*2` | `*2` |  是   | 是   | 是  | 是   |
| markdown查看器  |  -  | `*2` | `*2` | `*2` |  是   | 是   | 是  | 是   |
| 播放mp3/m4a     |  -  | 是   | 是   | 是   |  是   | 是   | 是  | 是   |
| 播放ogg/opus    |  -  |  -   |  -   |  -   |  是   | 是   | `*3`| 是   |
| **= 功能 =**    | ie6 | ie9  | ie10 | ie11 | ff 52 | c 49 | iOS | Andr |

* internet explorer 6到8行为相同
* firefox 52和chrome 49是最终的winxp版本
* `*1` 是的，但极其缓慢（ie10：`1 MiB/s`，ie11：`270 KiB/s`）
* `*2` 只能处理纯文本文档（无markdown渲染）
* `*3` iOS 11及更新版本，仅opus，需要服务器上的FFmpeg

更多古怪网络浏览器尝试查看目录索引的快速摘要：

| 浏览器 | 能否工作 |
| ------- | ------------- |
| **links** (2.21/macports) | 可以浏览、登录、上传/mkdir/msg |
| **lynx** (2.8.9/macports) | 可以浏览、登录、上传/mkdir/msg |
| **w3m** (0.5.3/macports)  | 可以浏览、登录、以100kB/s上传、mkdir/msg |
| **netsurf** (3.10/arch)   | 基本上是有更好css的ie6（javascript几乎没有效果） | 
| **opera** (11.60/winxp)   | 正常：缩略图、图像查看器、zip选择、重命名/剪切/粘贴。不行：up2k、导航面板、markdown、音频 |
| **ie4** 和 **netscape** 4.0  | 可以浏览，用`?b=u`上传，用`&pw=wark`认证 |
| **ncsa mosaic** 2.7       | 不及格，[图1](https://user-images.githubusercontent.com/241032/174189227-ae816026-cf6f-4be5-a26e-1b3b072c1b2f.png) - [图2](https://user-images.githubusercontent.com/241032/174189225-5651c059-5152-46e9-ac26-7e98e497901b.png) |
| **SerenityOS** (7e98457)  | 遇到页面错误，用`?b=u`工作，文件上传未实现 |
| **sony psp** 5.50         | 可以浏览、上传/mkdir/msg（感谢dwarf）[截图](https://github.com/user-attachments/assets/9d21f020-1110-4652-abeb-6fc09c533d4f) |
| **nintendo 3ds**          | 可以浏览、上传、查看缩略图（感谢bnjmn） |
| **Nintendo Wii (Opera 9.0 "Internet Channel")**          | 可以浏览，不能上传或下载（无本地存储），可以查看图像 - 用`?b=u`效果最好，默认视图损坏 |

<p align="center"><img src="https://github.com/user-attachments/assets/88deab3d-6cad-4017-8841-2f041472b853" /></p>


# 客户端示例

使用非浏览器客户端与copyparty交互

* javascript：将一些状态转储到文件中（两个单独的示例）
  * `await fetch('//127.0.0.1:3923/', {method:"PUT", body: JSON.stringify(foo)});`
  * `var xhr = new XMLHttpRequest(); xhr.open('POST', '//127.0.0.1:3923/msgs?raw'); xhr.send('foo');`

* curl/wget：上传一些文件（post=文件，chunk=stdin）
  * `post(){ curl -F f=@"$1" http://127.0.0.1:3923/?pw=wark;}`  
    `post movie.mkv`  （返回HTML）
  * `post(){ curl -F f=@"$1" 'http://127.0.0.1:3923/?want=url&pw=wark';}`  
    `post movie.mkv`  （返回热链接）
  * `post(){ curl -H pw:wark -H rand:8 -T "$1" http://127.0.0.1:3923/;}`  
    `post movie.mkv`  （随机文件名）
  * `post(){ wget --header='pw: wark' --post-file="$1" -O- http://127.0.0.1:3923/?raw;}`  
    `post movie.mkv`
  * `chunk(){ curl -H pw:wark -T- http://127.0.0.1:3923/;}`  
    `chunk <movie.mkv`

* bash：当curl和wget不可用或太无聊时
  * `(printf 'PUT /junk?pw=wark HTTP/1.1\r\n\r\n'; cat movie.mkv) | nc 127.0.0.1 3923`
  * `(printf 'PUT / HTTP/1.1\r\n\r\n'; cat movie.mkv) >/dev/tcp/127.0.0.1/3923`

* python：[u2c.py](https://github.com/9001/copyparty/blob/hovudstraum/bin/u2c.py)是命令行up2k客户端[(webm)](https://ocv.me/stuff/u2cli.webm)
  * 文件上传、文件搜索、[文件夹同步](#folder-sync)、中止/损坏上传的自动恢复
  * 可以从copyparty下载：控制面板 -> 连接 -> [u2c.py](http://127.0.0.1:3923/.cpr/a/u2c.py)
  * 参见[./bin/README.md#u2cpy](bin/README.md#u2cpy)

* FUSE：将copyparty服务器挂载为本地文件系统
  * [./bin/](bin/)中提供跨平台python客户端
  * 也能挂载nginx和iis目录列表，不仅仅是copyparty
  * 可以从copyparty下载：控制面板 -> 连接 -> [partyfuse.py](http://127.0.0.1:3923/.cpr/a/partyfuse.py)
  * [rclone](https://rclone.org/)作为客户端可以提供约5倍性能，参见[./docs/rclone.md](docs/rclone.md)

* sharex（截图工具）：参见[./contrib/sharex.sxcu](./contrib/#sharexsxcu)
  * 对于macos上的截图，参见[./contrib/ishare.iscu](./contrib/#ishareiscu)
  * 对于linux上的截图，参见[./contrib/flameshot.sh](./contrib/flameshot.sh)

* [Custom Uploader](https://f-droid.org/en/packages/com.nyx.custom_uploader/)（Android应用）作为copyparty自己的[PartyUP!](#android-app)的替代
  * 如果你将UploadURL设置为`https://your.com/foo/?want=url&pw=hunter2`，FormDataName设置为`f`，就能工作

* contextlet（网络浏览器集成）；参见[contrib contextlet](contrib/#send-to-cppcontextletjson)

* [igloo irc](https://iglooirc.com/)：方法：`post` 主机：`https://you.com/up/?want=url&pw=hunter2` 多部分：`yes` 文件参数：`f`

copyparty返回你的PUT/POST的截断sha512sum作为base64；你可以在本地生成相同的校验和来验证上传：

    b512(){ printf "$((sha512sum||shasum -a512)|sed -E 's/ .*//;s/(..)/\\x\1/g')"|base64|tr '+/' '-_'|head -c44;}
    b512 <movie.mkv

你可以使用头部`PW: hunter2`、cookie `cppwd=hunter2`、url参数`?pw=hunter2`或基本认证（作为用户名或密码）提供密码

> 对于基本认证，以下所有都被接受：`password` / `whatever:password` / `password:whatever`（用户名被忽略）

* 除非你启用了`--usernames`，那么是`PW: usr:pwd`、cookie `cppwd=usr:pwd`、url参数`?pw=usr:pwd`

注意：如果你使用`-T`结合url参数，curl不会发送原始文件名！另外，确保总是在URL中留下尾随斜杠，除非你想覆盖文件名


## 文件夹同步

与copyparty同步文件夹

注意：完全双向同步，像[nextcloud](https://docs.nextcloud.com/server/latest/user_manual/sv/files/desktop_mobile_sync.html)和[syncthing](https://syncthing.net/)那样，永远不会被支持！copyparty只能进行单向同步（服务器到客户端，或客户端到服务器）

* 如果你想要双向同步，那么copyparty和syncthing*应该*完全安全地结合；它们应该能够在相同文件夹上协作而不会给彼此造成任何麻烦。许多人这样做，到目前为止没有问题。但是，如果你*确实*遇到任何问题，请[提交copyparty错误](https://github.com/9001/copyparty/issues/new/choose)，我会尝试帮助 -- 只是记住我以前从未使用过syncthing :-)

带有`--dr`的命令行上传器[u2c.py](https://github.com/9001/copyparty/tree/hovudstraum/bin#u2cpy)是同步文件夹到copyparty的最佳方式；验证校验和并并行处理文件，在上传完成后删除服务器上的意外文件，这使文件重命名真的很便宜（它会在服务器端重命名并跳过上传）

如果你想用`u2c.py`同步，那么：
* 服务器上你要同步到的卷必须启用`e2dsa`选项（全局或卷标志）
* ...但不要启用全局选项`no-hash`或`no-idx`（或卷标志`nohash` / `noidx`），或至少确保它们配置为不影响你要同步到的任何内容
* ...并且u2c需要删除权限，所以至少`rwd`，或只是`A`，这与`rwmd.a`相同
  * 快速提醒`a`和`A`是不同的权限，`.`对同步非常有用

或者有[rclone](./docs/rclone.md)，它允许双向同步并且*更*灵活（直接从sftp/s3/gcs流式传输文件到copyparty，...），尽管没有完整性检查，如果copyparty在cloudflare后面，它不会处理超过100 MiB的文件

* 从rclone v1.63开始，rclone在低延迟连接上比u2c.py更快
  * 但这只对初始上传为真；u2c对定期同步会更快


## 挂载为驱动器

将远程copyparty服务器作为本地文件系统；转到控制面板并点击`connect`查看执行此操作的命令列表

或者，一些按速度大致排序的替代方案（不可重现的基准测试），最好的在前：

* [rclone-webdav](./docs/rclone.md)（25秒），读/写（rclone v1.63或更高版本）
* [rclone-http](./docs/rclone.md)（26秒），只读
* [partyfuse.py](./bin/#partyfusepy)（26秒），只读
* [rclone-ftp](./docs/rclone.md)（47秒），读/写
* davfs2（103秒），读/写
* [win10-webdav](#webdav-server)（138秒），读/写
* [win10-smb2](#smb-server)（387秒），读/写

大多数客户端将无法挂载copyparty服务器的根，除非有根卷（所以你访问时得到管理面板而不是浏览器） -- 在这种情况下，改为挂载特定卷

如果你有无需密码即可访问的卷，那么一些webdav客户端（如davfs2）需要全局选项`--dav-auth`来访问任何受密码保护的区域


# 安卓应用

一键上传到copyparty

<a href="https://f-droid.org/packages/me.ocv.partyup/"><img src="https://ocv.me/fdroid.png" alt="Get it on F-Droid" height="50" /> '' <img src="https://img.shields.io/f-droid/v/me.ocv.partyup.svg" alt="f-droid version info" /></a> '' <a href="https://github.com/9001/party-up"><img src="https://img.shields.io/github/release/9001/party-up.svg?logo=github" alt="github version info" /></a>

该应用**不是**完整的copyparty服务器！只是一个基本的上传客户端，还没有什么花哨的功能

如果你想在安卓设备上运行copyparty服务器，参见[在安卓上安装](#install-on-android)


# iOS快捷指令

没有iPhone应用，但以下快捷指令几乎一样好：

* [上传到copyparty](https://www.icloud.com/shortcuts/41e98dd985cb4d3bb433222bc1e9e770)（[离线](https://github.com/9001/copyparty/raw/hovudstraum/contrib/ios/upload-to-copyparty.shortcut)）（[png](https://user-images.githubusercontent.com/241032/226118053-78623554-b0ed-482e-98e4-6d57ada58ea4.png)）基于[Daedren](https://github.com/Daedren)的[原版](https://www.icloud.com/shortcuts/ab415d5b4de3467b9ce6f151b439a5d7)（谢谢！）
  * 可以剥离exif、上传文件、图片、视频、链接、剪贴板
  * 可以下载链接并在copyparty上重新托管目标文件（参见快捷指令内的第一个注释）
  * 如果你从图库分享到快捷指令，图片会变成低分辨率，所以最好启动快捷指令并从那里选择内容

如果你想在iPhone或iPad上运行copyparty服务器，参见[在iOS上安装](#install-on-iOS)


# 性能

默认设置通常很好 - 期望`8 GiB/s`下载，`1 GiB/s`上传

下面是一些按有用性大致排序的调整：

* 禁用HTTP/2和HTTP/3可以使上传快5倍，取决于服务器/客户端软件
* `-q`禁用日志记录，可以帮助很多，即使与`-lo`结合将日志重定向到文件
* `--hist`指向快速位置（ssd）将使目录列表和搜索在设置`-e2d`或`-e2t`时更快
  * 也使缩略图加载更快，无论e2d/e2t如何
* `--dedup`启用去重，因此如果有人上传重复文件，避免写入硬盘
* `--safe-dedup 1`通过跳过文件内容验证使上传期间的去重更快；如果没有其他软件编辑/移动卷中的文件则安全
* `--no-dirsz`显示文件夹inode的大小而不是内容的总大小，提供约30%更快的文件夹列表
* `--no-hash .`当索引网络磁盘时，如果你不关心实际文件哈希，只想要名称/标签可搜索
* 如果你的卷在网络磁盘上，如NFS / SMB / s3，为`--iobuf`和/或`--s-rd-sz`和/或`--s-wr-sz`指定更大的值可能有帮助；尝试将它们全部设置为`524288`或`1048576`或`4194304`
* `--no-htp --hash-mt=0 --mtag-mt=1 --th-mt=1`最小化线程数；可以在一些古怪环境中帮助（如vscode调试器）
* 在AlpineLinux或其他基于musl的发行版上运行时，尝试mimalloc以获得更高性能（和两倍的RAM使用）；`apk add mimalloc2`并使用环境变量`LD_PRELOAD=/usr/lib/libmimalloc-secure.so.2`运行copyparty
  * 注意mimalloc与prisonparty和/或bubbleparty/bubblewrap结合时需要特别小心；你必须给它访问`/proc`和`/sys`的权限，否则你会遇到FFmpeg问题（音频转码、缩略图）
* `-j0`启用多进程（实际多线程），可以将延迟减少到`20+80/numCores`百分比，通常在CPU密集型工作负载中提高性能，例如：
  * 大量连接（许多用户或重客户端）
  * 同时下载和上传饱和20gbps连接
  * 如果启用`-e2d`，`-j2`为目录列表提供4倍性能；`-j4`提供16倍
  
  ...但是它也增加上传期间的服务器/文件系统/硬盘负载，并为内部通信增加开销，所以通常最好不要
* 使用[pypy](https://www.pypy.org/)而不是[cpython](https://www.python.org/)*可以*对某些工作负载快70%，但对许多其他工作负载更慢
  * pypy有时可能在启动时与`-j0`一起崩溃（TODO创建问题）


## 客户端

上传文件时，

* 当从非常快的存储（NVMe SSD）使用chrome/firefox上传时，在`[⚙️] settings`标签中启用`[wasm]`以更有效地使用所有CPU核心进行哈希
  * 不要在Safari上这样做（不使用运行更快）
  * 不要在较旧的浏览器上这样做；可能引发浏览器错误（浏览器吃掉所有RAM并崩溃）
  * 可以在服务器端使用`--nosubtle 137`（chrome v137+）或`--nosubtle 2`（chrome+firefox）设为默认启用

* 推荐chrome（不幸的是），至少与firefox相比：
  * 哈希时快达90%，特别是在SSD上
  * 在极快的互联网上上传时快达40%
  * 但[u2c.py](https://github.com/9001/copyparty/blob/hovudstraum/bin/u2c.py)可以比chrome再快40%

* 如果你受CPU瓶颈限制，或浏览器正在最大化CPU核心：
  * 如果你通过切换离开`[🚀]` up2k ui标签（或关闭它）隐藏上传状态列表，上传可以快达30%
    * 可选地，你可以通过点击`[🥔]`切换到轻量级土豆UI
    * 切换到另一个浏览器标签也有效，在这种情况下图标会每10秒更新一次
  * 不太可能是问题，但在上传许多小文件时可能发生，或你的互联网太快，或PC太慢


# 安全性

有一个[discord服务器](https://discord.gg/25J8CdTT6G)，对所有重要更新有`@everyone`（缺乏更好的想法）

一些关于加固的注意事项

* 设置`--rproxy 0` *当且仅当*你的copyparty直接面向互联网（不通过反向代理）
  * 否则cors不能正常工作
* 如果你允许匿名上传或不信任卷的内容，你可以用卷标志`nohtml`防止XSS
  * 这将html文档作为纯文本返回，也禁用markdown渲染
* 在反向代理后面运行时，监听unix套接字以获得更严格的访问控制（和更多性能）；参见[反向代理](#reverse-proxy)或`--help-bind`

安全配置文件：

* 选项`-s`是设置以下选项的快捷方式：
  * `--no-thumb`禁用缩略图和音频转码，阻止copyparty在上传文件上运行`FFmpeg`/`Pillow`/`VIPS`，如果启用匿名上传，这是一个[好主意](https://www.cvedetails.com/vulnerability-list.php?vendor_id=3611)
  * `--no-mtag-ff`使用`mutagen`而不是`FFmpeg`获取音乐标签，这更安全更快但不太准确
  * `--dotpart`在上传仍在传入时从目录列表中隐藏它们
  * `--no-robots`和`--force-js`使爬虫的生活更困难，参见[对Google隐藏](#hiding-from-google)

* 选项`-ss`是上述的快捷方式加上：
  * `--unpost 0`、`--no-del`、`--no-mv`禁用所有移动/删除支持
  * `--hardlink`在去重上传时创建硬链接而不是符号链接，这需要更少维护
    * 但是注意如果你编辑一个文件，它也会影响其他副本
  * `--vague-403`返回"404 not found"而不是"401 unauthorized"，这是一个常见的企业模因
  * `-nih`从目录列表中删除服务器主机名

* 选项`-sss`是上述的快捷方式加上：
  * `--no-dav`禁用webdav支持
  * `--no-logues`和`--no-readme`禁用目录列表中readme和序言/结语的支持，否则让人们上传任意（但沙盒化的）`<script>`标签
  * `-lo cpp-%Y-%m%d-%H%M%S.txt.xz`启用磁盘日志记录
  * `-ls **,*,ln,p,r`在启动时扫描任何危险的符号链接

其他杂项注意事项：

* 你可以通过给予权限`g`而不是`r`来禁用目录列表，只接受文件的直接URL
  * 你可能想要[文件密钥](#filekeys)来防止文件名暴力破解
  * 权限`h`而不是`r`使copyparty表现得像传统网络服务器，禁用目录列表/索引，改为返回index.html
    * 与文件密钥的兼容性：index.html本身可以在没有正确文件密钥的情况下检索，但所有其他文件都受保护


## 陷阱

可能意外的行为

* 没有文件夹读取权限的用户仍然可以看到`.prologue.html` / `.epilogue.html` / `PREADME.md` / `README.md`内容，目的是显示如何使用上传器的描述
* 用户可以通过几种方式提交自动运行（在沙盒中）的`<script>`给其他访问者；
  * 上传`README.md` -- 用`--no-readme`避免
  * 将`some.html`重命名为`.epilogue.html` -- 用`--no-logues`或`--no-dot-ren`避免
  * 目录列表嵌入是沙盒化的（所以任何恶意脚本不能造成任何损害），但markdown编辑器不是100%安全的，见下文
* markdown文档可以包含html和`<script>`；尝试阻止脚本执行（除非指定`-emp`），但这不是100%防弹的，所以设置`nohtml`卷标志仍然是最安全的选择
  * 或通过只给可信任的人写访问权限来完全消除问题 :^)


## cors

跨站请求配置

默认情况下，除了`GET`和`HEAD`操作，所有请求必须：
* 根本不包含`Origin`头部
* 或有与服务器域匹配的`Origin`
* 或头部`PW`，值为你的密码

cors可以用`--acao`和`--acam`配置，或用`--allow-csrf`完全禁用保护


## 文件密钥

防止文件名暴力破解

卷标志`fk`为所有文件生成文件密钥（按文件访问密钥）；有完全读取权限（权限`r`）的用户将看到附加了正确文件密钥`?k=...`的URL，`g`用户必须提供包括正确密钥的URL以避免404

默认情况下，文件密钥基于盐（`--fk-salt`）+ 文件系统路径 + 文件大小 + inode（如果不是windows）生成；添加卷标志`fka`生成稍微弱一些的文件密钥，如果文件被编辑不会失效（只有盐 + 路径）

权限`wG`（写 + upget）让用户上传文件并接收自己的文件密钥，仍然无法看到其他上传

### 目录密钥

在卷中分享特定文件夹而不给出对其余部分的完全读取权限 -- 访问者只需要`g`（获取）权限来查看链接

卷标志`dk`为所有文件夹生成目录密钥（按目录访问密钥），授予对该文件夹的读取权限；默认只有该文件夹本身，没有子文件夹

卷标志`dky`禁用实际的密钥检查，意味着任何人都可以看到他们有`g`访问权限的文件夹内容，但不能看到其子目录

* `dk` + `dky`给出与所有有`g`访问权限的用户有完全读取权限相同的行为，但子文件夹是隐藏文件（就像它们的名称以点开头），所以`dky`是为此目的重命名所有文件夹的替代方案，也许只对某些用户

卷标志`dks`让人们也进入子文件夹，也启用下载为zip/tar

如果你启用目录密钥，启用文件密钥也可能是个好主意，否则从使用目录密钥访问的文件夹热链接文件将是不可能的

目录密钥基于另一个盐（`--dk-salt`）+ 文件系统路径生成，有一些限制：
* 如果文件夹内容被修改，密钥不会改变
  * 如果你需要新的目录密钥，要么更改盐要么重命名文件夹
* 如果接收者没有读取权限，链接到文本文件（所以它在文本文件查看器中打开）是不可能的


## 密码哈希

你可以在将密码放入配置文件/作为参数提供之前哈希密码；参见`--help-pwhash`了解所有详细信息

`--ah-alg argon2`启用它，如果你有任何明文密码，它会在启动时打印哈希版本，这样你可以替换它们

可选地也指定`--ah-cli`进入交互模式，它将哈希密码而不会将明文密码写入磁盘

默认配置在一台不错的笔记本电脑上处理新密码大约需要0.4秒和256 MiB RAM

当为docker或systemd服务使用`--ah-cli`生成哈希时，确保它使用相同的`--ah-salt`：
* 使用copyparty服务配置中的`--show-ah-salt`检查生成的盐
* 在两个环境中设置相同的`--ah-salt`

> ⚠️ 如果你启用了`--usernames`，那么在哈希时提供密码为`username:password`，例如`ed:hunter2`


## https

默认情况下HTTP和HTTPS都被接受，但让[反向代理](#reverse-proxy)处理https/tls/ssl会更好（可能默认更安全）

copyparty不支持HTTP/2或QUIC，所以使用反向代理也会解决这个问题 -- 但注意HTTP/1通常比HTTP/2和HTTP/3都快

如果安装了[cfssl](https://github.com/cloudflare/cfssl/releases/latest)，copyparty将在启动时自动创建CA和服务器证书
* 证书写入`--crt-dir`用于分发，参见`--help`了解其他`--crt`选项
* 这将是自签名证书，所以你必须将你的`ca.pem`安装到所有浏览器/设备中
* 如果你想避免手动分发证书的麻烦，请考虑使用反向代理


# 从崩溃中恢复

## 客户端崩溃

### firefox白屏

firefox 87可能在上传期间崩溃 -- 整个浏览器都会崩溃，包括所有其他浏览器标签，一切都变白

但是你可以在up2k标签中按`F12`并使用开发工具查看你在上传中走了多远：

* 获取所有上传的完整列表，按状态组织（ok / no-good / busy / queued）：  
  `var tabs = { ok:[], ng:[], bz:[], q:[] }; for (var a of up2k.ui.tab) tabs[a.in].push(a); tabs`

* 失败的文件名列表：  
  `​var ng = []; for (var a of up2k.ui.tab) if (a.in != 'ok') ng.push(a.hn.split('<a href=\"').slice(-1)[0].split('\">')[0]); ng`

* 将文件名列表发送到copyparty保存：  
  `await fetch('/inc', {method:'PUT', body:JSON.stringify(ng,null,1)})`


# HTTP API

参见[开发说明](./docs/devnotes.md#http-api)


# 依赖项

强制依赖项：
* `jinja2`（内置在SFX中）


## 可选依赖项

安装这些以启用额外功能

启用配置中的[哈希密码](#password-hashing)：`argon2-cffi`

启用[ftp服务器](#ftp-server)：
* 仅纯文本FTP，`pyftpdlib`（内置在SFX中）
* 带TLS加密，`pyftpdlib pyopenssl`

启用[音乐标签](#metadata-from-audio-files)：
* 要么`mutagen`（快，纯python，跳过一些标签，使copyparty GPL？不知道）
* 或`ffprobe`（慢20倍，更准确，根据你的发行版和用户可能危险）

启用[缩略图](#thumbnails)...
* **图像：** `Pillow`和/或`pyvips`和/或`ffmpeg`（需要py2.7或py3.5+）
* **视频/音频：** `ffmpeg`和`ffprobe`在`$PATH`中某处
* **HEIF图片：** `pyvips`或`ffmpeg`或`pillow-heif`
* **AVIF图片：** `pyvips`或`ffmpeg`或`pillow-avif-plugin`或pillow v11.3+
* **JPEG XL图片：** `pyvips`或`ffmpeg`
* **RAW图像：** `rawpy`，加上`pyvips`或`Pillow`之一（对某些格式）

启用从事件钩子发送[zeromq消息](#zeromq)：`pyzmq`

启用[smb](#smb-server)支持（**不**推荐）：`impacket==0.12.0`

`pyvips`比`Pillow`提供更高质量的缩略图，快320%，使用270%更多ram：`sudo apt install libvips42 && python3 -m pip install --user -U pyvips`

要在Windows上安装FFmpeg，获取[最新构建](https://www.gyan.dev/ffmpeg/builds/ffmpeg-git-full.7z) -- 你需要`bin`文件夹内的`ffmpeg.exe`和`ffprobe.exe`；将它们复制到`C:\Windows\System32`或你的`%PATH%`中的任何其他文件夹


### 依赖项开关

防止加载可选依赖项，例如如果：

* 你安装了不兼容的版本并导致问题
* 你只是不想让copyparty使用它，也许为了节省ram

设置以下任何环境变量来禁用其相关的可选功能，

| 环境变量             | 它的作用 |
| -------------------- | ------------ |
| `PRTY_NO_ARGON2`     | 禁用argon2-cffi密码哈希 |
| `PRTY_NO_CFSSL`      | 永远不尝试使用[cfssl](https://github.com/cloudflare/cfssl)生成自签名证书 |
| `PRTY_NO_FFMPEG`     | **音频转码**消失，**缩略图**必须由Pillow/libvips处理 |
| `PRTY_NO_FFPROBE`    | **音频转码**消失，**缩略图**必须由Pillow/libvips处理，**元数据扫描**必须由mutagen处理 |
| `PRTY_NO_MAGIC`      | 不使用[magic](https://pypi.org/project/python-magic/)进行文件类型检测 |
| `PRTY_NO_MUTAGEN`    | 不使用[mutagen](https://pypi.org/project/mutagen/)从媒体文件读取元数据；将回退到ffprobe |
| `PRTY_NO_PIL`        | 禁用所有基于[Pillow](https://pypi.org/project/pillow/)的缩略图支持；将回退到libvips或ffmpeg |
| `PRTY_NO_PILF`       | 禁用Pillow `ImageFont`文本渲染，用于文件夹缩略图 |
| `PRTY_NO_PIL_AVIF`   | 禁用Pillow avif支持（内部和/或[插件](https://pypi.org/project/pillow-avif-plugin/)） |
| `PRTY_NO_PIL_HEIF`   | 禁用第三方Pillow [HEIF支持](https://pypi.org/project/pillow-heif/)插件 |
| `PRTY_NO_PIL_WEBP`   | 禁用Pillow中原生webp支持的使用 |
| `PRTY_NO_PSUTIL`     | 不使用[psutil](https://pypi.org/project/psutil/)在Windows上收割卡住的钩子和插件 |
| `PRTY_NO_RAW`        | 禁用所有基于[rawpy](https://pypi.org/project/rawpy/)的RAW图像缩略图支持 |
| `PRTY_NO_VIPS`       | 禁用所有基于[libvips](https://pypi.org/project/pyvips/)的缩略图支持；将回退到Pillow或ffmpeg |

示例：`PRTY_NO_PIL=1 python3 copyparty-sfx.py`

* `PRTY_NO_PIL`节省ram
* `PRTY_NO_VIPS`节省ram和启动时间
* windows上的python2.7：`PRTY_NO_FFMPEG` + `PRTY_NO_FFPROBE`节省启动时间


## 可选GPL内容

一些捆绑工具有copyleft依赖项，参见[./bin/#mtag](bin/#mtag)

这些是独立程序，永远不会被copyparty导入/评估，必须通过`-mtp`配置启用


# sfx

自包含"二进制文件"（推荐！）[copyparty-sfx.py](https://github.com/9001/copyparty/releases/latest/download/copyparty-sfx.py)将解包自己并运行copyparty，假设你当然安装了python

如果你只需要英语，[copyparty-en.py](https://github.com/9001/copyparty/releases/latest/download/copyparty-en.py)是同样的东西但更小

你可以通过重新打包来减少sfx大小；参见[./docs/devnotes.md#sfx-repack](./docs/devnotes.md#sfx-repack)


## copyparty.exe

下载[copyparty.exe](https://github.com/9001/copyparty/releases/latest/download/copyparty.exe)（win8+）或[copyparty32.exe](https://github.com/9001/copyparty/releases/latest/download/copyparty32.exe)（win7+）

![copyparty-exe-fs8](https://user-images.githubusercontent.com/241032/221445946-1e328e56-8c5b-44a9-8b9f-dee84d942535.png)

在安装python有问题的机器上可能很方便，但**不推荐** -- 如果可能，请改用**[copyparty-sfx.py](https://github.com/9001/copyparty/releases/latest/download/copyparty-sfx.py)**

* [copyparty.exe](https://github.com/9001/copyparty/releases/latest/download/copyparty.exe)在win8或更新版本上运行，在win10上编译，做缩略图 + 媒体标签，*目前*使用安全，但任何未来的python/expat/pillow CVE只能通过下载更新版本的exe来修复

  * 在win8上需要[vc redist 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48145)，在win10上直接工作
  * 一些杀毒软件可能会惊慌（误报），可能[Avast、AVG和McAfee](https://www.virustotal.com/gui/file/52391a1e9842cf70ad243ef83844d46d29c0044d101ee0138fcdd3c8de2237d6/detection)

* 危险：[copyparty32.exe](https://github.com/9001/copyparty/releases/latest/download/copyparty32.exe)与[windows7](https://user-images.githubusercontent.com/241032/221445944-ae85d1f4-d351-4837-b130-82cab57d6cca.png)兼容，这意味着它使用古老的python副本（3.7.9），无法升级，永远不应该暴露在互联网上（局域网没问题）

* 危险且已弃用：[copyparty-winpe64.exe](https://github.com/9001/copyparty/releases/download/v1.8.7/copyparty-winpe64.exe)让你[在WinPE中运行copyparty](https://user-images.githubusercontent.com/241032/205454984-e6b550df-3c49-486d-9267-1614078dd0dd.png)，否则完全无用

同时[copyparty-sfx.py](https://github.com/9001/copyparty/releases/latest/download/copyparty-sfx.py)依赖于你的系统python，这提供更好的性能，只要你保持python安装最新就会保持安全

话说回来，如果你已经在从互联网下载可疑二进制文件，你可能也想要我的[最小构建](./scripts/pyinstaller#ffmpeg)的[ffmpeg](https://ocv.me/stuff/bin/ffmpeg.exe)和[ffprobe](https://ocv.me/stuff/bin/ffprobe.exe)，它使copyparty能够提取多媒体信息、做音频转码和缩略图/频谱图/波形，但如果你能承受大小，最好偶尔获取[最新官方构建](https://www.gyan.dev/ffmpeg/builds/ffmpeg-git-full.7z)


## zipapp

另一个紧急替代方案，[copyparty.pyz](https://github.com/9001/copyparty/releases/latest/download/copyparty.pyz)功能较少，很慢，需要python 3.7或更新版本，压缩更差，更重要的是无法从更新版本的jinja2等中受益（这使它不太安全）...这个真的有很多缺点 -- 但是，与sfx不同，它是一个完全正常的zipfile，不会将任何临时文件解包到磁盘，所以如果常规sfx因为计算机以某些奇怪方式搞砸而无法启动，它*可能*会工作，所以如果其他都失败了值得一试

通过双击运行它，或如果失败，尝试在你的终端/控制台/命令行/电传中输入`python copyparty.pyz`

它是一个python [zipapp](https://docs.python.org/3/library/zipapp.html)，意味着它不必将自己的python代码解包到任何地方运行，所以如果文件系统损坏，它有更好的机会到达某处
* 但注意它目前仍然需要将web资源提取到某处（它们会落在你操作系统的默认TEMP文件夹中）


# 在安卓上安装

安装[Termux](https://termux.com/) + 其伴侣应用`Termux:API`（参见[ocv.me/termux](https://ocv.me/termux/)），然后将此复制粘贴到Termux（长按）一次性全部：
```sh
yes | pkg upgrade && termux-setup-storage && yes | pkg install python termux-api && python -m ensurepip && python -m pip install --user -U copyparty && { grep -qE 'PATH=.*\.local/bin' ~/.bashrc 2>/dev/null || { echo 'PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc && . ~/.bashrc; }; }
echo $?
```

初始设置后，你可以通过在Termux中任何地方运行`copyparty`随时启动copyparty -- 如果你用`--qr`运行它，你会得到一个指向你外部ip的[整洁二维码](#qr-code)

如果你想要缩略图（照片+视频）并且愿意花费另外132 MiB存储，`pkg install ffmpeg && python3 -m pip install --user -U pillow`

* 或如果你想用`vips`做照片缩略图，`pkg install libvips && python -m pip install --user -U wheel && python -m pip install --user -U pyvips && (cd /data/data/com.termux/files/usr/lib/; ln -s libgobject-2.0.so{,.0}; ln -s libvips.so{,.42})`


# 在iOS上安装

首先安装以下之一：
* [a-Shell mini](https://apps.apple.com/us/app/a-shell-mini/id1543537943)给你基本功能
* [a-Shell](https://apps.apple.com/us/app/a-shell/id1473805438)也启用音频转码和更好的缩略图

然后将以下命令复制粘贴到`a-Shell`：

```sh
curl https://github.com/9001/copyparty/raw/refs/heads/hovudstraum/contrib/setup-ashell.sh | sh
```

这做什么：
* 创建一个名为`cpc`的基本[配置文件](#accounts-and-volumes)，你可以用`vim cpc`编辑
* 添加命令`cpp`用该配置文件启动copyparty

已知问题：
* 无法在后台运行；它需要在屏幕上接受连接/上传/下载
* 退出copyparty的最佳方式是滑走应用


# 报告错误

包含上下文的想法，以及提交位置

请使用以下任何URL联系：
* https://github.com/9001/copyparty/ **（主要）**
* https://gitlab.com/9001/copyparty/ *（镜像）*
* https://codeberg.org/9001/copyparty *（镜像）*

一般来说，命令行参数（和配置文件如果有）

如果上传期间某些东西损坏（用损坏的文件名的一部分替换FILENAME）：
```
journalctl -aS '48 hour ago' -u copyparty | grep -C10 FILENAME | tee bug.log
```

如果日志中有base64墙（线程堆栈），请包含那个，特别是如果你遇到冻结或卡住的东西，例如`OperationalError('database is locked')` -- 或者你可以访问`/?stack`实时查看堆栈，所以例如http://127.0.0.1:3923/?stack


# 开发说明

构建说明等，参见[./docs/devnotes.md](./docs/devnotes.md)

特别是你可能想要[构建sfx](https://github.com/9001/copyparty/blob/hovudstraum/docs/devnotes.md#just-the-sfx)或[从头构建](https://github.com/9001/copyparty/blob/hovudstraum/docs/devnotes.md#build-from-scratch)

参见[./docs/TODO.md](./docs/TODO.md)了解计划的功能/修复/更改
