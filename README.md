# 网络安全扫描工具

## 概述

这是一个基于 [Flask](https://flask.palletsprojects.com/) 的 Web 应用程序，用于网络安全扫描和分析，帮助用户识别漏洞和潜在威胁。

## 功能

- **目录扫描**：使用字典文件扫描目标 URL 的可访问目录。
- **SQL 注入扫描**：集成 [SQLMap](https://sqlmap.org/) 检测 SQL 注入漏洞。
- **日志分析**：分析日志文件，提取恶意 IP、域名、JNDI 攻击负载等。
- **网络扫描**：使用 FScan 扫描开放端口、服务和漏洞。
- **弱密码扫描**：尝试破解 Web 登录表单的弱密码。

## 安装

1. 克隆仓库：

   ```bash
   git clone <repository_url>
   ```

2. 安装依赖：

   ```bash
   pip install -r requirements.txt
   ```

3. 项目已包含 SQLMap（`sqlmap-master`）和 FScan（`sm`），无需单独安装。

## 配置

配置文件为 `config.py`，主要设置包括：

| 配置项               | 描述                 | 默认值                                |
| -------------------- | -------------------- | ------------------------------------- |
| `SECRET_KEY`         | 安全密钥             | `dev-key-please-change-in-production` |
| `SQLMAP_PATH`        | SQLMap 脚本路径      | `sqlmap-master/sqlmap.py`             |
| `FSCAN_PATH`         | FScan 可执行文件路径 | `sm/sm.exe`                           |
| `UPLOAD_FOLDER`      | 上传文件存储目录     | `uploads`                             |
| `MAX_DIR_DEPTH`      | 目录扫描最大深度     | `3`                                   |
| `SCAN_TIMEOUT`       | 扫描超时时间（秒）   | `5`                                   |
| `MAX_WORKERS`        | 最大工作进程数       | `10`                                  |
| `ALLOWED_EXTENSIONS` | 允许的文件扩展名     | `{'txt', 'log'}`                      |

## 运行

1. 运行启动脚本：

   ```bash
   start.bat
   ```

   或直接运行：

   ```bash
   python app.py
   ```

2. 在浏览器访问 `http://localhost:5000`。

## 使用

1. 打开 Web 界面，选择扫描类型（如目录扫描）。
2. 输入目标 URL 或上传字典文件/日志文件。
3. 启动扫描，获取任务 ID。
4. 通过 `/scan-status/<job_id>` 查看扫描状态，或 `/stop-scan/<job_id>` 停止扫描。

## 依赖

| 包名          | 版本   |
| ------------- | ------ |
| Flask         | 2.3.3  |
| requests      | 2.31.0 |
| python-dotenv | 1.0.0  |
| Werkzeug      | 2.3.7  |
| urllib3       | 2.0.4  |
| cryptography  | 41.0.3 |
| Flask-WTF     | 1.1.1  |
| Flask-Login   | 0.6.2  |
| gunicorn      | 21.2.0 |


## 注意事项

- 用户需提供字典文件用于目录和弱密码扫描。

- 生产环境建议使用 [Gunicorn](https://gunicorn.org/)：

  ```bash
  gunicorn app:app
  ```

- 应用程序包含错误处理机制，支持验证错误、文件错误和超时处理。

- 日志记录在 `app.log` 中，级别为 `INFO`。

## 贡献

欢迎贡献代码！请 fork 仓库，创建功能分支，并提交拉取请求。
