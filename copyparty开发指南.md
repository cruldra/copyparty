# CopyParty 开发指南

## 项目概述

CopyParty 是一个便携式文件服务器，支持断点续传上传/下载、文件去重、WebDAV、FTP、零配置、媒体索引、视频缩略图、音频转码和只写文件夹等功能。

### 核心特性
- **多协议支持**: HTTP/HTTPS、WebDAV、FTP、TFTP、SMB/CIFS
- **断点续传**: 基于 up2k 协议的可恢复上传/下载
- **文件去重**: 基于内容的重复文件检测
- **媒体处理**: 缩略图生成、音频转码、视频预览
- **权限管理**: 细粒度的用户和文件夹权限控制
- **跨平台**: 支持 Windows、Linux、macOS、Android、iOS

## 开发环境设置

### 环境要求
- Python 3.3+ (推荐 3.8+)
- 可选依赖：
  - `Pillow`: 图片缩略图
  - `FFmpeg`: 视频/音频处理
  - `mutagen`: 音频标签解析

### 安装开发环境

```bash
# 克隆项目
git clone https://github.com/9001/copyparty.git
cd copyparty

# 安装依赖
uv venv
uv pip install -e .
uv pip install -e ".[all]"  # 安装所有可选依赖

# 或使用传统方式
python -m pip install -e .
python -m pip install -e ".[all]"
```

### 开发工具配置

项目使用以下工具进行代码质量控制：

```bash
# 代码格式化
black --target-version py27 copyparty/

# 导入排序
isort copyparty/

# 代码检查
ruff check copyparty/
pylint copyparty/

# 类型检查
mypy copyparty/

# 安全检查
bandit -r copyparty/
```

## 项目架构

### 目录结构

```
copyparty/
├── copyparty/           # 主要源代码
│   ├── __main__.py     # 程序入口点
│   ├── httpsrv.py      # HTTP 服务器核心
│   ├── up2k.py         # 上传协议实现
│   ├── cfg.py          # 配置管理
│   ├── web/            # Web 前端资源
│   └── res/            # 静态资源
├── bin/                # 辅助工具和脚本
├── contrib/            # 第三方集成配置
├── docs/               # 文档
├── scripts/            # 构建和测试脚本
└── tests/              # 测试用例
```

### 核心模块

