# 自己构建镜像

```bash
./make.sh hclean pull img push
```
将从 github 下载最新的 copyparty-sfx.py（除非您已经[从头开始构建](../../docs/devnotes.md#just-the-sfx)），然后基于此构建所有镜像

已弃用的替代方案：运行 `make` 使用 makefile，但它使用 docker 而不是 podman，并且只构建 x86_64

`make.sh` 必然(?)过度工程化，因为：
* podman 不使用缓存镜像而持续消耗 dockerhub 拉取次数（`--pull=never` 不适用于清单）
* podman 无法从本地清单构建，只能从本地镜像或远程清单构建

但我真的不知道我在这里做什么 💩

* 推送镜像到仓库的认证；  
  `podman login docker.io`  
  `podman login ghcr.io -u 9001`  
  [关于 gchq](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry)（使用经典令牌作为密码）


## 在 alpine 上构建

```bash
apk add podman{,-docker}
rc-update add cgroups
service cgroups start
vim /etc/containers/storage.conf  # driver = "btrfs"
modprobe tun
echo ed:100000:65536 >/etc/subuid
echo ed:100000:65536 >/etc/subgid
apk add qemu-openrc qemu-tools qemu-{arm,armeb,aarch64,s390x,ppc64le}
rc-update add qemu-binfmt
service qemu-binfmt start
```
