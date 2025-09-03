# copyparty.conf 配置指南

## 概述

copyparty 支持使用配置文件来管理服务器设置，这比使用命令行参数更加方便和可维护。配置文件使用类似 YAML 的语法，但实际上不是标准的 YAML 格式。

## 配置文件结构

配置文件主要包含以下几个部分：

1. `[global]` - 全局设置
2. `[accounts]` - 用户账户
3. `[groups]` - 用户组
4. `[/path]` - 卷(Volume)定义

## 基本语法

```yaml
# 注释必须在 # 号前有两个空格
[section]
  key: value  # 行内注释
  flag        # 布尔标志
```

## 全局配置 [global]

### 网络设置

```yaml
[global]
  # 监听地址和端口
  i: 127.0.0.1        # 只监听本地地址
  i: 0.0.0.0          # 监听所有地址
  p: 3939             # 监听端口
  p: 8086, 3939       # 监听多个端口
  
  # 连接限制
  nc: 1024            # 最大客户端连接数
  j: 4                # 最大CPU核心数，0=全部，1=默认
```

### 功能开关

```yaml
[global]
  # 文件索引和扫描
  e2d                 # 启用数据库，使文件可搜索
  e2ds                # 启动时扫描可写文件夹
  e2dsa               # 启动时扫描所有文件夹
  
  # 多媒体索引
  e2t                 # 启用多媒体索引
  e2ts                # 启动时扫描现有文件的标签
  e2tsr               # 完全重新扫描（删除所有元数据）
  
  # 其他功能
  ed                  # 允许显示隐藏文件
  grid                # 默认显示网格/缩略图视图
  qr                  # 生成二维码
  z                   # 启用 zeroconf/mDNS
```

### UI 设置

```yaml
[global]
  theme: 2            # 主题编号 (0-9)
  lang: eng           # 语言设置 (eng/nor/chi)
  localtime           # 使用本地时区而非UTC
  name: "我的服务器"   # 服务器名称
```

## 用户账户 [accounts]

```yaml
[accounts]
  admin: password123    # 用户名: 密码
  user1: pass1
  user2: pass2
  guest: guest123
```

## 用户组 [groups]

```yaml
[groups]
  admins: admin, user1      # 组名: 用户列表
  users: user1, user2
  readonly: guest
```

## 卷配置 [/path]

### 基本卷定义

```yaml
[/]                   # URL路径
  /srv/files          # 文件系统路径
  accs:               # 访问控制
    r: *              # 所有人只读
    rw: admin         # admin 读写权限

[/music]
  /home/user/Music
  accs:
    r: @users         # users组只读 (@ 表示组)
    rw: admin
```

### 权限系统详解

| 权限 | 说明 |
|------|------|
| `r` | 读取：浏览文件夹，下载文件 |
| `w` | 写入：上传文件（需要r权限才能看到上传的文件） |
| `m` | 移动：移动文件和文件夹 |
| `d` | 删除：永久删除文件和文件夹 |
| `g` | 获取：只能下载文件，不能浏览文件夹 |
| `G` | 上传获取：类似g，但可以看到自己上传的文件密钥 |
| `h` | HTML：类似g，但文件夹返回index.html |
| `a` | 管理员：查看上传者IP，配置重载 |
| `A` | 全部：等同于 `rwmda.` |
| `.` | 点文件：用户可以请求显示隐藏文件 |

### 权限组合示例

```yaml
[/upload]
  /srv/upload
  accs:
    w: *              # 所有人可上传
    rwmd: admin       # admin 全权限
    r: @users         # users组只读

[/private]
  /srv/private
  accs:
    rwmda: admin      # admin 全权限
    r: user1, user2   # 特定用户只读

[/sharex]
  /srv/sharex
  accs:
    wG: *             # 所有人可上传并查看自己的文件
    rwmd: admin       # admin 管理权限
```

## 卷标志 (Volume Flags)

卷标志用于为特定卷启用或禁用功能：

```yaml
[/volume]
  /path/to/files
  accs:
    r: *
  flags:
    # 数据库相关
    e2d               # 启用数据库
    e2ds              # 启动时扫描
    scan: 60          # 每60秒重新扫描
    
    # 上传控制
    nodupe            # 拒绝重复文件
    fk: 4             # 启用文件密钥（4字符长）
    rand              # 强制随机文件名
    
    # 安全设置
    d2t               # 禁用多媒体解析器
    dthumb            # 禁用缩略图
    
    # 文件系统
    nohash: "\.iso$"  # 跳过匹配模式的文件哈希
    xdev              # 避免跨文件系统
```