1. **httpsrv.py**: HTTP 服务器实现，处理请求路由
2. **up2k.py**: 实现 up2k 上传协议，支持断点续传
3. **cfg.py**: 配置文件解析和命令行参数处理
4. **authsrv.py**: 用户认证和权限管理
5. **svchub.py**: 服务管理中心，协调各个服务
6. **web/**: 前端 JavaScript 和 CSS 文件

## 开发流程

### 运行开发服务器

```bash
# 直接运行
python -m copyparty

# 使用配置文件
python -m copyparty -c docs/example.conf

# 开发模式（详细日志）
python -m copyparty --log-fk --log-conn -v .::rw
```

### 测试

```bash
# 运行所有测试
python -m unittest discover -s tests

# 运行特定测试
python -m unittest tests.test_up2k

# 运行集成测试
bash scripts/run-tests.sh

# 冒烟测试
python scripts/test/smoketest.py
```

### 代码贡献规范

1. **不使用 AI/LLM**: 项目要求 100% 人工编写代码
2. **代码风格**: 遵循 Black 格式化标准
3. **兼容性**: 支持 Python 2.7 和 3.3+
4. **测试**: 新功能必须包含测试用例

### 提交流程

```bash
# 安装 git hooks
bash scripts/install-githooks.sh

# 运行测试
bash scripts/run-tests.sh

# 提交代码
git add .
git commit -m "feat: 添加新功能"
git push origin feature-branch
```

## 构建和发布

### 构建 SFX (自解压文件)

```bash
# 构建 SFX
bash scripts/make-sfx.sh

# 构建 Windows 可执行文件
bash scripts/pyinstaller/build.sh
```

### 发布流程

```bash
# 准备发布
bash scripts/prep.sh

# 创建发布包
bash scripts/make-tgz-release.sh
bash scripts/make-pypi-release.sh
```

## 配置管理

### 配置文件格式

```yaml
[global]
  p: 3923        # 监听端口
  e2dsa          # 启用文件索引
  
[accounts]
  user1: pass1   # 用户账户

[/]              # 根目录
  /path/to/share # 本地路径
  accs:
    r: *         # 所有人可读
    rw: user1    # user1 可读写
```

### 权限系统

- `r`: 读取（浏览、下载）
- `w`: 写入（上传）
- `m`: 移动文件
- `d`: 删除文件
- `a`: 管理员权限
- `g`: 仅下载（不能浏览）
- `G`: 上传者可见自己的文件

## 调试技巧

### 日志配置

```bash
# 启用详细日志
python -m copyparty --log-fk --log-conn --log-thm

# 调试特定模块
python -m copyparty --log-fk=up2k,auth
```

### 性能分析

```bash
# 性能分析
python scripts/profile.py

# 文件系统性能测试
python scripts/speedtest-fs.py
```

### 常见问题

1. **缩略图不显示**: 检查 Pillow 或 FFmpeg 安装
2. **上传失败**: 检查磁盘空间和权限
3. **性能问题**: 调整并发设置和缓存配置

## 扩展开发

### 事件钩子

在 `bin/hooks/` 目录下创建脚本：

```python
#!/usr/bin/env python3
# 文件上传完成后触发
import sys
import json

event = json.loads(sys.argv[1])
if event['type'] == 'upload':
    print(f"文件上传: {event['path']}")
```

### 解析器插件

在 `bin/mtag/` 目录下创建解析器：

```python
#!/usr/bin/env python3
# 自定义文件格式解析器
import sys

def parse_file(file_path):
    # 解析文件并返回元数据
    return {"title": "示例", "author": "作者"}

if __name__ == "__main__":
    result = parse_file(sys.argv[1])
    print(json.dumps(result))
```

## 部署指南

### 系统服务

```bash
# 复制服务文件
sudo cp contrib/systemd/copyparty.service /etc/systemd/system/

# 启用服务
sudo systemctl enable copyparty
sudo systemctl start copyparty
```

### 反向代理

参考 `contrib/nginx/copyparty.conf` 配置 Nginx。

### Docker 部署

```bash
# 构建镜像
cd scripts/docker
make

# 运行容器
docker run -p 3923:3923 -v /data:/data copyparty
```

## 社区和支持

- **GitHub**: https://github.com/9001/copyparty
- **Discord**: https://discord.gg/25J8CdTT6G
- **演示服务器**: https://a.ocv.me/pub/demo/

## API 开发

### HTTP API

CopyParty 提供 RESTful API 用于文件操作：

#### 文件上传 (up2k 协议)

```bash
# 1. 获取上传令牌
curl -X POST "http://localhost:3923/up2k" \
  -H "Content-Type: application/json" \
  -d '{"name":"test.txt","size":1024,"hash":["abc123"]}'

# 2. 上传文件块
curl -X POST "http://localhost:3923/up2k" \
  -H "wark: upload_token" \
  -H "chs: chunk_hash" \
  --data-binary @chunk_data
```

#### 文件管理

```bash
# 列出文件
curl "http://localhost:3923/api/ls/path"

# 删除文件
curl -X POST "http://localhost:3923/api/delete" \
  -d "f=filename"

# 移动文件
curl -X POST "http://localhost:3923/api/move" \
  -d "f=source&t=target"
```

### WebDAV 支持

```bash
# 启用 WebDAV
python -m copyparty --dav

# 客户端连接
curl -X PROPFIND "http://localhost:3923/dav/"
```

## 前端开发

### JavaScript 架构

前端使用原生 JavaScript，无构建依赖：

- `browser.js`: 主要 UI 逻辑
- `up2k.js`: 上传功能
- `player.js`: 媒体播放器

### 自定义主题

```css
/* 在 contrib/themes/ 下创建主题 */
:root {
  --bg: #1a1a1a;
  --fg: #ffffff;
  --accent: #00ff00;
}
```

### 插件开发

```javascript
// contrib/plugins/example.js
(function() {
  'use strict';

  // 添加自定义功能
  function customFeature() {
    console.log('自定义功能');
  }

  // 注册插件
  if (window.copyparty) {
    window.copyparty.plugins.push(customFeature);
  }
})();
```

## 高级配置

### 性能优化

```yaml
[global]
  # 并发设置
  j: 4              # 工作线程数

  # 缓存设置
  th-maxage: 86400  # 缩略图缓存时间

  # 网络设置
  s-rd-sz: 65536    # 读取缓冲区大小
