## 开发笔记目录

* 顶部
* [未来想法](#未来想法) - 可能永远不会实现的梦想清单
* [设计](#设计)
    * [up2k](#up2k) - up2k 协议的快速概述
        * [为什么不用 tus](#为什么不用-tus) - 我不知道 [tus](https://tus.io/)
        * [为什么使用块哈希](#为什么使用块哈希) - 单个 sha512 会更好，对吧？
        * [块大小列表](#块大小列表) - 强制使用特定的块大小
* [哈希密码](#哈希密码) - 关于奇怪的决定
* [http api](#http-api)
    * [读取](#读取)
    * [写入](#写入)
    * [管理](#管理)
    * [通用](#通用)
* [事件钩子](#事件钩子) - 关于编写你自己的[钩子](../README.md#event-hooks)
    * [钩子效果](#钩子效果) - 钩子可以产生有意的副作用
* [假设](#假设)
    * [mdns](#mdns)
* [sfx 重新打包](#sfx-重新打包) - 通过移除功能来减少 sfx 的大小
* [构建](#构建)
    * [开发环境设置](#开发环境设置)
    * [仅构建 sfx](#仅构建-sfx)
    * [从发布压缩包构建](#从发布压缩包构建) - 使用包含的预构建 webdeps
    * [从头开始构建](#从头开始构建) - 制作过程
    * [完整发布](#完整发布)
* [调试](#调试)
    * [手机上音乐播放停止](#手机上音乐播放停止) - 在 android 上基本正常
    * [废弃的想法](#废弃的想法)


# 未来想法

可能永远不会实现的梦想清单

* JS 是一团糟 -- ~~preact~~ 重写会很好
  * 最好不要像 webpack/babel/node.js 这样的构建依赖，也许用 python 来将 js 文件组装成 main.js
  * 很好的借口来看看使用虚拟列表（当文件夹包含超过 5000 个文件时浏览器开始卡顿）
  * 也许 preact / vdom 不是最好的选择，可以等待下一个大事件
* UX 是一团糟 -- 合适的设计会很好
  * 非常有机（就像 python/js 一样），一切都是事后想法
  * 对于布局和视觉效果都是如此
  * 像 tron 会议室 ui（或大多数其他好莱坞的，如钢铁侠）会很 :100:
    * 最好保持信息密度，只是更有组织但[不太无聊](https://blog.rachelbinx.com/2023/02/unbearable-sameness/)
* 一些 python 文件太大了
  * `up2k.py` 最终做了所有文件索引 / 数据库管理
  * `httpcli.py` 一般应该分离成模块


# 设计

## up2k

up2k 协议的快速概述，参见[上传](https://github.com/9001/copyparty#uploading)了解 web 客户端
* up2k 客户端将文件分割成"最优"数量的块
  * 每个 1 MiB，除非超过 256 个块
  * 尝试 1.5M、2M、3、4、6、... 直到 <= 256 个块或大小 >= 32M
* 客户端发送哈希列表、文件名、大小、最后修改时间
* 服务器创建 `wark`，这次上传的标识符
  * `sha512( salt + filesize + chunk_hashes )`
  * 并创建一个稀疏文件供块放入
* 客户端发送一系列 POST，每个包含一个或多个连续块
  * 块哈希（逗号分隔）和 wark 的头部条目
  * 服务器根据哈希将块写入位置
* 客户端用哈希列表再次握手；服务器回复 OK 或需要重新上传的块列表

up2k 已经拯救了一些上传免于在传输中损坏；
* 在 wireshark 中抓到一个 wifi 上的 android 手机有位翻转，但是带 https 的 bup *可能*也会注意到（感谢 tls 也作为完整性检查）
* 也阻止了某人上传，因为他们的内存坏了

关于上传期间频繁的服务器日志消息；  
`6.0M 106M/s 2.77G 102.9M/s n948 thank 4/0/3/1 10042/7198 00:01:09`
* 这个块是 `6 MiB`，以 `106 MiB/s` 上传
* 在这个 http 连接上，传输了 `2.77 GiB`，平均 `102.9 MiB/s`，处理了 `948` 个块
* 客户端说 `4` 个上传 OK，`0` 个失败，`3` 个忙碌，`1` 个排队，总大小 `10042 MiB`，剩余 `7198 MiB` 和 `00:01:09`

### 为什么不用 tus

当我制作这个时我不知道 [tus](https://tus.io/)，但是：
* up2k 的优势是它支持非连续块的并行上传直接到最终文件 -- [tus 在最后进行合并](https://tus.io/protocols/resumable-upload.html#concatenation)，这很慢并且对服务器硬盘/文件系统造成负担（除非我理解错了）
* up2k 的轻微劣势是需要客户端在上传开始前对整个文件进行哈希，但这有立即跳过重复文件的好处
  * 而且哈希在单独的线程中进行，所以通常不是瓶颈

### 为什么使用块哈希

单个 sha512 会更好，对吧？

这是由于 `crypto.subtle` [尚未](https://github.com/w3c/webcrypto/issues/73)提供流式 api（或用起始哈希为 sha512 哈希器播种的选项）

结果，哈希比它们本来可能的用处要小得多（通过 sha512 搜索服务器，在响应 http 头中提供 sha512，...）

但是它允许并行哈希多个块，大大增加了从快速存储（NVMe、raid-0 等）的上传速度

* [浏览器上传器](https://github.com/9001/copyparty#uploading)和[命令行上传器](https://github.com/9001/copyparty/tree/hovudstraum/bin#u2cpy)现在都这样做，即使从明文 http 也允许快速上传

hashwasm 会解决流式问题，但会降低 sha512 的哈希速度（xxh128 做 6 GiB/s），并且会使旧浏览器和 [iphones](https://bugs.webkit.org/show_bug.cgi?id=228552) 不受支持

* blake2 可能是更好的选择，因为 xxh 是非加密的，但在较慢的 android 上只能达到 ~15 MiB/s

### 块大小列表

根据总文件大小强制使用特定的块大小

每对文件大小/块大小是将使用其列出的块大小的最大文件大小；512 MiB 文件将使用块大小 2 MiB，但如果文件比 512 MiB 大一个字节，那么它就变成 3 MiB

为了性能（或避开任意代理限制），可以分别使用拼接和/或子块来上传组合和/或部分块

| 文件大小           | 文件大小 | 块大小        | 块大小  |
| -----------------: | -------: | ------------: | ------: |
|        268 435 456 |  256 MiB |     1 048 576 | 1.0 MiB |
|        402 653 184 |  384 MiB |     1 572 864 | 1.5 MiB |
|        536 870 912 |  512 MiB |     2 097 152 | 2.0 MiB |
|        805 306 368 |  768 MiB |     3 145 728 | 3.0 MiB |
|      1 073 741 824 |  1.0 GiB |     4 194 304 | 4.0 MiB |
|      1 610 612 736 |  1.5 GiB |     6 291 456 | 6.0 MiB |
|      2 147 483 648 |  2.0 GiB |     8 388 608 | 8.0 MiB |
|      3 221 225 472 |  3.0 GiB |    12 582 912 |  12 MiB |
|      4 294 967 296 |  4.0 GiB |    16 777 216 |  16 MiB |
|      6 442 450 944 |  6.0 GiB |    25 165 824 |  24 MiB |
|    137 438 953 472 |  128 GiB |    33 554 432 |  32 MiB |
|    206 158 430 208 |  192 GiB |    50 331 648 |  48 MiB |
|    274 877 906 944 |  256 GiB |    67 108 864 |  64 MiB |
|    412 316 860 416 |  384 GiB |   100 663 296 |  96 MiB |
|    549 755 813 888 |  512 GiB |   134 217 728 | 128 MiB |
|    824 633 720 832 |  768 GiB |   201 326 592 | 192 MiB |
|  1 099 511 627 776 |  1.0 TiB |   268 435 456 | 256 MiB |
|  1 649 267 441 664 |  1.5 TiB |   402 653 184 | 384 MiB |
|  2 199 023 255 552 |  2.0 TiB |   536 870 912 | 512 MiB |
|  3 298 534 883 328 |  3.0 TiB |   805 306 368 | 768 MiB |
|  4 398 046 511 104 |  4.0 TiB | 1 073 741 824 | 1.0 GiB |
|  6 597 069 766 656 |  6.0 TiB | 1 610 612 736 | 1.5 GiB |
|  8 796 093 022 208 |  8.0 TiB | 2 147 483 648 | 2.0 GiB |
| 13 194 139 533 312 | 12.0 TiB | 3 221 225 472 | 3.0 GiB |
| 17 592 186 044 416 | 16.0 TiB | 4 294 967 296 | 4.0 GiB |
| 26 388 279 066 624 | 24.0 TiB | 6 442 450 944 | 6.0 GiB |
| 35 184 372 088 832 | 32.0 TiB | 8 589 934 592 | 8.0 GiB |


# 哈希密码

关于奇怪的决定

所有密码都有一个静态盐；
* 因为大多数 copyparty API 允许用户仅使用密码进行身份验证，使用户名未知，所以无法进行每个账户的盐
* 这样做的缺点是攻击者可以并行暴力破解所有账户，但是大多数 copyparty 实例首先只有少数账户，无论如何都可以通过增加哈希成本来补偿


# http api

* 表格列 `params` = URL 参数；`?foo=bar&qux=...`
* 表格列 `body` = POST 载荷
* 方法 `jPOST` = json post
* 方法 `mPOST` = multipart post
* 方法 `uPOST` = url-encoded post
* `FILE` = 传统的 HTTP 文件上传条目（rfc1867 等，`Content-Disposition` 中的文件名）

使用头部 `Cookie: cppwd=foo` 或 url 参数 `&pw=foo` 进行身份验证

## 读取

| 方法 | 参数 | 结果 |
|--|--|--|
| GET | `?dl` | 下载文件（不在浏览器中显示） |
| GET | `?ls` | 将 URL 处的文件/文件夹列为 JSON |
| GET | `?ls&dots` | 将 URL 处的文件/文件夹列为 JSON，包括点文件 |
| GET | `?ls=t` | 将 URL 处的文件/文件夹列为纯文本 |
| GET | `?ls=v` | 将 URL 处的文件/文件夹列出，终端格式 |
| GET | `?lt` | 在列表中，使用符号链接时间戳而不是目标 |
| GET | `?b` | 将 URL 处的文件/文件夹列为简化的 HTML |
| GET | `?tree=.` | 列出 URL 内一级子目录 |
| GET | `?tree` | 列出到 URL 的每一级的一级子目录 |
| GET | `?tar` | 将 URL 下的所有内容下载为 gnu-tar 文件 |
| GET | `?tar=gz:9` | ...作为 gzip-level-9 gnu-tar 文件 |
| GET | `?tar=xz:9` | ...作为 xz-level-9 gnu-tar 文件 |
| GET | `?tar=pax` | ...作为 pax-tar 文件 |
| GET | `?tar=pax,xz` | ...作为 xz-level-1 pax-tar 文件 |
| GET | `?zip` | ...作为 zip 文件 |
| GET | `?zip=dos` | ...作为 WinXP 兼容的 zip 文件 |
| GET | `?zip=crc` | ...作为 MSDOS 兼容的 zip 文件 |
| GET | `?tar&w` | 预生成 webp 缩略图 |
| GET | `?tar&j` | 预生成 jpg 缩略图 |
| GET | `?tar&p` | 预生成音频波形 |
| GET | `?shares` | 列出你的共享文件/文件夹 |
| GET | `?dls` | 显示活动下载（以管理员身份执行） |
| GET | `?ups` | 显示来自你 IP 的最近上传 |
| GET | `?ups&filter=f` | ...其中 URL 包含 `f` |
| GET | `?ru` | 显示所有最近上传 |
| GET | `?ru&filter=f` | ...其中 URL 包含 `f` |
| GET | `?ru&j` | ...作为 json |
| GET | `?mime=foo` | 指定返回 mimetype `foo` |
| GET | `?v` | 渲染 URL 处的 markdown 文件 |
| GET | `?v` | 在媒体播放器中打开图像/视频/音频 |
| GET | `?txt` | 获取 URL 处的文件作为纯文本 |
| GET | `?txt=iso-8859-1` | ...使用特定字符集 |
| GET | `?tail` | 持续流式传输增长的文件 |
| GET | `?tail=1024` | ...从字节 1024 开始 |
| GET | `?tail=-128` | ...从末尾 128 字节开始 |
| GET | `?th` | 获取 URL 处的图像/视频作为缩略图 |
| GET | `?th=opus` | 将音频文件转换为 128kbps opus |
| GET | `?th=caf` | ...在 iOS 专有容器中 |

| 方法 | 主体 | 结果 |
|--|--|--|
| jPOST | `{"q":"foo"}` | 进行服务器范围搜索；参见 `[🔎]` 搜索标签 `raw` 字段的语法 |

| 方法 | 参数 | 主体 | 结果 |
|--|--|--|--|
| jPOST | `?tar` | `["foo","bar"]` | 将 URL 内的文件夹 `foo` 和 `bar` 下载为 tar 文件 |

## 写入

| 方法 | 参数 | 结果 |
|--|--|--|
| POST | `?copy=/foo/bar` | 将 URL 处的文件/文件夹复制到 /foo/bar |
| POST | `?move=/foo/bar` | 将 URL 处的文件/文件夹移动/重命名到 /foo/bar |

| 方法 | 参数 | 主体 | 结果 |
|--|--|--|--|
| PUT | | (二进制数据) | 上传到 URL 处的文件 |
| PUT | `?j` | (二进制数据) | ...并用 json 回复 |
| PUT | `?ck` | (二进制数据) | 上传时不生成校验和（更快） |
| PUT | `?ck=md5` | (二进制数据) | 返回 md5 而不是 sha512 |
| PUT | `?gz` | (二进制数据) | 用 gzip 压缩并写入 URL 处的文件 |
| PUT | `?xz` | (二进制数据) | 用 xz 压缩并写入 URL 处的文件 |
| mPOST | | `f=FILE` | 将 `FILE` 上传到 URL 处的文件夹 |
| mPOST | `?j` | `f=FILE` | ...并用 json 回复 |
| mPOST | `?ck` | `f=FILE` | ...并禁用校验和生成（更快） |
| mPOST | `?ck=md5` | `f=FILE` | ...并返回 md5 而不是 sha512 |
| mPOST | `?replace` | `f=FILE` | ...并覆盖现有文件 |
| mPOST | `?media` | `f=FILE` | ...并返回媒体链接（不是热链接） |
| mPOST | | `act=mkdir`, `name=foo` | 在 URL 处创建目录 `foo` |
| POST | `?delete` | | 递归删除 URL |
| POST | `?eshare=rm` | | 停止共享文件/文件夹 |
| POST | `?eshare=3` | | 设置过期时间为 3 分钟 |
| jPOST | `?share` | (复杂) | 为文件/文件夹创建临时 URL |
| jPOST | `?delete` | `["/foo","/bar"]` | 递归删除 `/foo` 和 `/bar` |
| uPOST | | `msg=foo` | 将消息 `foo` 发送到服务器日志 |
| mPOST | | `act=tput`, `body=TEXT` | 覆盖 URL 处的 markdown 文档 |

上传修饰符：

| http-header | url-param | 效果 |
|--|--|--|
| `Accept: url` | `want=url` | 仅返回文件 URL |
| `Accept: json` | `want=json` | 将上传信息作为 json 返回；与 `?j` 相同 |
| `Rand: 4` | `rand=4` | 生成 4 个字符的随机文件名 |
| `Life: 30` | `life=30` | 30 秒后删除文件 |
| `CK: no` | `ck` | 禁用服务器端校验和（可能更快） |
| `CK: md5` | `ck=md5` | 返回 md5 校验和而不是 sha512 |
| `CK: sha1` | `ck=sha1` | 返回 sha1 校验和 |
| `CK: sha256` | `ck=sha256` | 返回 sha256 校验和 |
| `CK: b2` | `ck=b2` | 返回 blake2b 校验和 |
| `CK: b2s` | `ck=b2s` | 返回 blake2s 校验和 |

* `life` 只有在卷有生命周期时才有效果，并且卷生命周期必须大于文件的生命周期

* `msg` 的服务器行为可以用 `--urlform` 重新配置

## 管理

| 方法 | 参数 | 结果 |
|--|--|--|
| GET | `?reload=cfg` | 重新加载配置文件并重新扫描卷 |
| GET | `?scan` | 启动提供 URL 的卷的重新扫描 |
| GET | `?scan=/a,/b` | 启动卷 `/a` 和 `/b` 的重新扫描 |
| GET | `?stack` | 显示所有线程的堆栈跟踪 |

## 通用

| 方法 | 参数 | 结果 |
|--|--|--|
| GET | `?pw=x` | 注销 |
| GET | `?grid` | ui: 显示网格视图 |
| GET | `?imgs` | ui: 显示带缩略图的网格视图 |
| GET | `?grid=0` | ui: 显示列表视图 |
| GET | `?imgs=0` | ui: 显示列表视图 |
| GET | `?thumb` | ui, 网格模式: 显示缩略图 |
| GET | `?thumb=0` | ui, 网格模式: 显示图标 |


# 事件钩子

关于编写你自己的[钩子](../README.md#event-hooks)

## 钩子效果

钩子可以产生有意的副作用，例如将上传重定向到另一个位置，或创建+索引额外文件，或删除现有文件，通过在 stdout 上返回 json

* `reloc` 可以在上传完成前/后根据文件名、扩展名、文件内容、上传者 ip/名称等重定向上传
  * 示例：[reloc-by-ext](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/reloc-by-ext.py)
* `idx` 通知 copyparty 关于作为此上传结果要索引的新文件
  * 示例：[podcast-normalizer.py](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/podcast-normalizer.py)
* `del` 告诉 copyparty 通过 vpath 删除不相关的文件
  * 示例：(　´・ω・) nyoro~n

为了使这些生效，钩子必须用 `c1` 标志定义；参见示例 [reloc-by-ext](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/reloc-by-ext.py)

效果类型的子集可用于钩子类型的子集，

* 大多数钩子类型 (xbu/xau/xbr/xar/xbd/xad/xm) 支持所有 http 协议（up2k / basic-uploader / webdav）的 `idx` 和 `del`，但不支持 ftp/tftp/smb
* 如果给出标志 `c`，大多数钩子类型将中止/拒绝操作，如果钩子返回非零，参见示例 [reject-extension](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/reject-extension.py) 和 [reject-mimetype](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/reject-mimetype.py)
* `xbu` 支持所有 http 协议（up2k / basic-uploader / webdav）的 `reloc`，但不支持 ftp/tftp/smb
* `xau` 仅支持 basic-uploader / webdav 的 `reloc`，不支持 up2k 或 ftp/tftp/smb
  * 所以像 sharex 这样的客户端受支持，但不支持拖放到浏览器

要触发文件 `/foo/1.txt` 和 `/foo/bar/2.txt` 的索引，钩子可以 `print(json.dumps({"idx":{"vp":["/foo/1.txt","/foo/bar/2.txt"]}}))` （并将 "idx" 替换为 "del" 来删除）
* 注意：以 `/` 开头的路径是绝对 URL，但你也可以相对于每个上传文件的目标文件夹做 `../3.txt`


# 假设

## mdns

* 传出回复总是适合一个数据包
* 如果客户端提到我们的任何服务，假设它没有遗漏任何
* 总是回答所有服务，即使客户端只询问了几个
* 未实现：探测平局打破（太复杂）
* 未实现：单播监听（假设 avahi 接管了）


# sfx 重新打包

通过移除功能来减少 sfx 的大小

如果你不需要所有功能，你可以重新打包 sfx 并节省大量空间；你只需要一个 sfx 和这个仓库的副本（除了如果你在 windows 上那么你需要 msys2 或 WSL，否则不需要下载或构建其他东西）
* `393k` v1.1.3 原始 sfx.py 的大小
* `310k` 在 `./scripts/make-sfx.sh re no-cm` 之后
* `269k` 在 `./scripts/make-sfx.sh re no-cm no-hl` 之后

你可以选择丢弃的功能是
* `cm`/easymde，"花哨"的 markdown 编辑器，节省 ~89k
* `hl`，prism，语法高亮器，节省 ~41k
* `fnt`，source-code-pro，等宽字体，节省 ~9k

为了使 `re`pack 工作，首先运行其中一个 sfx 一次来解包它

**注意：** 你也可以只下载并运行 [/scripts/copyparty-repack.sh](https://github.com/9001/copyparty/blob/hovudstraum/scripts/copyparty-repack.sh) -- 这将从 github 获取最新的 copyparty 发布并进行一些重新打包；在 linux/macos 上工作（以及带有 msys2 或 WSL 的 windows）


# 构建

## 开发环境设置

由于类型提示，你需要 python 3.9 或更新版本

只有当你想要为 vscode 或类似工具设置 venv 时，才需要设置带有以下包的 venv

```sh
python3 -m venv .venv
. .venv/bin/activate
pip install jinja2 strip_hints  # 必需
pip install argon2-cffi  # 密码哈希
pip install pyzmq  # 从钩子发送 0mq
pip install mutagen  # 音频元数据
pip install pyftpdlib  # ftp 服务器
pip install partftpy  # tftp 服务器
pip install impacket  # smb 服务器 -- 如果你在 windows 上真的需要这个，请禁用 Windows Defender
pip install Pillow pillow-heif  # 缩略图
pip install pyvips  # 更快的缩略图
pip install psutil  # 在 windows 上更好地清理卡住的元数据解析器
pip install black==21.12b0 click==8.0.2 bandit pylint flake8 isort mypy  # vscode 工具
```


## 仅构建 sfx

如果你只想修改 copyparty 源代码（py/html/css/js），那么这是最简单的方法

使用以下任何示例构建 sfx：

```sh
./scripts/make-sfx.sh           # 常规版本
./scripts/make-sfx.sh fast      # 构建更快（更差的 js/css 压缩）
./scripts/make-sfx.sh gz no-cm  # gzip 压缩 + 没有花哨的 markdown 编辑器
```


## 从发布压缩包构建

使用包含的预构建 webdeps

如果你从 github 下载了[发布](https://github.com/9001/copyparty/releases)源压缩包（例如 [copyparty-1.6.15.tar.gz](https://github.com/9001/copyparty/releases/download/v1.6.15/copyparty-1.6.15.tar.gz)，所以不是自动生成的），你可以这样构建它，

```bash
python3 -m pip install --user -U build setuptools wheel jinja2 strip_hints
bash scripts/run-tests.sh python3  # 可选
python3 -m build
```

如果你无法使用 `build`，你可以使用旧的 setuptools 方法，

```bash
python3 setup.py install --user setuptools wheel jinja2
python3 setup.py build
# 你现在有一个可以安装的 wheel。或者提取并重新打包：
python3 setup.py install --skip-build --prefix=/usr --root=$HOME/pe/copyparty
```


## 从头开始构建

制作过程：

要开始，首先 `cd` 到 `scripts` 文件夹

* 第一步是 webdeps；它们最终在 `../copyparty/web/deps/` 中，例如 `../copyparty/web/deps/marked.js.gz` -- 如果你需要构建 webdeps，运行 `make -C deps-docker`
  * 这需要无根 podman 和 `podman-docker` 兼容层来伪装成 docker，尽管*应该*也可以使用有根/无根 docker
  * 如果你没有无根 podman/docker，那么 `sudo make -C deps-docker` 也可以
  * 或者，你可以完全跳过构建 webdeps，而是用 `./make-sfx.sh fast dl-wd` 从最新的 github 发布中提取编译的 webdeps

* 接下来，通过运行 `./make-sfx.sh gz fast` 构建 `copyparty-sfx.py`
  * 这是大多数剩余步骤的依赖，因为它们以 sfx 作为输入
  * 移除 `fast` 使其压缩更好
  * 也移除 `gz` 压缩得更好，但启动变慢

* 如果你想构建 `.pyz` 独立"二进制"，现在运行 `./make-pyz.sh`

* 如果你想构建用于 linux 发行版包的 `tar.gz`，现在运行 `./make-tgz-release.sh theVersionNumber`

* 如果你想构建 pypi 包，现在运行 `./make-pypi-release.sh d`

* 如果你想构建 docker 镜像，你有两个选择：
  * 如果你想使用 podman 为所有支持的架构构建所有 docker 镜像，现在运行 `(cd docker; ./make.sh hclean; ./make.sh hclean pull img)`
  * 如果你想使用 docker 为你的本机架构构建所有 docker 镜像，现在运行 `sudo make -C docker`
  * 如果你想做其他事情，请查看 `docker/make.sh` 或 `docker/Makefile` 获取灵感

* 如果你想构建 windows exe，首先拿一些零食和啤酒，[你会需要它](https://github.com/9001/copyparty/tree/hovudstraum/scripts/pyinstaller)

从头开始构建的完整构建时依赖列表如下：

* 在 ubuntu-server 上，安装 podman 或 [docker](https://get.docker.com/)，然后 `sudo apt install make zip bzip2`
  * 因为 ubuntu 是有人特别询问的 :-p


## 完整发布

也构建 sfx，所以跳过上面的 sfx 部分

*警告：`rls.sh` 尚未更新 docker 镜像和 arch/nix 打包*

完全从头开始，直接从你的本地仓库

在 `scripts` 文件夹中：

* 运行 `make -C deps-docker` 构建所有依赖
* 运行 `./rls.sh 1.2.3` 上传到 pypi + 创建 github 发布 + sfx


# 调试

## 手机上音乐播放停止

在 android 上基本正常，但仍然没有找到让 iphones 表现良好的方法

* 根据 mp.au.readyState <3 或 <4 有条件地启动/停止 mp.fau 没有帮助
* loop=true 不起作用，从 onended 手动循环 mp.fau 也不起作用（它什么都不做）
* 在计时器中分配 fau.currentTime 不起作用，因为 safari 只是假装分配它
* 在 ios 16.7.7 上，mp.fau 有时可以让一切看起来正常工作，但实际上没有音频到达扬声器

可以用 `--no-sendfile --s-wr-sz 8192 --s-wr-slp 0.3 --rsp-slp 6` 重现，然后在屏幕关闭的情况下播放一系列小音频文件，`ffmpeg -i track01.cdda.flac -c:a libopus -b:a 128k -segment_time 12 -f segment smol-%02d.opus`


## 废弃的想法

* 没有改善性能的优化尝试
  * 移除代理/多进程的东西；https://github.com/9001/copyparty/tree/no-broker
  * 减少 `HttpCli` / `httpcli.py` 中的嵌套/间接
    * 像用本地 `hsrv` 变量替换所有 `self.conn.hsrv` 这样的东西几乎没有好处
* 所有 up2k 块的单个 sha512？
  * crypto.subtle 不能流式处理，必须使用 hashwasm，昂贵
* 每个标签单独的 sqlite 表
  * 通过跳过一些索引（`+mt.k`）修复了性能
* 音频指纹
  * 只有在可以有 wasm 客户端时才有意义，而那还不存在（除了 olaf，它是 agpl，因此算作不存在）
* up2k 克隆的 `os.copy_file_range`
  * 无论如何几乎从不命中这个路径
* up2k 部分 ui
  * 感觉没有太多意义
* 在客户端缓存 sha512 块
  * 太危险 -- 被 turbo 模式超越
* 评论字段
  * 不
* 查看 android 缩略图缓存文件格式
  * 绝对不
* 用于哈希、配置启用/清除/大小的 indexedDB，2gb 可用，1g 约 9k，100m 约 4k，自动驱逐前 500k 项
  * up-ok 时空白哈希列表以跳过握手
    * 太多令人困惑的副作用
* 供其他人放入代码的 hls 框架 :^)
  * 可能不会，要考虑的东西太多 -- 寻找、从偏移开始、任务拼接（可能是 np-hard）、条件直通、速率控制（特别是多消费者）、会话保活、缓存管理...
