# [`u2c.py`](u2c.py)
* 命令行 up2k 客户端 [(webm)](https://ocv.me/stuff/u2cli.webm)
* 文件上传、文件搜索、自动恢复中断/损坏的上传
* [同步本地文件夹到服务器](https://github.com/9001/copyparty/#folder-sync)
* 通常比浏览器更快
* 如果出现问题，重启即可


# [`partyjournal.py`](partyjournal.py)
通过收集 up2k 数据库和文件系统的信息，生成所有上传文件的时间顺序列表
* 输出独立的 HTML 文件
* 可选的 IP 地址到昵称的映射


# [`partyfuse.py`](partyfuse.py)
* 将 copyparty 服务器挂载为本地文件系统（只读）
* **支持 Windows！** -- 预期顺序读取速度 `194 MiB/s`
* **支持 Linux** -- 预期顺序读取速度 `600 MiB/s`
* **支持 macOS** -- 预期顺序读取速度 `85 MiB/s`

注意 copyparty 应该使用 `-ed` 参数运行以启用点文件（否则会被隐藏）

建议考虑使用 [../docs/rclone.md](../docs/rclone.md) 替代；通常更快一些，特别是在 Windows 上


## 在 Windows 上运行：
* 安装 [winfsp](https://github.com/billziss-gh/winfsp/releases/latest) 和 [python 3](https://www.python.org/downloads/)
  * [x] 将 python 3.x 添加到 PATH（安装时会询问）
* `python -m pip install --user fusepy`（或从 copyparty 的 `connect` 页面获取 `fuse.py` 副本，并保存在同一文件夹中）
* `python ./partyfuse.py n: http://192.168.1.69:3923/`

在 [msys2](https://www.msys2.org/) 中快 10%，如果启用调试打印则快 700%：
* `pacman -S mingw64/mingw-w64-x86_64-python{,-pip}`
* `/mingw64/bin/python3 -m pip install --user fusepy`
* `/mingw64/bin/python3 ./partyfuse.py [...]`

你可以用 [dokan](https://github.com/dokan-dev/dokany/releases/latest) 替换 winfsp，如果你[知道怎么做](https://github.com/dokan-dev/dokany/wiki/FUSE)请告诉我  
（winfsp 的 sshfs 有内存泄漏，但 winfsp 本身看起来没有，应该没问题）



# [`partyfuse2.py`](partyfuse2.py)
* 将 copyparty 服务器挂载为本地文件系统（只读）
* 做同样的事情但更正确，`samba` 认可
* **支持 Linux** -- 预期速度 `18 MiB/s`（等等，什么？）
* **支持 macOS** -- 可能支持



# [`partyfuse-streaming.py`](partyfuse-streaming.py)
* 假装这个不存在



# [`mtag/`](mtag/)
* 执行各种文件分析的独立程序
* copyparty 可以在文件索引期间 Popen 这样的程序来收集额外的元数据



# [`dbtool.py`](dbtool.py)
升级工具，可以显示数据库信息并帮助在数据库之间传输数据，例如当新版本的 copyparty 与旧数据库不兼容并自动从头重建数据库时，但你有一些非常昂贵的 `-mtp` 解析器，想要从旧数据库复制标签

对于该示例（升级到 v0.11.20），首先像往常一样启动新版本的 copyparty，让它备份旧数据库并重建新数据库，直到开始运行 mtp（添加 mtp 标签时的彩色消息），这时按 CTRL-C 并从旧数据库中修补旧的 mtp 标签

假设你有 `-mtp` 解析器来提供标签 `key` 和 `.bpm`：

```
cd /mnt/nas/music/.hist
~/src/copyparty/bin/dbtool.py -ls up2k.db
~/src/copyparty/bin/dbtool.py -src up2k.*.v3 up2k.db -cmp
~/src/copyparty/bin/dbtool.py -src up2k.*.v3 up2k.db -rm-mtp-flag -copy key
~/src/copyparty/bin/dbtool.py -src up2k.*.v3 up2k.db -rm-mtp-flag -copy .bpm -vac
```



# [`prisonparty.sh`](prisonparty.sh)
* 在 chroot 中运行 copyparty，防止任何意外的文件访问
* 为 /bin、/lib 等创建绑定挂载，参见 `sysdirs=`

# [`bubbleparty.sh`](bubbleparty.sh)
* 在隔离进程中运行 copyparty，防止任何意外的文件访问等