```

### 安全配置

```yaml
[global]
  # HTTPS 设置
  https: 3924
  cert: server.crt
  key: server.key

  # 访问控制
  ban-pw: 24,9,3600  # 密码错误封禁
  xff-hdr: x-real-ip # 真实 IP 头
```

### 文件索引

```yaml
[global]
  e2dsa             # 启用文件索引
  e2ts              # 启用媒体标签索引

[/music]
  /path/to/music
  flags:
    e2d             # 卷级别索引
    e2ts            # 媒体标签
```

## 故障排除

### 常见错误

1. **端口占用**
   ```bash
   # 检查端口使用
   netstat -tulpn | grep 3923
   ```

2. **权限问题**
   ```bash
   # 检查文件权限
   ls -la /path/to/share
   ```

3. **依赖缺失**
   ```bash
   # 检查可选依赖
   python -c "import PIL; print('Pillow OK')"
   ffmpeg -version
   ```

### 日志分析

```bash
# 启用详细日志
python -m copyparty --log-fk --log-conn 2>&1 | tee copyparty.log

# 分析上传问题
grep "up2k" copyparty.log

# 分析认证问题
grep "auth" copyparty.log
```

### 性能监控

```bash
# 启用 Prometheus 指标
python -m copyparty --stats

# 查看指标
curl http://localhost:3923/metrics
```

## 贡献指南

### 代码审查清单

- [ ] 代码符合 Black 格式
- [ ] 通过所有测试
- [ ] 兼容 Python 2.7+
- [ ] 包含适当的文档
- [ ] 无 AI 生成代码

### 功能开发流程

1. **创建 Issue**: 描述功能需求
2. **设计讨论**: 在 Discord 或 GitHub 讨论
3. **实现功能**: 遵循代码规范
4. **编写测试**: 确保功能正确
5. **提交 PR**: 详细描述变更

## 实用开发示例

### 添加新的 HTTP 端点

```python
# 在 httpsrv.py 中添加新路由
def handle_custom_api(self, req, resp):
    """处理自定义 API 请求"""
    if req.method != "POST":
        raise Pebkac(405, "Method not allowed")

    # 解析请求数据
    data = req.get_json()

    # 处理业务逻辑
    result = self.process_custom_request(data)

    # 返回 JSON 响应
    resp.set_json(result)

# 注册路由
self.add_route("/api/custom", self.handle_custom_api)
```

### 创建自定义中间件

```python
# 在 httpcli.py 中添加中间件
class CustomMiddleware:
    def __init__(self, app):
        self.app = app

    def __call__(self, req, resp):
        # 请求前处理
        self.before_request(req)

        # 调用下一个处理器
        result = self.app(req, resp)

        # 响应后处理
        self.after_request(req, resp)

        return result

    def before_request(self, req):
        # 添加自定义头部
        req.headers["X-Custom"] = "value"

    def after_request(self, req, resp):
        # 记录访问日志
        self.log_access(req, resp)
```

### 扩展文件处理器

```python
# 在 up2k.py 中添加文件处理逻辑
class CustomFileProcessor:
    def __init__(self, config):
        self.config = config

    def process_upload(self, file_path, metadata):
        """处理上传的文件"""
        # 文件验证
        if not self.validate_file(file_path):
            raise ValueError("文件验证失败")

        # 生成缩略图
        if self.is_image(file_path):
            self.generate_thumbnail(file_path)

        # 提取元数据
        if self.is_media(file_path):
            metadata.update(self.extract_media_info(file_path))

        return metadata

    def validate_file(self, file_path):
        """验证文件格式和内容"""
        # 检查文件大小
        if os.path.getsize(file_path) > self.config.max_file_size:
            return False

        # 检查文件类型
        mime_type = self.get_mime_type(file_path)
        if mime_type not in self.config.allowed_types:
            return False

        return True
