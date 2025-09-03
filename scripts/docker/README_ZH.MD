copyparty 可在以下仓库中获取：
* https://hub.docker.com/u/copyparty
* https://github.com/9001?tab=packages&repo_name=copyparty


# 快速开始

运行以下命令获取最新的 copyparty 镜像并启动：
```bash
docker run --rm -it -u 1000 -p 3923:3923 -v /mnt/nas:/w -v $PWD/cfgdir:/cfg copyparty/ac
```

* `/w` 是容器内默认共享的路径，将一个或多个要共享的文件夹挂载到此路径下
* `/cfg` 是可选的配置文件夹，包含零个或多个配置文件（*.conf）
* `copyparty/ac` 是推荐的[镜像版本](#版本)
* 您可以通过将 `copyparty/ac` 替换为 `ghcr.io/9001/copyparty-ac` 来从 github 下载镜像
* 如果您使用无根 podman，请移除 `-u 1000`
* 如果您使用 selinux，请在所有 `-v` 参数后添加 `:z`（例如 `-v /mnt/nas:/w:z`）

此示例也可作为兼容 podman 的 [docker-compose yaml](https://github.com/9001/copyparty/blob/hovudstraum/docs/examples/docker/basic-docker-compose) 使用；使用示例：`docker-compose up`（您可能需要 `systemctl enable --now podman.socket` 或类似命令）

我对容器不是很熟悉，如果这部分可以改进请告诉我 🙏


## portainer

* 有一个[portainer 教程](https://github.com/9001/copyparty/blob/hovudstraum/docs/examples/docker/portainer.md)，但大部分未经测试


## 配置

> 本节基本解释了 [docker-compose yaml](https://github.com/9001/copyparty/blob/hovudstraum/docs/examples/docker/basic-docker-compose) 的工作原理，您也可以直接查看那里

容器具有与 sfx 和 pypi 模块相同的默认配置，即监听端口 3923 并将"当前文件夹"（容器内的 `/w`）作为任何人都可读写的共享

在容器内配置 copyparty 的推荐方法是挂载一个包含一个或多个[配置文件](https://github.com/9001/copyparty/blob/hovudstraum/docs/example.conf)的文件夹；`-v /your/config/folder:/cfg`

* 但如果您愿意，也可以向 docker 命令提供参数
* 配置文件必须命名为 `something.conf` 才能被识别

另请参阅[Docker 特定建议](#docker-特定建议)


## 版本

安装后的镜像大小和 gzip 压缩后的大小

* [`min`](https://hub.docker.com/r/copyparty/min) (57 MiB, 20 gz) 仅包含 copyparty 本身
* [`im`](https://hub.docker.com/r/copyparty/im) (70 MiB, 25 gz) 可以使用 pillow 生成图像缩略图，使用 mutagen 解析媒体文件
* [`ac` (163 MiB, 56 gz)](https://hub.docker.com/r/copyparty/ac) 是 `im` 加上 ffmpeg，用于视频/音频缩略图 + 音频转码 + 更好的标签
* [`iv`](https://hub.docker.com/r/copyparty/iv) (211 MiB, 73 gz) 是 `ac` 加上 vips，用于更快的 heif / avic / jxl 缩略图
* [`dj`](https://hub.docker.com/r/copyparty/dj) (309 MiB, 104 gz) 是 `iv` 加上 beatroot/keyfinder 来检测音乐调性和 bpm

[推荐使用 `ac`](https://hub.docker.com/r/copyparty/ac)，因为 `iv` 和 `dj` 中的附加功能很少有用

大多数版本支持 `x86`、`x86_64`、`armhf`、`aarch64`、`ppc64le`、`s390x`
* `dj` 不能在 `ppc64le`、`s390x`、`armhf` 上运行
* `iv` 不能在 `ppc64le`、`s390x` 上运行

> 注意：以下版本是未完成的实验，未在任何地方发布：djd djf djff dju


## 检测 bpm 和音乐调性

`dj` 版本包含 `keyfinder` 和 `beatroot`，可用于检测音乐 bpm 和音乐调性

在配置文件中全局启用：
```yaml
[global]
e2dsa, e2ts  # 启用文件系统索引和多媒体索引
mtp: .bpm=f,t30,/mtag/audio-bpm.py  # 应该需要约 10 秒
mtp: key=f,t190,/mtag/audio-key.py  # 应该需要约 50 秒
```

或仅为一个卷启用：
```yaml
[/music]  # 共享名称 / URL
  music   # docker 卷 `/w` 内的文件系统路径
  flags:
    e2dsa, e2ts
    mtp: .bpm=f,t30,/mtag/audio-bpm.py
    mtp: key=f,t190,/mtag/audio-key.py
```

或使用命令行参数：
```
-e2dsa -e2ts -mtp .bpm=f,t30,/mtag/audio-bpm.py -mtp key=f,t190,/mtag/audio-key.py
```


# 常见问题

以下建议是尽力而为的，不保证完全正确

* 问：在 debian 12 上启动无根容器失败，错误为 `failed to register layer: lsetxattr user.overlay.impure /etc: operation not supported`
  * 答：debian 上 docker 的默认无根配置使用 overlay2 存储驱动程序；这不起作用。您的选择是将 docker 替换为 podman（好选择），或配置 docker 使用 `fuse-overlayfs` 存储驱动程序



# Docker 特定建议

* copyparty 通常会在每个卷的顶部创建一个 `.hist` 文件夹，其中包含文件系统索引、缩略图等。出于性能原因，也为了保持整洁，将这些存储在配置文件夹内可能会很方便。在您的 `copyparty.conf` 的 `[global]` 部分内添加 `hist: /cfg/hists/` 行来实现这一点

* 如果您想要更好的性能，并且可以接受内存使用量翻倍，那么考虑启用 mimalloc **（可能有错误）**，使用以下之一：

  * `-e LD_PRELOAD=/usr/lib/libmimalloc-secure.so.2` 使下载为 zip **快 3 倍**，文件系统索引**快 1.5 倍**等

  * `-e LD_PRELOAD=/usr/lib/libmimalloc-insecure.so.2` 增加额外 10% 的速度，但使未来漏洞更容易被利用

  * 完整示例：`podman run --rm -it -p 3923:3923 -v "$PWD:/w:z" -e LD_PRELOAD=/usr/lib/libmimalloc-secure.so.2 copyparty/ac -v /w::r`


## 启用 ftp 服务器

...很棘手，因为 ftp 是一个奇怪的协议，而 docker 让它变得更糟 🎉

将以下三个配置条目添加到您的 `copyparty.conf` 的 `[global]` 部分：

* `ftp: 3921` 启用服务，监听端口 3921 上的连接

* `ftp-nat: 127.0.0.1` 但将 `127.0.0.1` 替换为您服务器的实际外部 IP；客户端只能连接到此 IP，即使服务器有多个 IP

* `ftp-pr: 12000-12099` 限制[被动模式](http://slacksite.com/other/ftp.html#passive)端口选择范围；这允许最多 100 个同时文件传输

然后最后更新您的 docker 配置，使您指定的端口范围（12000-12099）暴露给互联网


# 自己构建镜像

基本上是 `./make.sh hclean pull img push`，但请参阅 [devnotes.md](./devnotes.md)