### 常用标志说明

| 标志 | 说明 |
|------|------|
| `e2d` | 启用数据库，使文件可搜索 |
| `e2ds` | 启动时扫描可写文件夹 |
| `e2t` | 启用多媒体索引 |
| `e2ts` | 启动时扫描多媒体标签 |
| `nodupe` | 拒绝重复文件上传 |
| `fk: N` | 启用N字符长的文件密钥 |
| `scan: N` | 每N秒重新扫描文件 |
| `d2t` | 禁用多媒体解析器 |
| `dthumb` | 禁用缩略图生成 |
| `grid` | 默认显示网格视图 |
| `rand` | 强制随机文件名 |

## 配置文件包含

可以包含其他配置文件：

```yaml
# 包含其他配置文件（注意%后的空格）
% /etc/copyparty/additional.conf
% copyparty.d                    # 包含目录中所有.conf文件
```

## 完整示例

```yaml
# copyparty.conf 完整示例
[global]
  p: 3939             # 监听端口
  e2dsa               # 启用文件索引和扫描
  e2ts                # 启用多媒体索引
  grid                # 默认网格视图
  qr                  # 生成二维码
  theme: 2            # 使用主题2

[accounts]
  admin: admin123
  user1: pass1
  user2: pass2
  guest: guest

[groups]
  staff: admin, user1
  users: user1, user2

[/]
  /srv/public
  accs:
    r: *              # 公开只读
    rw: @staff        # 员工读写

[/upload]
  /srv/upload
  accs:
    w: *              # 所有人可上传
    rwmd: admin       # admin管理
  flags:
    e2d               # 启用数据库
    nodupe            # 拒绝重复文件

[/private]
  /srv/private
  accs:
    rwmda: admin      # 仅admin访问

[/music]
  /home/music
  accs:
    r: @users         # 用户组只读
    rw: admin
  flags:
    e2t               # 启用音乐标签索引
    grid              # 网格视图
```

## 使用配置文件

```bash
# 使用配置文件启动
copyparty -c copyparty.conf

# 或设置环境变量
export PRTY_CONFIG=copyparty.conf
copyparty

# 多个配置文件
copyparty -c main.conf -c extra.conf
```

## 高级配置

### 钩子和处理器

```yaml
[/volume]
  /path
  flags:
    # 上传后执行脚本
    xau: script.py
    xau: j,t10,script.py    # j=提供JSON，t10=10秒超时

    # 其他钩子
    xm: message_handler.py  # 消息钩子
    on404: error_handler.py # 404错误处理
    on403: auth_handler.py  # 403错误处理
```

### 上传限制

```yaml
[/volume]
  /path
  flags:
    # 上传数量限制
    maxn: 250,600         # 15分钟内最多250个文件
    maxb: 1g,300          # 5分钟内最多1GB

    # 卷大小限制
    vmaxb: 10g            # 卷总大小限制10GB
    vmaxn: 4k             # 卷最多4096个文件

    # 文件权限
    chmod_f: 644          # 新文件权限
    chmod_d: 755          # 新目录权限
    uid: 1000             # 文件所有者UID
    gid: 1000             # 文件所有者GID
```

### WebDAV 配置

```yaml
[global]
  # 启用WebDAV
  dav                   # 启用WebDAV服务器

[/webdav]
  /srv/webdav
  accs:
    rw: user1
  flags:
    davauth             # WebDAV客户端需要登录
    daw                 # 启用完整WebDAV写入支持（危险）
```

### 多媒体设置

```yaml
[/media]
  /srv/media
  flags:
    # 缩略图设置
    thsize: 256x256     # 缩略图尺寸
    crop: y             # 启用裁剪
    th3x: y             # 3倍分辨率

    # 转换超时
    convt: 30           # 图像转换超时30秒
    aconvt: 60          # 音频转换超时60秒

    # 禁用特定缩略图
    dvthumb             # 禁用视频缩略图
    dathumb             # 禁用音频缩略图
    dithumb             # 禁用图像缩略图
```

### 身份提供者(IDP)集成