```

### 数据库操作示例

```python
# 在 up2k.py 中操作 SQLite 数据库
class DatabaseManager:
    def __init__(self, db_path):
        self.db_path = db_path
        self.init_database()

    def init_database(self):
        """初始化数据库表"""
        with sqlite3.connect(self.db_path) as conn:
            conn.execute("""
                CREATE TABLE IF NOT EXISTS custom_metadata (
                    file_path TEXT PRIMARY KEY,
                    metadata TEXT,
                    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
                )
            """)

    def save_metadata(self, file_path, metadata):
        """保存文件元数据"""
        with sqlite3.connect(self.db_path) as conn:
            conn.execute(
                "INSERT OR REPLACE INTO custom_metadata (file_path, metadata) VALUES (?, ?)",
                (file_path, json.dumps(metadata))
            )

    def get_metadata(self, file_path):
        """获取文件元数据"""
        with sqlite3.connect(self.db_path) as conn:
            cursor = conn.execute(
                "SELECT metadata FROM custom_metadata WHERE file_path = ?",
                (file_path,)
            )
            row = cursor.fetchone()
            return json.loads(row[0]) if row else None
```

## 最佳实践

### 错误处理

```python
# 使用项目的异常类
from .util import Pebkac, HttpException

def safe_operation():
    try:
        # 危险操作
        result = risky_function()
    except FileNotFoundError:
        raise Pebkac(404, "文件未找到")
    except PermissionError:
        raise Pebkac(403, "权限不足")
    except Exception as e:
        # 记录详细错误
        self.log("error", f"操作失败: {e}")
        raise HttpException(500, "内部服务器错误")
```

### 配置管理

```python
# 添加新的配置选项
class CustomConfig:
    def __init__(self):
        self.custom_option = False
        self.custom_value = "default"

    def load_from_args(self, args):
        """从命令行参数加载配置"""
        if hasattr(args, 'custom_option'):
            self.custom_option = args.custom_option
        if hasattr(args, 'custom_value'):
            self.custom_value = args.custom_value

    def load_from_config(self, config_dict):
        """从配置文件加载配置"""
        self.custom_option = config_dict.get('custom_option', False)
        self.custom_value = config_dict.get('custom_value', 'default')
```

### 日志记录

```python
# 使用项目的日志系统
def log_custom_event(self, level, message, **kwargs):
    """记录自定义事件"""
    # 格式化消息
    formatted_msg = f"[CUSTOM] {message}"

    # 添加上下文信息
    if kwargs:
        formatted_msg += f" {kwargs}"

    # 使用项目日志方法
    self.log(level, formatted_msg)

# 使用示例
self.log_custom_event("info", "处理自定义请求",
                     user=req.user, path=req.path)
```

### 性能优化

```python
# 使用缓存减少重复计算
from functools import lru_cache
import threading

class PerformanceOptimizer:
    def __init__(self):
        self._cache = {}
        self._lock = threading.Lock()

    @lru_cache(maxsize=1000)
    def expensive_operation(self, input_data):
        """昂贵的计算操作，使用缓存"""
        # 模拟耗时操作
        time.sleep(0.1)
        return f"processed_{input_data}"

    def thread_safe_operation(self, key, value):
        """线程安全的操作"""
        with self._lock:
            self._cache[key] = value
            return self._cache.get(key)
```

### 文档贡献

- 更新 README.md
- 添加配置示例
- 翻译文档
- 改进 API 文档

## 测试策略

### 单元测试

```python
# tests/test_custom.py
import unittest
import tempfile
import os
from copyparty.custom_module import CustomProcessor

