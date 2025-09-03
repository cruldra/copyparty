# copyparty 的替代方案

copyparty 与所有类似软件的对比分析

可能存在一些无意的偏见，请提交修正建议

目前与 [awesome-selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted) 保持同步，但可能不会持续更新


## 符号说明

### ...在功能矩阵中：
* `█` = 完全支持
* `╱` = 部分支持
* `•` = 可能支持？
* ` ` = 不支持

### ...在评测中：
* ✅ = 相对于 copyparty 的优势
  * 💾 = copyparty 提供的替代方案
* 🔵 = 相似之处
* ⚠️ = 劣势（copyparty 做得"更好"的地方）
* 🔥 = 危险/问题


## 目录

* 顶部
* [推荐方案](#推荐方案)
* [功能对比](#功能对比)
    * [通用特性](#通用特性)
    * [文件传输](#文件传输)
    * [协议和客户端支持](#协议和客户端支持)
    * [服务器配置](#服务器配置)
    * [服务器能力](#服务器能力)
    * [客户端功能](#客户端功能)
    * [集成能力](#集成能力)
    * [其他对比](#其他对比)
* [详细评测](#详细评测)
    * [copyparty](#copyparty)
    * [hfs2](#hfs2) 🔥
    * [hfs3](#hfs3)
    * [nextcloud](#nextcloud)
    * [seafile](#seafile)
    * [rclone](#rclone)
    * [dufs](#dufs)
    * [chibisafe](#chibisafe)
    * [kodbox](#kodbox)
    * [filebrowser](#filebrowser)
    * [filegator](#filegator)
    * [sftpgo](#sftpgo)
    * [arozos](#arozos)
    * [updog](#updog)
    * [goshs](#goshs)
    * [gimme-that](#gimme-that)
    * [ass](#ass)
    * [linx](#linx)
    * [h5ai](#h5ai)
    * [autoindex](#autoindex)
    * [miniserve](#miniserve)
    * [pingvin-share](#pingvin-share)
* [简要考虑](#简要考虑)
* [注释](#注释)


# 推荐方案

* [kodbox](https://github.com/kalcaddle/kodbox) ([评测](#kodbox)) 如果你不介意运行中国软件，这似乎是一个很棒的替代方案，在某些方面比 copyparty 更有优势
  * 但任何你想要共享的内容都必须移动到 kodbox 文件系统中
* [seafile](https://github.com/haiwen/seafile) ([评测](#seafile)) 和 [nextcloud](https://github.com/nextcloud/server) ([评测](#nextcloud)) 如果你需要比 copyparty 更重量级的解决方案，可能是不错的替代品
  * 但它们的 [许可证 (AGPL)](https://snyk.io/learn/agpl-license/) 比较 [棘手](https://opensource.google/documentation/reference/using/agpl-policy)
  * 而且 copyparty 在上传方面要好得多（可恢复、加速）
  * 任何你想要共享的内容都必须移动到相应的文件系统中
* [filebrowser](https://github.com/filebrowser/filebrowser) ([评测](#filebrowser)) 和 [dufs](https://github.com/sigoden/dufs) ([评测](#dufs)) 是更简单的 copyparty 替代品，但带有设置界面
  * 具有 copyparty 的一些相同优势，便携且能够处理现有的文件夹结构
  * ...但 copyparty 在上传和其他一些方面更好


# 功能对比

```
<&Kethsar> copyparty 确实很臃肿，是的
```

下面矩阵中的表头是不同的软件，在下一节中有每个软件的快速评测

软件列表：
* `a` = [copyparty](https://github.com/9001/copyparty)
* `b` = [hfs2](https://github.com/rejetto/hfs2/) 🔥
* `c` = [hfs3](https://rejetto.com/hfs/)
* `d` = [nextcloud](https://github.com/nextcloud/server)
* `e` = [seafile](https://github.com/haiwen/seafile)
* `f` = [rclone](https://github.com/rclone/rclone)，特指 `rclone serve webdav .`
* `g` = [dufs](https://github.com/sigoden/dufs)
* `h` = [chibisafe](https://github.com/chibisafe/chibisafe)
* `i` = [kodbox](https://github.com/kalcaddle/kodbox)
* `j` = [filebrowser](https://github.com/filebrowser/filebrowser)
* `k` = [filegator](https://github.com/filegator/filegator)
* `l` = [sftpgo](https://github.com/drakkan/sftpgo)
* `m` = [arozos](https://github.com/tobychui/arozos)

矩阵中未包含的软件：
* [updog](#updog)
* [goshs](#goshs)
* [gimme-that](#gimmethat)
* [ass](#ass)
* [linx](#linx)
* [h5ai](#h5ai)
* [autoindex](#autoindex)
* [miniserve](#miniserve)
* [pingvin-share](#pingvin-share)

符号说明：
* `█` = 完全支持
* `╱` = 部分支持
* `•` = 可能支持？
* ` ` = 不支持


## 通用特性

| 功能 / 软件             | a | b | c | d | e | f | g | h | i | j | k | l | m |
| ----------------------- | - | - | - | - | - | - | - | - | - | - | - | - | - |
| 直观的用户体验          |   | ╱ | █ | █ | █ |   | █ | █ | █ | █ | █ | █ | █ |
| 配置界面                |   | █ | █ | █ | █ |   |   | █ | █ | █ |   | █ | █ |
| 良好的文档              |   |   | █ | █ | █ | █ | █ |   |   | █ | █ | ╱ | ╱ |
| 在 iOS 上运行           | ╱ |   |   |   |   | ╱ |   |   |   |   |   |   |   |
| 在 Android 上运行       | █ |   | █ |   |   | █ |   |   |   |   |   |   |   |
| 在 WinXP 上运行         | █ | █ |   |   |   | █ |   |   |   |   |   |   |   |
| 在 Windows 上运行       | █ | █ | █ | █ | █ | █ | █ | ╱ | █ | █ | █ | █ | ╱ |
| 在 Linux 上运行         | █ | ╱ | █ | █ | █ | █ | █ | █ | █ | █ | █ | █ | █ |
| 在 macOS 上运行         | █ |   | █ | █ | █ | █ | █ | █ | █ | █ | █ | █ |   |
| 在 FreeBSD 上运行       | █ |   | █ | • | █ | █ | █ | • | █ | █ |   | █ |   |
| 在 Risc-V 上运行        | █ |   |   | █ | █ | █ |   | • |   | █ |   |   |   |
| 便携式二进制文件        | █ | █ | █ |   |   | █ | █ |   |   | █ |   | █ | █ |
| 零配置，即开即用        | █ | █ | █ |   |   | ╱ | █ |   |   | █ |   | ╱ | █ |
| Android 应用            | ╱ |   |   | █ | █ |   |   |   |   |   |   |   |   |
| iOS 应用                | ╱ |   |   | █ | █ |   |   |   |   |   |   |   |   |

* `零配置` = 只需启动应用程序就能获得基本可用的设置，无需安装任何软件或配置
* `a`/copyparty 备注：
  * 没有服务器设置的图形界面；只有客户端功能
  * 在 iOS/iPad 上使用 [a-Shell](https://holzschu.github.io/a-Shell_iOS/)（相当好）或 [iSH](https://ish.app/)（很慢）运行，但无法在后台运行，也无法共享所有手机存储（只能使用单独的专用文件夹）
  * [Android 应用](https://f-droid.org/en/packages/me.ocv.partyup/) 仅用于上传
  * 没有 iOS 应用，但有用于轻松上传的 [快捷指令](https://github.com/9001/copyparty#ios-shortcuts)
* `b`/hfs2 通过 wine 在 Linux 上运行
* `f`/rclone 必须使用 `rclone serve webdav .` 或类似命令启动
* `h`/chibisafe 有未记录的 Windows 支持
* `l`/sftpgo 必须使用命令启动
* `m`/arozos 有部分 Windows 支持


## 文件传输

*copyparty 真正擅长的领域*

| 功能 / 软件             | a | b | c | d | e | f | g | h | i | j | k | l | m |
| ----------------------- | - | - | - | - | - | - | - | - | - | - | - | - | - |
| 下载文件夹为 zip        | █ | █ | █ | █ | ╱ |   | █ |   | █ | █ | ╱ | █ | ╱ |
| 下载文件夹为 tar        | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 上传                    | █ | █ | █ | █ | █ | █ | █ | █ | █ | █ | ╱ | █ | █ |
| 并行上传                | █ |   |   | █ | █ |   | • |   | █ | █ | █ |   | █ |
| 断点续传上传            | █ |   | █ |   |   |   |   |   | █ | █ | █ | ╱ |   |
| 上传分片                | █ |   | █ | █ |   |   |   | █ | █ | █ | █ | ╱ | █ |
| 上传加速                | █ |   |   |   |   |   |   |   | █ |   | █ |   |   |
| 上传验证                | █ |   |   | █ | █ |   |   |   | █ |   |   |   |   |
| 上传去重                | █ |   |   |   | █ |   |   |   | █ |   |   |   |   |
| 上传 999 TiB 文件       | █ |   |   |   | █ | █ | • |   | █ |   | █ | ╱ | ╱ |
| 从设备 CTRL-V           | █ |   |   | █ |   |   |   |   |   |   |   |   |   |
| 竞速传输（"p2p"）       | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| "tail -f" 流式传输      | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 保持最后修改时间        | █ |   | █ | █ | █ | █ |   |   |   |   |   | █ |   |
| 上传规则                | ╱ | ╱ | ╱ | ╱ | ╱ |   |   | ╱ | ╱ |   | ╱ | ╱ | ╱ |
| ┗ 最大磁盘使用量        | █ | █ | █ |   | █ |   |   |   | █ |   |   | █ | █ |
| ┗ 最大文件大小          | █ |   |   |   |   |   |   | █ |   |   | █ | █ | █ |
| ┗ 文件夹最大项目数      | █ |   |   |   |   |   |   |   |   |   |   | ╱ |   |
| ┗ 最大文件年龄          | █ |   |   |   |   |   |   |   | █ |   |   |   |   |
| ┗ 时间段内最大上传量    | █ |   |   |   |   |   |   |   |   |   |   | ╱ |   |
| ┗ 写入前压缩            | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| ┗ 随机化文件名          | █ |   |   |   |   |   |   | █ | █ |   |   |   |   |
| ┗ MIME类型拒绝列表      | ╱ |   |   |   |   |   |   |   | • | ╱ |   | ╱ | • |
| ┗ 扩展名拒绝列表        | ╱ |   |   |   |   |   |   | █ | • | ╱ |   | ╱ | • |
| ┗ 上传路由              | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 提供校验和              |   |   |   | █ | █ |   |   |   | █ | ╱ |   |   |   |
| 云存储后端              | ╱ | ╱ | ╱ | █ | █ | █ | ╱ |   |   | ╱ | █ | █ | ╱ |

* `上传分片` = 文件被切分成块，使得在 Cloudflare 等平台上可以上传超过 100 MiB 的文件

* `上传加速` = 每个文件可以使用多个 TCP 连接上传，在长距离/不稳定连接上可以提供巨大的速度提升 -- 就像以前的 [下载加速器](https://en.wikipedia.org/wiki/GetRight) 的反向版本

* `上传验证` = 上传的文件会进行校验和或其他方式的正确性确认

* `从设备 CTRL-V` = 在 Windows 资源管理器（或其他）中按 CTRL-C，然后粘贴到网页浏览器中上传

* `竞速传输` = 文件可以在仍在上传时被下载；下载者的速度会被减慢，以确保上传者始终领先

* `tail -f` = 查看或下载日志文件时，连接可以保持打开状态，实时显示新添加的行

* `上传路由` = 根据文件类型/内容/上传者等，文件可以被重定向到另一个位置或进行其他转换；缓解诸如 [sharex#3992](https://github.com/ShareX/ShareX/issues/3992) 等限制
  * copyparty 示例：[reloc-by-ext](https://github.com/9001/copyparty/tree/hovudstraum/bin/hooks#before-upload)

* `提供校验和` = 从服务器下载文件时，提供文件的校验和用于客户端验证

* `云存储后端` = 能够从（并写入）S3 或类似的云服务提供文件；`╱` 表示软件可以通过 `rclone mount` 作为桥梁来实现

* `a`/copyparty 可以拒绝上传的文件（基于复杂条件），例如 [按扩展名](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/reject-extension.py) 或 [MIME类型](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/reject-mimetype.py)
* `e`/seafile 下载为zip不是流式的；它在下载开始前创建完整的zip文件，大文件夹会失败
* `j`/filebrowser 备注：
  * 可以按需为单个文件提供校验和
  * 可能可以像 copyparty 一样进行扩展名/MIME类型拒绝
* `k`/filegator 下载为zip不是流式的；它在下载开始前创建完整的zip文件
* `l`/sftpgo：
  * 断点续传/分片上传仅在 SFTP 上支持，HTTP 不支持
  * 上传规则仅是总量，不是时间段内的
  * 可能可以像 copyparty 一样进行扩展名/MIME类型拒绝
* `m`/arozos 下载为zip不是流式的；它在下载开始前创建完整的zip文件，大文件夹会失败


## 协议和客户端支持

| 功能 / 软件             | a | b | c | d | e | f | g | h | i | j | k | l | m |
| ----------------------- | - | - | - | - | - | - | - | - | - | - | - | - | - |
| 提供 HTTPS              | █ |   | █ | █ | █ | █ | █ | █ | █ | █ | █ | █ | █ |
| 提供 WebDAV             | █ |   |   | █ | █ | █ | █ |   | █ |   |   | █ | █ |
| 提供 FTP (TCP)          | █ |   |   |   |   | █ |   |   |   |   |   | █ | █ |
| 提供 FTPS (TLS)         | █ |   |   |   |   | █ |   |   |   |   |   | █ |   |
| 提供 TFTP (UDP)         | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 提供 SFTP (SSH)         |   |   |   |   |   | █ |   |   |   |   |   | █ | █ |
| 提供 SMB/CIFS           | ╱ |   |   |   |   | █ |   |   |   |   |   |   |   |
| 提供 DLNA               |   |   |   |   |   | █ |   |   |   |   |   |   |   |
| 监听 Unix 套接字        | █ |   |   | █ | █ |   | █ | █ | █ | █ | █ | █ |   |
| Zeroconf                | █ |   |   |   |   |   |   |   |   |   |   |   | █ |
| 支持 Netscape 4         | ╱ |   |   |   |   | █ |   |   |   |   | • |   | ╱ |
| ...Internet Explorer 6  | ╱ | █ |   | █ |   | █ |   |   |   |   | • |   | ╱ |
| 乱码文件名              | █ |   |   | • | • | █ | █ | • | █ | • |   | ╱ |   |
| 无法解码的文件名        | █ |   |   | • | • | █ |   | • |   |   |   | ╱ |   |

* `WebDAV` = 便于将远程服务器挂载为本地文件系统的协议；参见 zeroconf：
* `Zeroconf` = 服务器在局域网上宣告自己，[自动出现](https://user-images.githubusercontent.com/241032/215344737-0eae8d98-9496-4256-9aa8-cd2f6971810d.png) 在其他支持 zeroconf 的设备上
* `乱码文件名` = 使用错误编解码器解码然后重新编码的文件名（通常是 utf-8），所以 `宇多田ヒカル` 可能看起来像 `ëFæ╜ôcâqâJâï`
* `无法解码的文件名` = 无法解析为 utf-8 的纯二进制垃圾
  * 你可以通过 rclone 挂载远程 copyparty 服务器成功播放 `$'\355\221'`，很棒
* `a`/copyparty 备注：
  * 极简的 samba/cifs 服务器
  * Netscape 4 / IE6 支持主要是作为笑话列出的，尽管有些人确实发现它有用（[IE4 也行](https://user-images.githubusercontent.com/241032/118192791-fb31fe00-b446-11eb-9647-898ea8efc1f7.png)）
* `l`/sftpgo 将乱码文件名转换为有效的 utf-8（信息丢失）
* `m`/arozos 对旧浏览器有只读支持；无上传功能


## 服务器配置

| 功能 / 软件             | a | b | c | d | e | f | g | h | i | j | k | l | m |
| ----------------------- | - | - | - | - | - | - | - | - | - | - | - | - | - |
| 命令行参数配置          | █ |   | █ |   |   | █ | █ |   |   | █ |   | ╱ | ╱ |
| 配置文件                | █ | █ | █ | ╱ | ╱ | █ |   | █ |   | █ | • | ╱ | ╱ |
| 运行时配置重载          | █ | █ | █ |   |   |   |   | █ | █ | █ | █ |   | █ |
| 同端口 HTTP / HTTPS     | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 监听多个端口            | █ |   |   |   |   |   |   |   |   |   |   | █ |   |
| 虚拟文件系统            | █ | █ | █ |   |   |   | █ |   |   |   |   | █ |   |
| 反向代理兼容            | █ |   | █ | █ | █ | █ | █ | █ | • | • | • | █ | ╱ |
| 文件夹反向代理兼容      | █ |   | █ |   | █ | █ |   | • | • | █ | • |   | • |

* `文件夹反向代理` = 反向代理时不需要专用的整个（子）域名，而是使用子文件夹
* `l`/sftpgo：
  * 配置：用户必须通过 GUI / API 调用添加
* `m`/arozos：
  * 配置主要通过 GUI 进行
  * 反向代理不保证看到正确的客户端 IP


## 服务器能力

| 功能 / 软件             | a | b | c | d | e | f | g | h | i | j | k | l | m |
| ----------------------- | - | - | - | - | - | - | - | - | - | - | - | - | - |
| 账户系统                | █ | █ | █ | █ | █ | █ | █ | █ | █ | █ | █ | █ | █ |
| 每账户 chroot           |   |   |   |   |   |   |   |   |   |   |   | █ |   |
| 单点登录                | ╱ |   |   | █ | █ |   |   |   | • |   |   |   |   |
| 令牌认证                | ╱ |   |   | █ | █ |   |   | █ |   |   |   |   | █ |
| 双因素认证              | ╱ |   | ╱ | █ | █ |   |   |   |   |   |   | █ | ╱ |
| 每卷权限                | █ | █ | █ | █ | █ | █ | █ |   | █ | █ | ╱ | █ | █ |
| 每文件夹权限            | ╱ |   | █ | █ | █ |   | █ |   | █ | █ | ╱ | █ | █ |
| 每文件权限              |   |   | █ | █ | █ |   | █ |   | █ |   |   |   | █ |
| 每文件密码              | █ |   |   | █ | █ |   | █ |   | █ |   |   |   | █ |
| 取消映射子文件夹        | █ |   | █ |   |   |   | █ |   |   | █ | ╱ | • |   |
| index.html 阻止列表     | ╱ |   |   |   |   |   | █ |   |   | • |   |   |   |
| 只写文件夹              | █ |   | █ |   | █ |   |   |   |   |   | █ | █ |   |
| 文件按原样存储          | █ | █ | █ | █ |   | █ | █ |   |   | █ | █ | █ | █ |
| 文件版本控制            |   |   |   | █ | █ |   |   |   |   |   |   |   |   |
| 文件加密                |   |   |   | █ | █ | █ |   |   |   |   |   | █ |   |
| 文件索引                | █ |   | █ | █ | █ |   |   | █ | █ | █ |   |   |   |
| ┗ 每卷数据库            | █ |   | • | • | • |   |   | • | • |   |   |   |   |
| ┗ 数据库存储在文件夹中  | █ |   |   |   |   |   |   | • | • | █ |   |   |   |
| ┗ 数据库存储在树外      | █ |   | █ | █ | █ |   |   | • | • | █ |   |   |   |
| ┗ 现有文件树            | █ |   | █ |   |   |   |   |   |   | █ |   |   |   |
| 文件操作事件钩子        | █ |   |   |   |   |   |   |   |   | █ |   | █ | • |
| 单向文件夹同步          | █ |   |   | █ | █ | █ |   |   |   |   |   |   |   |
| 完全同步                |   |   |   | █ | █ |   |   |   |   |   |   |   |   |
| 速度限制                |   | █ | █ |   |   | █ |   |   | █ |   |   | █ |   |
| 防暴力破解              | █ | █ | █ | █ | █ |   |   |   | • |   |   | █ | • |
| 动态DNS更新器           |   | █ | █ |   |   |   |   |   |   |   |   |   |   |
| 自动更新器              |   |   | █ |   |   |   |   |   |   |   |   |   | █ |
| 日志轮转                | █ |   | █ | █ | █ |   |   | • | █ |   |   | █ | • |
| 上传跟踪/日志           | █ | █ | • | █ | █ |   |   | █ | █ |   |   | ╱ | █ |
| Prometheus 指标         | █ |   |   | █ |   |   |   |   |   |   |   | █ |   |
| curl 友好的 ls          | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| curl 友好的上传         | █ |   | █ |   |   | █ | █ | • |   |   |   |   |   |

* `取消映射子文件夹` = "遮蔽"；在现有文件系统树中间挂载本地文件夹，以禁用对该路径下方的访问
* `文件按原样存储` = 上传的文件可以从服务器硬盘上轻松读取，不会被切分成块或放在奇怪的文件夹结构中
* `数据库存储在文件夹中` = 文件系统索引可以写入文件夹本身内的数据库文件
* `数据库存储在树外` = 文件系统索引可以存储在其他地方，不一定在共享文件夹内
* `现有文件树` = 会索引找到的任何现有文件
* `文件操作事件钩子` = 在上传、移动、重命名等之前/之后运行脚本
* `单向文件夹同步` = 类似 rsync，可选择删除目标处的意外文件
* `完全同步` = 有状态的，类似 Dropbox 的同步
* `速度限制` = 速率限制（每 IP、每用户、每连接等）
* `curl 友好的 ls` = 当使用 curl 时返回 [可排序的纯文本文件夹列表](https://user-images.githubusercontent.com/241032/215322619-ea5fd606-3654-40ad-94ee-2bc058647bb2.png)
* `curl 友好的上传` = 使用 curl 上传就是 `curl -T some.bin http://.../`
* `a`/copyparty 备注：
  * 单点登录、令牌认证和双因素认证可以通过 authelia/authentik 或类似系统实现，但还没有人制作示例
  * 从本地到服务器的单向文件夹同步可以通过 [u2c.py](https://github.com/9001/copyparty/tree/hovudstraum/bin#u2cpy) 高效完成，或者使用 WebDAV 和传统的 rsync
  * 可以热重载配置文件（只有少数例外）
  * 如果将文件夹制作成单独的卷，可以设置每文件夹权限，但有配置开销
  * `index.html` 本身不会阻止目录列表，但权限 `h`（而不是 `r`）强制返回 index.html 而不是文件夹内容
  * [事件钩子](https://github.com/9001/copyparty/tree/hovudstraum/bin/hooks) ([Discord](https://user-images.githubusercontent.com/241032/215304439-1c1cb3c8-ec6f-4c17-9f27-81f969b1811a.png), [桌面](https://user-images.githubusercontent.com/241032/215335767-9c91ed24-d36e-4b6b-9766-fb95d12d163f.png)) 受 filebrowser 启发，以及更复杂的 [媒体解析器](https://github.com/9001/copyparty/tree/hovudstraum/bin/mtag) 替代方案
  * 上传历史可以使用 [partyjournal](https://github.com/9001/copyparty/blob/hovudstraum/bin/partyjournal.py) 可视化
* `k`/filegator 备注：
  * `每* 权限` -- 可以将用户限制在一个文件夹及其子文件夹
  * `取消映射子文件夹` -- 可以全局过滤路径列表
* `l`/sftpgo：
  * `文件操作事件钩子` 也包括下载触发器
  * `上传跟踪/日志` 在主日志文件中
* `m`/arozos：
  * `双因素认证` 可能通过 LDAP/OAuth 实现
* `c`/hfs3
  * `双因素认证` 通过安装插件可用


## 客户端功能

| 功能 / 软件             | a | b | c | d | e | f | g | h | i | j | k | l | m |
| ----------------------- | - | - | - | - | - | - | - | - | - | - | - | - | - |
| 单页应用                | █ |   | █ | █ | █ |   |   | █ | █ | █ | █ |   | █ |
| 主题                    | █ | █ | █ | █ |   |   |   |   | █ |   |   |   |   |
| 目录树导航              | █ | ╱ |   |   | █ |   |   |   | █ |   | ╱ |   |   |
| 多列排序                | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 缩略图                  | █ |   | ╱ | ╱ | ╱ |   |   | █ | █ | ╱ |   |   | █ |
| ┗ 图片缩略图            | █ |   | ╱ | █ | █ |   |   | █ | █ | █ |   |   | █ |
| ┗ 视频缩略图            | █ |   |   | █ | █ |   |   |   | █ |   |   |   | █ |
| ┗ 音频频谱图            | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 音频播放器              | █ |   | ╱ | █ | █ |   |   |   | █ | ╱ |   |   | █ |
| ┗ 无缝播放              | █ |   |   |   |   |   |   |   | • |   |   |   |   |
| ┗ 音频均衡器            | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| ┗ 波形搜索栏            | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| ┗ 操作系统集成          | █ |   | █ |   |   |   |   |   |   |   |   |   |   |
| ┗ 转码为有损格式        | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 视频播放器              | █ |   | █ | █ | █ |   |   |   | █ | █ |   |   | █ |
| ┗ 视频转码              |   |   | ╱ |   |   |   |   |   | █ |   |   |   |   |
| 音频 BPM 检测器         | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 音频调性检测器          | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 按路径/名称搜索         | █ | █ | █ | █ | █ |   | █ |   | █ | █ | ╱ |   |   |
| 按日期/大小搜索         | █ |   |   |   | █ |   |   | █ | █ |   |   |   |   |
| 按 BPM/调性搜索         | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 按自定义标签搜索        |   |   |   |   |   |   |   | █ | █ |   |   |   |   |
| 搜索文件内容            |   |   |   | █ | █ |   |   |   | █ |   |   |   |   |
| 按自定义解析器搜索      | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 查找本地文件            | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 撤销最近上传            | █ |   |   |   |   |   |   |   |   |   |   |   |   |
| 创建目录                | █ |   | █ | █ | █ | ╱ | █ | █ | █ | █ | █ | █ | █ |
| 图片查看器              | █ |   | █ | █ | █ |   |   |   | █ | █ | █ |   | █ |
| Markdown 查看器         | █ |   | ╱ |   | █ |   |   |   | █ | ╱ | ╱ |   | █ |
| Markdown 编辑器         | █ |   |   |   | █ |   |   |   | █ | ╱ | ╱ |   | █ |
| 列表中的 readme.md      | █ |   | ╱ | █ |   |   |   |   |   |   |   |   |   |
| 重命名文件              | █ | █ | █ | █ | █ | ╱ | █ |   | █ | █ | █ | █ | █ |
| 批量重命名              | █ |   |   |   |   |   |   |   | █ |   |   |   |   |
| 剪切/粘贴文件           | █ | █ | █ | █ | █ |   |   |   | █ |   |   |   | █ |
| 移动文件                | █ | █ | █ | █ | █ |   | █ |   | █ | █ | █ |   | █ |
| 删除文件                | █ | █ | █ | █ | █ | ╱ | █ | █ | █ | █ | █ | █ | █ |
| 复制文件                |   |   | ╱ |   | █ |   |   |   | █ | █ | █ |   | █ |

* `单页应用` = 多任务处理；可以在上传时继续导航
* `音频播放器 » 操作系统集成` = 使用 [锁屏](https://user-images.githubusercontent.com/241032/142711926-0700be6c-3e31-47b3-9928-53722221f722.png) 或 [媒体热键](https://user-images.githubusercontent.com/241032/215347492-b4250797-6c90-4e09-9a4c-721edf2fb15c.png) 来播放/暂停、上一首/下一首歌曲
* `按自定义标签搜索` = 通过 UI 为文件添加标签并按这些标签搜索的能力
* `查找本地文件` = 将文件拖入浏览器以查看服务器上是否存在
* `撤销最近上传` = 没有删除权限的账户有一个时间窗口可以撤销自己的上传
* `a`/copyparty 播放无缝专辑时有微小的跳跃，取决于音频编解码器（opus 最佳）
* `b`/hfs2 有一个非常基本的目录树视图，不显示兄弟文件夹
* `f`/rclone 通过 WebDAV 托管时可以进行一些文件管理（mkdir、重命名、删除）
* `j`/filebrowser 备注：
  * 音频播放不会继续到下一首歌曲
  * 纯文本查看器/编辑器
* `k`/filegator 目录树是一个模态窗口


## 集成能力

| 功能 / 软件             | a | b | c | d | e | f | g | h | i | j | k | l | m |
| ----------------------- | - | - | - | - | - | - | - | - | - | - | - | - | - |
| 上传时操作系统提醒      | ╱ |   |   |   |   |   |   |   |   | ╱ |   | ╱ |   |
| Discord                 | ╱ |   |   |   |   |   |   |   |   | ╱ |   | ╱ |   |
| ┗ 宣告上传              | ╱ |   |   |   |   |   |   |   |   |   |   | ╱ |   |
| ┗ 自定义嵌入            |   |   |   |   |   |   |   |   |   |   |   | ╱ |   |
| ShareX                  | █ |   |   | █ |   | █ | ╱ | █ |   |   |   |   |   |
| Flameshot               |   |   |   |   |   | █ |   |   |   |   |   |   |   |

* ShareX `╱` = 支持，但不提供示例 ShareX 配置
* `a`/copyparty 备注：
  * `上传时操作系统提醒` 作为 [插件](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/notify.py) 可用
  * `Discord » 宣告上传` 作为 [插件](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/discord-announce.py) 可用
* `j`/filebrowser 可能可以通过类似 copyparty 的命令运行器实现这些功能
* `l`/sftpgo 没有内置功能但非常可扩展


## 其他对比

| 软件 / 功能 | 语言   | 许可证 | 大小   |
| ----------- | ------ | ------ | ------ |
| copyparty   | Python | █ MIT  | 0.6 MB |
| hfs2        | Delphi | ░ GPL3 |   2 MB |
| hfs3        | TS     | ░ GPL3 |  36 MB |
| nextcloud   | PHP    | ‼ AGPL |    •   |
| seafile     | C      | ‼ AGPL |    •   |
| rclone      | Go     | █ MIT  |  45 MB |
| dufs        | Rust   | █ APL2 | 2.5 MB |
| chibisafe   | TS     | █ MIT  |    •   |
| kodbox      | PHP    | ░ GPL3 |  92 MB |
| filebrowser | Go     | █ APL2 |  20 MB |
| filegator   | PHP    | █ MIT  |    •   |
| sftpgo      | Go     | ‼ AGPL |  44 MB |
| arozos      | Go     | ░ GPL3 | 531 MB |
| updog       | Python | █ MIT  |  17 MB |
| goshs       | Go     | █ MIT  |  11 MB |
| gimme-that  | Python | █ MIT  | 4.8 MB |
| ass         | TS     | █ ISC  |    •   |
| linx        | Go     | ░ GPL3 |  20 MB |
| h5ai        | PHP    | █ MIT  |    •   |
| autoindex   | Go     | █ MPL2 |  11 MB |
| miniserve   | Rust   | █ MIT  |   2 MB |
| pingvin     | Go     | █ BSD2 | 487 MB |

* `大小` = 二进制文件（如果可用）或程序及其依赖项的安装大小
  * copyparty 大小是 [独立 Python](https://github.com/9001/copyparty/releases/latest/download/copyparty-sfx.py) 文件的大小；[Windows exe](https://github.com/9001/copyparty/releases/latest/download/copyparty.exe) 是 **6 MiB**


# 详细评测

* ✅ 是相对于 copyparty 的优势
  * 💾 是 copyparty 提供的替代方案
* 🔵 是相似之处
* ⚠️ 是劣势（copyparty 做得"更好"的地方）
* 🔥 是危险/问题

## [copyparty](https://github.com/9001/copyparty)
* 可恢复的上传，服务器端验证
* 上传分片允许在某些连接上实现更快的上传速度，即使在 Cloudflare 上也能处理 TB 级文件
  * 以上两个功能都是令人惊讶的罕见特性
* 非常跨平台（Python，无依赖）

## [hfs2](https://github.com/rejetto/hfs2/)
* 传奇的原版（现在被 [hfs3](#hfs3) 取代）
* 🔥 hfs2 已死且危险！未修复的 RCE：[信息](https://github.com/rejetto/hfs2/issues/44)，[信息](https://github.com/drapid/hfs/issues/3)，[信息](https://asec.ahnlab.com/en/67650/)
* ⚠️ 上传不可恢复/加速/完整性检查
  * ⚠️ 在 Cloudflare 上：最大上传大小 100 MiB
* ⚠️ 仅限 Windows
* ✅ 配置 GUI
* 带 GUI 配置的虚拟文件系统，每卷权限
* 开始显示其年龄，因此重写：

## [hfs3](https://rejetto.com/hfs/)
* Node.js；跨平台
* 带 GUI 配置的虚拟文件系统，每卷权限
* 本地测试，ArchLinux 上的 v0.53.2
* 🔵 上传可恢复
* ⚠️ 上传不加速（copyparty 跨大西洋快 3 倍）
* ⚠️ 上传不进行完整性检查
* ⚠️ 上传小文件还可以；`107` 文件/秒（copyparty 做 `670`/秒，快 6 倍）
* ⚠️ 不支持奇怪的文件名
* ✅ 配置 GUI
* ✅ 下载计数器
* ✅ 监视活动连接
* ✅ 插件

## [nextcloud](https://github.com/nextcloud/server)
* PHP，MariaDB
* 本地测试，[linuxserver/nextcloud](https://hub.docker.com/r/linuxserver/nextcloud) v30.0.2（SQLite）
* ⚠️ [隔离的磁盘文件层次结构] 在每用户文件夹中
  * 不算太糟，可能可以通过绑定挂载或符号链接解决
* ⚠️ 上传不可恢复/加速/完整性检查
  * 🔵 上传是分片的；即使在 Cloudflare 上也没有文件大小限制
* ⚠️ 上传小文件很慢；`4` 文件/秒（copyparty 做 `670`/秒，快 160 倍）
* ⚠️ 没有只写/仅上传文件夹
* ⚠️ 仅 HTTP/WebDAV；没有 FTP、zeroconf
* ⚠️ 音乐播放器不够出色
* ⚠️ 不能在 Android 或 iPad 上运行
* ⚠️ AGPL 许可
* ✅ 出色的 UI/UX
* ✅ 配置 GUI
* ✅ 应用（Android / iPhone）
  * 💾 Android 仅上传应用 + iPhone 上传快捷指令
* ✅ 更细粒度的权限（每文件）
* ✅ 搜索：文件内容的全文索引
* ✅ WebAuthn 无密码认证

## [seafile](https://github.com/haiwen/seafile)
* C，MariaDB
* 本地测试，[官方容器](https://manual.seafile.com/latest/docker/deploy_seafile_with_docker/) v11.0.13
* ⚠️ [隔离的磁盘文件层次结构](https://manual.seafile.com/maintain/seafile_fsck/)，与其他软件不兼容
  * *在这方面比 Nextcloud 更糟*
* ⚠️ 上传不可恢复/加速/完整性检查
  * ⚠️ 在 Cloudflare 上：最大上传大小 100 MiB
* ⚠️ 上传小文件很慢；`4.7` 文件/秒（copyparty 做 `670`/秒，快 140 倍）
* ⚠️ 大文件夹无法 zip 下载
* ⚠️ 仅 HTTP/WebDAV；没有 FTP、zeroconf
* ⚠️ 音乐播放器不够出色
* ⚠️ 不能在 Android 或 iPad 上运行
* ⚠️ AGPL 许可
* ✅ 出色的 UI/UX
* ✅ 配置 GUI
* ✅ 应用（Android / iPhone）
  * 💾 Android 仅上传应用 + iPhone 上传快捷指令
* ✅ 更细粒度的权限（每文件）
* ✅ 搜索：文件内容的全文索引

## [rclone](https://github.com/rclone/rclone)
* 优秀的独立 C 程序
* ⚠️ 上传不可恢复/加速/完整性检查
  * ⚠️ 在 Cloudflare 上：最大上传大小 100 MiB
* ⚠️ 没有 Web UI，只是服务器/下载器/上传器实用程序
* ✅ 适用于几乎任何协议、云提供商
  * ⚠️ copyparty 的 WebDAV 服务器稍快

## [dufs](https://github.com/sigoden/dufs)
* Rust；跨平台（Windows、Linux、macOS）
* 本地测试，ArchLinux 上的 v0.43.0（纯二进制）
* ⚠️ 上传不可恢复/加速/完整性检查
  * ⚠️ 在 Cloudflare 上：最大上传大小 100 MiB
  * ⚠️ 跨大西洋，copyparty 快 3 倍
* ⚠️ 上传小文件还可以；`97` 文件/秒（copyparty 做 `670`/秒，快 7 倍）
* ⚠️ 不支持奇怪的文件名
* ✅ 每 URL 访问控制（copyparty 是每卷）
* 🔵 基本但非常快速的 UI
* 🔵 上传、重命名、删除...见功能矩阵

## [chibisafe](https://github.com/chibisafe/chibisafe)
* Node.js；推荐 Docker
* 🔵 *它有上传分片！*
  * ⚠️ 但上传仍然不可恢复/加速/完整性检查
* ⚠️ 不便携
* ⚠️ 隔离的磁盘文件层次结构，与其他软件不兼容
* ⚠️ 仅 HTTP/WebDAV；没有 FTP 或 zeroconf
* ✅ 漂亮的 UI
* ✅ 服务器设置和用户管理的控制面板
* ✅ 用户注册
* ✅ 可搜索的图片标签；按标签删除
* ✅ 浏览器扩展，将文件上传到服务器
* ✅ 按文件扩展名拒绝上传
  * 💾 可以使用插件按 [扩展名](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/reject-extension.py) 或 [MIME类型](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/reject-mimetype.py) 拒绝上传
* ✅ 令牌认证（API 密钥）

## [kodbox](https://github.com/kalcaddle/kodbox)
* 这东西很疯狂（但正在受到 [arozos](#arozos) 的竞争）
* PHP；[Docker](https://hub.docker.com/r/kodcloud/kodbox)
* 🔵 *上传分片、加速和完整性检查！*
  * ⚠️ 但上传不可恢复（？）
* ⚠️ 不便携
* ⚠️ 隔离的磁盘文件层次结构，与其他软件不兼容
* ⚠️ 上传小文件到 copyparty 快 16 倍
* ⚠️ 上传大文件到 copyparty 快 3 倍
* ⚠️ 仅 HTTP/WebDAV；没有 FTP 或 zeroconf
* ⚠️ GUI 的某些部分是中文
* ✅ 出色的 UI/UX
* ✅ 服务器设置和用户管理的控制面板
* ✅ 文件标签；文件讨论！？
* ✅ 视频转码
* ✅ 解压上传的档案
* ✅ 带语法高亮的 IDE
* ✅ OpenOffice 文件的所见即所得编辑器

## [filebrowser](https://github.com/filebrowser/filebrowser)
* Go；跨平台（Windows、Linux、Mac）
* 本地测试，ArchLinux 上的 v2.31.2（纯二进制）
* 🔵 上传可恢复且分片
* 🔵 多个文件并行上传，但...
  * ⚠️ 大文件不加速（copyparty 跨大西洋快 5 倍）
* ⚠️ 上传不进行完整性检查
* ⚠️ 上传小文件还可以；`69` 文件/秒（copyparty 做 `670`/秒，快 9 倍）
* ⚠️ 仅 HTTP；没有 WebDAV / FTP / zeroconf
* ⚠️ 不支持奇怪的文件名
* ⚠️ 没有目录树导航
* ⚠️ 有限的文件搜索
* ✅ 设置 GUI
* ✅ 良好的 UI/UX
  * ⚠️ 但没有用于导航的目录树
* ✅ 用户注册
* ✅ 命令运行器/远程 shell
* ✅ 更高效；可以处理大约两倍的同时流量
* 注意：关注 [gtsteffaniak 的分支](https://github.com/gtsteffaniak/filebrowser)

## [filegator](https://github.com/filegator/filegator)
* PHP；跨平台（Windows、Linux、Mac）
* 🔵 *它有上传分片和加速*
  * ⚠️ 但上传仍然不进行完整性检查
  * ⚠️ 在 copyparty 上，上传快 40 倍
    * 与可能很糟糕的官方 filegator Docker 示例相比
* ⚠️ 仅 HTTP；没有 WebDAV / FTP / zeroconf
* ⚠️ 不支持符号链接
* ⚠️ 昂贵的下载为zip功能
* ⚠️ 不支持奇怪的文件名
* ⚠️ 有限的文件搜索

## [sftpgo](https://github.com/drakkan/sftpgo)
* Go；跨平台（Windows、Linux、Mac）
* ⚠️ HTTP 上传不可恢复/加速/完整性检查
  * ⚠️ 在 Cloudflare 上：最大上传大小 100 MiB
  * ⚠️ 跨大西洋，copyparty 快 2.5 倍
  * 🔵 SFTP 上传可恢复
* ⚠️ Web UI 非常简陋且有点慢
  * ⚠️ 没有缩略图/图片查看器/音频播放器
  * ⚠️ 基本文件管理器（没有剪切/粘贴/移动）
* ⚠️ 没有文件系统索引/搜索
* ⚠️ 不能在手机、平板上运行
* ⚠️ 没有 zeroconf（mDNS/SSDP）
* ⚠️ 不实用的目录 URL
* ⚠️ AGPL 许可
* 🔵 上传小文件很快；`340` 文件/秒（copyparty 做 `670`/秒）
* 🔵 FTP、FTPS、WebDAV
* ✅ SFTP 服务器
* ✅ 设置 GUI
* ✅ ACME（自动 TLS 证书）
  * 💾 依赖 Caddy/Certbot/acme.sh
* ✅ 静态加密
  * 💾 依赖 LUKS/BitLocker
* ✅ 可以使用 S3/GCS 作为存储后端
  * 💾 依赖 rclone-mount
* ✅ 下载时事件钩子（其他方面与 copyparty 相同）
* ✅ 更广泛的权限控制

## [arozos](https://github.com/tobychui/arozos)
* 类似 [kodbox](#kodbox) 的大型应用套件，copyparty 在下载/上传/音乐/索引方面更好，但 arozos 有其他优势
* Go；主要是 Linux（Windows 支持有限）
* ⚠️ 需要 root
* ⚠️ 上传不可恢复/完整性检查
* ⚠️ 上传小文件到 copyparty 快 2.7 倍
* ⚠️ 上传大文件到 copyparty 至少快 10%
  * arozos 基于 WebSocket，512 KiB 块；将每个块写入单独的文件然后合并
  * copyparty 直接拼接到最终文件；对硬盘和文件系统更快更好
* ⚠️ 跨大西洋，上传到 copyparty 快 6 倍
* ⚠️ 没有目录树导航面板；不那么容易导航
* ⚠️ 下载为zip不是流式的；在服务器上创建临时文件
* ⚠️ 不是自包含的（从 jsdelivr 拉取）
* ⚠️ 有音频播放器，但支持的文件类型较少
* ⚠️ 配置真实 IP 检测的支持有限
* ✅ SFTP 服务器
* ✅ 设置 GUI
* ✅ 好看的 GUI
* ✅ IDE、MS Office 查看器、丰富的主机集成等等

## [updog](https://github.com/sc0tfree/updog)
* Python；跨平台
* 带上传功能的基本目录列表
* ⚠️ 便携性较差
* ⚠️ 上传不可恢复/加速/完整性检查
  * ⚠️ 在 Cloudflare 上：最大上传大小 100 MiB
* ⚠️ 没有虚拟文件系统；单文件夹，单账户

## [goshs](https://github.com/patrickhener/goshs)
* Go；跨平台（Windows、Linux、Mac）
* ⚠️ 没有虚拟文件系统；单文件夹，单账户
* ⚠️ 上传不可恢复/加速/完整性检查
  * ⚠️ 在 Cloudflare 上：最大上传大小 100 MiB
* ✅ 酷炫的剪贴板小部件
  * 💾 Markdown 编辑器是一个不错的替代品
* 🔵 只读和仅上传模式（与 copyparty 的只写相同）
* 🔵 HTTPS、WebDAV，但没有 FTP

## [gimme-that](https://github.com/nejdetckenobi/gimme-that)
* Python，但有 C 依赖
* ⚠️ 没有虚拟文件系统；单文件夹，多账户
* ⚠️ 上传不可恢复/加速/完整性检查
  * ⚠️ 在 Cloudflare 上：最大上传大小 100 MiB
* ⚠️ 上传的奇怪文件夹结构
* ✅ 上传时 ClamAV 防病毒检查！很棒
* 🔵 可选的最大文件大小，上传时操作系统通知
  * 💾 操作系统通知作为 [插件](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/notify.py) 可用

## [ass](https://github.com/tycrek/ass)
* Node.js；推荐 Docker
* ⚠️ 不便携
* ⚠️ 仅上传；没有浏览器
* ⚠️ 仅通过 ShareX 上传；没有 Web UI
* ⚠️ 上传不可恢复/加速/完整性检查
  * ⚠️ 在 Cloudflare 上：最大上传大小 100 MiB
* ✅ 令牌认证
* ✅ GPS 元数据剥离
  * 💾 可以通过 [插件](https://github.com/9001/copyparty/blob/hovudstraum/bin/mtag/image-noexif.py) 实现
* ✅ Discord 集成（自定义嵌入，上传 webhook）
  * 💾 [上传 webhook 插件](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/discord-announce.py)
* ✅ 按 MIME 类型拒绝上传
  * 💾 可以使用插件按 [扩展名](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/reject-extension.py) 或 [MIME类型](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/reject-mimetype.py) 拒绝上传
* ✅ 可以使用 S3 作为存储后端
  * 💾 依赖 rclone-mount
* ✅ 自定义 404 页面

## [linx](https://github.com/ZizzyDizzyMC/linx-server/)
* 最初是 [andreimarcu/linx-server](https://github.com/andreimarcu/linx-server) 但开发已结束
* ⚠️ 上传不可恢复/加速/完整性检查
  * ⚠️ 在 Cloudflare 上：最大上传大小 100 MiB
* 🔵 它的一些独特功能已添加到 copyparty，因为前 linx 用户已迁移
  * 文件过期计时器，文件名随机化
* ✅ 密码保护的文件
  * 💾 密码保护的文件夹 + 文件密钥跳过文件夹密码似乎涵盖了大多数用例
* ✅ 文件删除密钥
* ✅ 将文件下载为种子
* ✅ 远程上传（向服务器发送链接，它会下载）
  * 💾 作为 [插件](https://github.com/9001/copyparty/blob/hovudstraum/bin/hooks/wget.py) 可用
* ✅ 可以使用 S3 作为存储后端
  * 💾 依赖 rclone-mount

## [h5ai](https://larsjung.de/h5ai/)
* ⚠️ 只读；没有上传/移动/删除
* ⚠️ 搜索直接访问文件系统；不索引/缓存
* ✅ 时尚的 UI
* ✅ 浏览器内二维码生成器分享 URL
* 🔵 目录树、图片查看器、缩略图、下载为tar

## [autoindex](https://github.com/nielsAD/autoindex)
* ⚠️ 只读；没有上传/移动/删除
* ✅ 用于更快浏览云存储的目录缓存
  * 💾 用于递归搜索（名称/属性/标签）的本地索引/缓存，但不用于浏览

## [miniserve](https://github.com/svenstaro/miniserve)
* Rust；跨平台（Windows、Linux、Mac）
* ⚠️ 上传不可恢复/加速/完整性检查
  * ⚠️ 在 Cloudflare 上：最大上传大小 100 MiB
* ⚠️ 没有缩略图/图片查看器/音频播放器/文件管理器
* ⚠️ 没有文件系统索引/搜索
* 🔵 上传、tar/zip 下载、二维码
* ✅ 加载大文件夹更快

## [pingvin-share](https://github.com/stonith404/pingvin-share)
* Node.js；Linux（Docker）
* 主要用于上传，不是通用文件服务器
* 🔵 上传是分片的（避免 Cloudflare 大小限制）
* 🔵 分片直接写入目标文件（对硬盘友好）
* ⚠️ 浏览器或笔记本电脑崩溃后上传不可恢复
* ⚠️ 上传不加速/完整性检查
  * ⚠️ 跨大西洋，copyparty 快 3 倍
    * 使用 96 MiB 块大小测量；pingvin 的默认 10 MiB 要慢得多
* ⚠️ 无法上传带子文件夹的文件夹
* ⚠️ 没有上传 ETA
* 🔵 过期时间、共享、上传撤销
* ✅ 配置 + 用户注册 GUI
* ✅ 内置 OpenID 和 LDAP 支持
  * 💾 [IdP 中间件](https://github.com/9001/copyparty#identity-providers) 和配置文件
* ✅ 可能有不止一个人理解代码


# 简要考虑

* [pydio](https://github.com/pydio/cells)：Python/AGPL3，看起来很棒，出色的 UX -- 但需要 MariaDB，系统级安装
* [gossa](https://github.com/pldubouilh/gossa)：Go/MIT，极简主义，基本文件上传，文本编辑器，mkdir 和重命名（没有删除/移动）


# 注释

* 高延迟连接（跨大西洋上传）可以用 `tc qdisc add dev eth0 root netem delay 100ms` 准确模拟

---

*本文档翻译自 [versus.md](./versus.md)，可能存在一些术语翻译差异。如有疑问，请参考英文原版。*