```yaml
[global]
  # IDP头部设置
  idp-h-usr: X-Remote-User      # 用户名头部
  idp-h-grp: X-Remote-Groups    # 用户组头部

  # 登录页面设置
  login: pw,ipu                 # 显示密码和IDP登录

# 动态卷配置
[/u/${u}]               # ${u} 会被用户名替换
  /home/${u}
  accs:
    rwmda: ${u}         # 用户对自己的目录有全权限

[/group/${g}]           # ${g} 会被组名替换
  /srv/groups/${g}
  accs:
    rw: @${g}           # 组成员有读写权限
```

### 安全设置

```yaml
[global]
  # 访问控制
  ipa: 192.168.1.      # 只允许特定IP段访问
  ban-pw: 9,3600,86400 # 密码错误9次，1小时内，封禁24小时

  # SSL/TLS
  crt: server.crt      # SSL证书
  key: server.key      # SSL私钥

[/secure]
  /srv/secure
  accs:
    r: admin
  flags:
    # 安全标志
    no_db_ip            # 不在数据库中存储IP
    forget_ip: 43200    # 30天后忘记上传者IP
```

### 性能优化

```yaml
[global]
  # 性能设置
  j: 0                  # 使用所有CPU核心
  nc: 2048              # 增加最大连接数

[/volume]
  /path
  flags:
    # 文件系统优化
    xdev                # 避免跨文件系统
    xvol                # 忽略跨卷符号链接

    # 哈希优化
    nohash: "\.iso$"    # 跳过大文件哈希
    safededup           # 安全去重验证

    # 扫描优化
    scan: 3600          # 每小时扫描一次
    d2ds                # 禁用启动时索引
```

## 故障排除

### 常见问题

1. **权限问题**
   ```yaml
   # 确保文件系统权限正确
   flags:
     chmod_f: 644
     chmod_d: 755
   ```

2. **性能问题**
   ```yaml
   # 禁用不需要的功能
   flags:
     d2t               # 禁用多媒体解析
     dthumb            # 禁用缩略图
     nohash: ".*"      # 禁用所有哈希
   ```

3. **内存使用**
   ```yaml
   [global]
     j: 1              # 限制CPU使用
     nc: 512           # 限制连接数
   ```

### 调试配置

```yaml
[global]
  # 详细日志
  v                     # 详细模式
  vv                    # 更详细模式

  # 测试配置
  no-reload             # 禁用配置重载
```

## 注意事项

1. 注释前必须有两个空格
2. 配置文件优先级高于命令行参数
3. 路径可以使用 `~` 表示用户主目录
4. 组名前需要加 `@` 符号
5. `*` 表示所有用户（包括匿名用户）
6. 配置文件支持热重载（需要admin权限）
7. 使用 `-` 前缀可以禁用标志（如 `-e2d`）
8. 标志可以组合在一行：`e2d, nodupe, fk: 4`
9. 动态变量 `${u}` 和 `${g}` 需要IDP支持
10. 路径分隔符在Windows上会自动转换

## 实际应用场景

### 家庭媒体服务器

```yaml
# 家庭媒体服务器配置
[global]
  p: 3939
  e2dsa               # 全面索引
  e2ts                # 音视频标签
  grid                # 网格视图
  qr                  # 二维码访问
  theme: 2

[accounts]
  admin: family_admin_pass
  family: family_pass
  guest: guest_pass

[/]
  /srv/media
  accs:
    r: *              # 公开浏览
    rw: admin

[/movies]
  /srv/movies
  accs:
    r: family, guest
    rw: admin
  flags:
    e2t, grid

[/music]
  /srv/music
  accs:
    r: family, guest
    rw: admin
  flags:
    e2t, grid

[/photos]
  /srv/photos
  accs:
    r: family
    rw: admin
  flags:
    e2d, grid, thsize: 512x512

[/upload]
  /srv/upload
  accs:
    w: family         # 家庭成员可上传
    rwmd: admin
  flags:
    e2d, nodupe, fk: 6
```

### 企业文件共享