class TestCustomProcessor(unittest.TestCase):
    def setUp(self):
        """测试前准备"""
        self.temp_dir = tempfile.mkdtemp()
        self.processor = CustomProcessor(self.temp_dir)

    def tearDown(self):
        """测试后清理"""
        import shutil
        shutil.rmtree(self.temp_dir)

    def test_file_validation(self):
        """测试文件验证功能"""
        # 创建测试文件
        test_file = os.path.join(self.temp_dir, "test.txt")
        with open(test_file, "w") as f:
            f.write("test content")

        # 测试验证
        self.assertTrue(self.processor.validate_file(test_file))

    def test_metadata_extraction(self):
        """测试元数据提取"""
        metadata = self.processor.extract_metadata("test.jpg")
        self.assertIn("format", metadata)
        self.assertEqual(metadata["format"], "JPEG")

if __name__ == "__main__":
    unittest.main()
```

### 集成测试

```python
# tests/test_integration.py
import requests
import subprocess
import time
import threading

class TestIntegration(unittest.TestCase):
    @classmethod
    def setUpClass(cls):
        """启动测试服务器"""
        cls.server_process = subprocess.Popen([
            "python", "-m", "copyparty",
            "--port", "3924",
            "--no-browser"
        ])
        time.sleep(2)  # 等待服务器启动

    @classmethod
    def tearDownClass(cls):
        """停止测试服务器"""
        cls.server_process.terminate()
        cls.server_process.wait()

    def test_upload_download(self):
        """测试上传下载流程"""
        # 上传文件
        files = {"file": ("test.txt", "test content")}
        response = requests.post("http://localhost:3924/upload", files=files)
        self.assertEqual(response.status_code, 200)

        # 下载文件
        response = requests.get("http://localhost:3924/test.txt")
        self.assertEqual(response.status_code, 200)
        self.assertEqual(response.text, "test content")

    def test_api_endpoints(self):
        """测试 API 端点"""
        # 测试文件列表
        response = requests.get("http://localhost:3924/api/ls/")
        self.assertEqual(response.status_code, 200)

        # 测试搜索
        response = requests.get("http://localhost:3924/api/search?q=test")
        self.assertEqual(response.status_code, 200)
```

### 性能测试

```python
# tests/test_performance.py
import time
import concurrent.futures
import requests

class TestPerformance(unittest.TestCase):
    def test_concurrent_uploads(self):
        """测试并发上传性能"""
        def upload_file(file_id):
            files = {"file": (f"test_{file_id}.txt", f"content_{file_id}")}
            start_time = time.time()
            response = requests.post("http://localhost:3924/upload", files=files)
            end_time = time.time()
            return response.status_code, end_time - start_time

        # 并发上传 10 个文件
        with concurrent.futures.ThreadPoolExecutor(max_workers=10) as executor:
            futures = [executor.submit(upload_file, i) for i in range(10)]
            results = [future.result() for future in futures]

        # 验证所有上传成功
        for status_code, duration in results:
            self.assertEqual(status_code, 200)
            self.assertLess(duration, 5.0)  # 每个上传应在 5 秒内完成

    def test_memory_usage(self):
        """测试内存使用情况"""
        import psutil
        import os

        # 获取当前进程
        process = psutil.Process(os.getpid())
        initial_memory = process.memory_info().rss

        # 执行大量操作
        for i in range(1000):
            requests.get("http://localhost:3924/")

        # 检查内存增长
        final_memory = process.memory_info().rss
        memory_growth = final_memory - initial_memory

        # 内存增长应该在合理范围内（例如 < 100MB）
        self.assertLess(memory_growth, 100 * 1024 * 1024)
```

## 部署最佳实践

### 生产环境配置

```yaml
# production.conf
[global]
  # 安全设置
  https: 443
  cert: /etc/ssl/certs/copyparty.crt
  key: /etc/ssl/private/copyparty.key

  # 性能设置
  j: 8                    # 工作线程数
  s-rd-sz: 1048576       # 1MB 读取缓冲区

  # 日志设置
  log-file: /var/log/copyparty/access.log
  log-fk: auth,up2k      # 记录认证和上传日志

  # 安全限制
  ban-pw: 24,5,3600      # 密码错误封禁策略
  max-req: 1000          # 最大请求大小