```yaml
# 企业文件共享配置
[global]
  p: 443
  crt: /etc/ssl/company.crt
  key: /etc/ssl/company.key
  e2dsa
  ban-pw: 5,1800,7200   # 更严格的密码策略

[accounts]
  admin: secure_admin_pass
  manager1: manager_pass1
  manager2: manager_pass2
  employee1: emp_pass1
  employee2: emp_pass2

[groups]
  managers: manager1, manager2
  employees: employee1, employee2
  all_staff: manager1, manager2, employee1, employee2

[/]
  /srv/company
  accs:
    r: @all_staff
    rw: admin

[/public]
  /srv/public
  accs:
    r: *              # 公开访问
    rw: @managers

[/departments/hr]
  /srv/hr
  accs:
    r: @managers
    rw: admin
  flags:
    e2d, no_db_ip     # 不记录IP保护隐私

[/departments/finance]
  /srv/finance
  accs:
    rwmda: admin      # 仅管理员
  flags:
    e2d, forget_ip: 86400  # 24小时后忘记IP

[/projects]
  /srv/projects
  accs:
    r: @all_staff
    rw: @managers
    m: @employees     # 员工可移动文件
  flags:
    e2d, scan: 300    # 5分钟扫描一次

[/upload]
  /srv/incoming
  accs:
    w: @all_staff
    rwmd: @managers
  flags:
    e2d, nodupe, maxb: 100m,3600  # 1小时内最多100MB
```

### 个人云存储

```yaml
# 个人云存储配置
[global]
  p: 8080
  e2dsa
  e2ts
  qr
  grid

[accounts]
  owner: my_secure_password

[/]
  /home/user/cloud
  accs:
    rwmda: owner

[/backup]
  /home/user/backup
  accs:
    rwmda: owner
  flags:
    e2d, nodupe, dedup  # 启用去重节省空间

[/sync]
  /home/user/sync
  accs:
    rwmda: owner
  flags:
    e2d, scan: 60     # 快速同步检测

[/public]
  /home/user/public
  accs:
    r: *              # 公开分享
    rw: owner
  flags:
    e2d, fk: 8        # 长文件密钥用于分享
```

### 开发团队协作

```yaml
# 开发团队配置
[global]
  p: 3939
  e2dsa
  theme: 1            # 深色主题适合开发者

[accounts]
  lead: lead_pass
  dev1: dev1_pass
  dev2: dev2_pass
  tester: test_pass

[groups]
  developers: lead, dev1, dev2
  team: lead, dev1, dev2, tester

[/]
  /srv/project
  accs:
    r: @team
    rw: @developers

[/releases]
  /srv/releases
  accs:
    r: @team
    rw: lead          # 只有负责人可发布
  flags:
    e2d, nodupe

[/docs]
  /srv/docs
  accs:
    r: *              # 文档公开
    rw: @team
  flags:
    e2d, exp          # 启用文本扩展

[/uploads]
  /srv/uploads
  accs:
    w: @team
    rwmd: lead
  flags:
    e2d, magic        # 自动检测文件类型
    maxn: 50,900      # 15分钟内最多50个文件

[/builds]
  /srv/builds
  accs:
    r: @developers
    w: lead           # 只有负责人可上传构建
  flags:
    e2d, nohash: "\.(zip|tar\.gz|exe)$"  # 跳过大文件哈希
```

## 最佳实践

### 安全建议

1. **使用强密码**
   ```yaml
   [accounts]
     admin: $(openssl rand -base64 32)  # 生成随机密码
   ```

2. **限制访问**
   ```yaml
   [global]
     ipa: 192.168.1.    # 限制内网访问
     ban-pw: 3,1800,86400  # 严格的密码策略
   ```

3. **启用HTTPS**
   ```yaml
   [global]
     crt: /path/to/cert.pem
     key: /path/to/key.pem
   ```

### 性能优化

1. **合理使用索引**
   ```yaml
   # 只在需要搜索的卷启用
   flags:
     e2d               # 仅在必要时启用
   ```

2. **控制扫描频率**
   ```yaml
   flags:
     scan: 3600        # 根据需要调整扫描间隔
   ```

3. **优化缩略图**
   ```yaml
   flags:
     thsize: 256x256   # 合适的缩略图尺寸
     dthumb            # 在不需要时禁用
   ```

### 维护建议

1. **定期备份配置**
   ```bash
   cp copyparty.conf copyparty.conf.backup
   ```

2. **使用版本控制**
   ```bash
   git init
   git add copyparty.conf
   git commit -m "Initial config"
   ```

3. **监控日志**
   ```yaml
   [global]
     v                 # 启用详细日志
   ```

4. **测试配置**
   ```bash
   # 测试配置文件语法
   copyparty -c copyparty.conf --help > /dev/null
   ```

## 常见问题解答

### Q: 如何重新加载配置文件？
A: 有管理员权限的用户可以在控制面板中点击"reload"按钮，或者发送SIGHUP信号：
```bash
kill -HUP $(pgrep copyparty)
```

### Q: 配置文件中的路径支持哪些格式？
A: 支持以下格式：
- 绝对路径：`/srv/files`
- 相对路径：`./files`
- 用户主目录：`~/files`
- 环境变量：`$HOME/files`

### Q: 如何设置只允许上传不允许下载？
A: 使用 `w` 权限而不给 `r` 权限：
```yaml
[/upload-only]
  /srv/upload
  accs:
    w: user1          # 只能上传
    rwmd: admin       # 管理员全权限
```

### Q: 如何实现用户只能看到自己上传的文件？
A: 使用 `wG` 权限组合和文件密钥：
```yaml
[/personal]
  /srv/personal
  accs:
    wG: *             # 写入+上传获取权限
    rwmd: admin
  flags:
    fk: 6             # 启用文件密钥
```

### Q: 如何禁用某个全局设置？
A: 在卷配置中使用 `-` 前缀：
```yaml
[global]
  e2d                 # 全局启用数据库

[/no-db]
  /srv/simple
  flags:
    -e2d              # 此卷禁用数据库
```

### Q: 如何设置文件上传大小限制？
A: 使用 `maxb` 标志：
```yaml
flags:
  maxb: 100m,3600     # 1小时内最多100MB
  vmaxb: 10g          # 卷总大小限制10GB
```

### Q: 如何启用WebDAV？
A: 在全局配置中启用，并为卷设置适当权限：
```yaml
[global]
  dav                 # 启用WebDAV

[/webdav]
  /srv/webdav
  accs:
    rw: user1
  flags:
    davauth           # 需要认证
```

### Q: 如何自定义错误页面？
A: 使用错误处理钩子：
```yaml
flags:
  on404: /path/to/404_handler.py
  on403: /path/to/403_handler.py
```

## 配置文件模板

### 最小配置
```yaml
[global]
  p: 3939

[accounts]
  admin: password

[/]
  .
  accs:
    r: *
    rw: admin
```

### 标准配置
```yaml
[global]
  p: 3939
  e2dsa
  e2ts
  grid
  qr

[accounts]
  admin: secure_password
  user: user_password

[/]
  /srv/files
  accs:
    r: *
    rw: admin, user
  flags:
    e2d

[/upload]
  /srv/upload
  accs:
    w: *
    rwmd: admin
  flags:
    e2d, nodupe
```

### 高级配置
```yaml
[global]
  p: 3939, 8080
  e2dsa
  e2ts
  grid
  qr
  theme: 2
  ban-pw: 5,3600,86400

[accounts]
  admin: $(cat /etc/copyparty/admin.pass)
  user1: user1_pass
  user2: user2_pass

[groups]
  users: user1, user2

[/]
  /srv/public
  accs:
    r: *
    rw: admin

[/private]
  /srv/private
  accs:
    rwmda: admin
  flags:
    e2d, no_db_ip

[/shared]
  /srv/shared
  accs:
    r: @users
    rw: admin
  flags:
    e2d, scan: 1800

[/upload]
  /srv/upload
  accs:
    w: @users
    rwmd: admin
  flags:
    e2d, nodupe, fk: 8, maxb: 500m,3600
```

## 参考资源

### 命令行帮助
```bash
copyparty --help           # 基本帮助
copyparty --help-accounts  # 账户系统帮助
copyparty --help-flags     # 卷标志帮助
copyparty --help-handlers  # 处理器帮助
```

### 相关文件
- `docs/example.conf` - 基本配置示例
- `docs/example2.conf` - 包含文件示例
- `docs/chungus.conf` - 完整配置参考
- `docs/copyparty.d/` - 模块化配置示例

### 在线资源
- GitHub仓库：https://github.com/9001/copyparty
- 官方文档：项目README文件
- 问题反馈：GitHub Issues

---

*本指南基于 copyparty 的最新版本编写，具体功能可能因版本而异。建议查看 `copyparty --help` 获取最新信息。*