[accounts]
  admin: $2b$12$encrypted_password_hash

[/public]
  /var/www/public
  accs:
    r: *                 # 公开只读

[/private]
  /var/www/private
  accs:
    rw: admin           # 仅管理员可读写
  flags:
    e2d                 # 启用文件索引
    fk: 8               # 8 字符文件密钥
```

### 系统服务配置

```ini
# /etc/systemd/system/copyparty.service
[Unit]
Description=CopyParty File Server
After=network.target

[Service]
Type=simple
User=copyparty
Group=copyparty
WorkingDirectory=/opt/copyparty
ExecStart=/usr/bin/python3 -m copyparty -c /etc/copyparty/production.conf
Restart=always
RestartSec=10

# 安全设置
NoNewPrivileges=true
PrivateTmp=true
ProtectSystem=strict
ProtectHome=true
ReadWritePaths=/var/www /var/log/copyparty

[Install]
WantedBy=multi-user.target
```

### 监控和日志

```bash
# 日志轮转配置 /etc/logrotate.d/copyparty
/var/log/copyparty/*.log {
    daily
    missingok
    rotate 30
    compress
    delaycompress
    notifempty
    create 644 copyparty copyparty
    postrotate
        systemctl reload copyparty
    endscript
}

# 监控脚本
#!/bin/bash
# /usr/local/bin/monitor-copyparty.sh
LOGFILE="/var/log/copyparty/monitor.log"
PIDFILE="/var/run/copyparty.pid"

check_service() {
    if ! systemctl is-active --quiet copyparty; then
        echo "$(date): CopyParty service is down, restarting..." >> $LOGFILE
        systemctl restart copyparty
    fi
}

check_disk_space() {
    USAGE=$(df /var/www | tail -1 | awk '{print $5}' | sed 's/%//')
    if [ $USAGE -gt 90 ]; then
        echo "$(date): Disk usage is ${USAGE}%, cleaning up..." >> $LOGFILE
        # 清理临时文件
        find /var/www -name "*.tmp" -mtime +1 -delete
    fi
}

check_service
check_disk_space
```

### 备份策略

```bash
#!/bin/bash
# /usr/local/bin/backup-copyparty.sh

BACKUP_DIR="/backup/copyparty"
DATE=$(date +%Y%m%d_%H%M%S)

# 创建备份目录
mkdir -p "$BACKUP_DIR/$DATE"

# 备份配置文件
cp -r /etc/copyparty "$BACKUP_DIR/$DATE/"

# 备份数据库
cp /var/www/.hist/up2k.db "$BACKUP_DIR/$DATE/"

# 备份用户数据（可选，根据数据量决定）
# rsync -av /var/www/data "$BACKUP_DIR/$DATE/"

# 压缩备份
tar -czf "$BACKUP_DIR/copyparty_backup_$DATE.tar.gz" -C "$BACKUP_DIR" "$DATE"
rm -rf "$BACKUP_DIR/$DATE"

# 清理旧备份（保留 30 天）
find "$BACKUP_DIR" -name "*.tar.gz" -mtime +30 -delete

echo "Backup completed: copyparty_backup_$DATE.tar.gz"
```

### 负载均衡配置

```nginx
# /etc/nginx/sites-available/copyparty
upstream copyparty_backend {
    server 127.0.0.1:3923;
    server 127.0.0.1:3924;
    server 127.0.0.1:3925;
}

server {
    listen 80;
    server_name files.example.com;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name files.example.com;

    ssl_certificate /etc/ssl/certs/files.example.com.crt;
    ssl_certificate_key /etc/ssl/private/files.example.com.key;

    client_max_body_size 10G;

    location / {
        proxy_pass http://copyparty_backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;

        # WebSocket 支持
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";

        # 超时设置
        proxy_connect_timeout 60s;
        proxy_send_timeout 60s;
        proxy_read_timeout 60s;
    }
}
```

## 许可证

MIT License - 详见 LICENSE 文件

---

*本指南持续更新中，欢迎贡献改进建议！*
