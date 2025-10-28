# Emby-Nginx 助手

[![Docker Pulls](https://img.shields.io/docker/pulls/yantaocheng/emby-nginx.svg)](https://hub.docker.com/r/yantaocheng/emby-nginx)
[![GitHub stars](https://img.shields.io/github/stars/Yongzz668/emby-nginx.svg)](https://github.com/Yongzz668/emby-nginx/stargazers)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**Emby-Nginx 助手** 是一款专为 Emby、Jellyfin 等媒体服务器设计的专业级 Nginx 反向代理工具，支持 Docker 一键部署、HTTPS 安全访问控制、多设备直链播放及 STRM 文件管理。

🌐 官方网站：[https://6080808.xyz](https://6080808.xyz)

---

## 📌 官方资源 / 官方教程

[![Telegram](https://img.shields.io/badge/Telegram-加入群-blue?logo=telegram)](https://t.me/Embynginx)  
[![Bilibili](https://img.shields.io/badge/B站-教程-red?logo=bilibili)](https://b23.tv/pwru3We)  
[![腾讯文档](https://img.shields.io/badge/腾讯文档-教程-green?logo=tencentdocs)](https://docs.qq.com/doc/DTHVTcHRwb3pJdk1D)

---
## 核心功能 

### 🔒 安全保护
- 启用程序自锁机制，超过五次输错密码程序自锁  
- 网盘 Cookie、账号密码、API 密钥默认防查看、防复制，保护密保不被泄露

### ⚡ 自动化配置
- 扫 115 网盘二维码登录 Cookie 各端  
- 支持官方认证 115 网盘 Open 与 123 云盘 Open  
- 支持直链播放及strm生成 115 网盘或 123 云盘  
- 自动生成基于 openlist 的网盘 STRM 文件并提供直链播放

### 🔍 实时监控
- 基于事件通知实时监控 115 网盘文件变动  
- 自动同步生成或删除 STRM 文件  
- 基于 CD2Webhook 实时监控生成/删除 123 云盘 STRM 文件  
- STRM 文件增减秒级同步刷新 Emby 海报墙

### 📱 多平台支持
- 完美适配 Emby、Jellyfin、飞牛影视、极影视  
- 支持芝度、绿联、Infuse、Vidhub 等主流播放器

### 🎬 媒体信息获取
- 实时生成 STRM 并探测文件媒体信息  
- 支持字幕文件自动下载

### 🤖 微信机器人
- 企业微信 Webhook 通知 STRM 生成/更新提醒  
- Cookie 失效自动提醒并重新生成二维码  
- Emby 入库/播放通知，观影账户反馈登录城市 IP，避免不明异地 302 风控

### ☁️ WebDAV 支持
- 通过 5002 端口开启 WebDAV 服务  
- 支持芝度、腾讯极光、Infuse、Vidhub 等播放器直接刮削封面并在线播放

### 🚀 123 云盘特别支持
- 生成 123 云盘反代直链播放  
- 支持 115 网盘资源无需下载直接离线至 123 云盘

---

## 独家功能 

### 🎯 快速生成 ED2K 链接
- 独创选择模式和实时监控 115 网盘文件的 ED2K 链接  
- 多元化分享方式

### 🔄 115 转 123 云盘
- 灵活选择 115 文件高速离线至 123 云盘  
- 实现跨网盘资源高速迁移

### 👥 多设备同时播放
- 同一网盘视频文件同时支持 7 个设备在线播放  
- 满足家庭共同观影需求

### ⚖️ 多账号负载均衡
- 多个网盘账号挂载均衡使用  
- 提升系统稳定性与性能

### 🔄 多服务器反代
- Nginx 同时反代多个 Emby/Jellyfin 与飞牛影视  
- 统一反代多个媒体服务器直链播放

### 💾 硬链接轮询监控
- 利用硬链接轮询监控，实现秒上传文件  
- 节省上传宽带占用，避免家宽被封控

### 🔧 精准媒体信息探测
- 内置 Emby 媒体文件信息探测线程（全量 + 追更探测）  
- 确保秒起播与媒体信息完整性

### 🌐 远程 STRM 挂载
- 内置 WebDAV 将 STRM 文件远程挂载识别刮削  
- 实现跨设备识别与刮削

---

## 🐳 Docker CLI 部署示例
```
docker run -d   --name emby-nginx \                        # 容器名称
  -p 7001:7001 \                             # 反向代理 Emby/Jellyfin 8096 端口
  -p 8021:8001 \                             # 飞牛影视系统专用直链反代端口
  -p 9527:9527 \                             # 管理后台访问端口
  -p 5002:5002 \                             # WebDAV 服务端口
  -v /vol1/1000/emby-nginx/strm:/strm \     # STRM 文件映射
  -v /vol1/1000/emby-nginx/backup:/app/backup \  # 备份目录
  --network bridge   --restart unless-stopped   --privileged   yantaocheng/emby-nginx:latest
  ```

---

## 🐳 Docker Compose 部署示例

```yaml
version: '3.8'

services:
  emby-nginx:
    image: yantaocheng/emby-nginx:latest
    container_name: emby-nginx
    ports:
      - "7001:7001"    # 反向代理 Emby/Jellyfin 8096 端口
      - "8021:8001"    # 飞牛影视系统专用直链反代端口
      - "9527:9527"    # 管理后台访问端口
      - "5002:5002"    # WebDAV 服务端口
    volumes:
      - /vol1/1000/emby-nginx/strm:/strm       # STRM 文件映射
      - /vol1/1000/emby-nginx/backup:/app/backup  # 备份目录
    network_mode: bridge
    restart: unless-stopped
    privileged: true
```
---

### 🔌 端口说明

| 容器端口 | 主机端口 | 功能说明 |
|-----------|----------|----------|
| 9527      | 9527     | 管理后台访问端口，STRM 文件外网访问的前缀通道 |
| 7001      | 7001     | 反向代理 Emby/Jellyfin 的 8096 端口，实现302直链播放 |
| 5002      | 5002     | WebDAV 服务端口，支持播放器直接挂载刮削外网strm |
| 8021      | 8001     | 飞牛影视专用反代直链播放端口 |

### 📂 STRM 文件目录说明

| 目录路径             | 功能说明 |
|---------------------|----------|
| /strm/local          | 本机 Emby/Jellyfin 容器映射的 STRM 文件目录 |
| /strm/online         | 外部播放器使用的 STRM 文件，通过 WebDAV 挂载 |
| /strm/openlist       | 存放基于挂载在 openlist 网盘的 STRM 文件 |



## 📄 更新日志
[📄 查看更新日志](./CHANGELOG.md)

---
本工具为付费本地永久激活工具，激活购买前有24小时所有功能无限制试用期，请安装试用期满以后再行慎重考虑是否购买激活码永久使用。
## 📱 关注微信公众号
扫码关注获取购买激活码帮助

<p align="center">
  <img src="https://cdn.jsdelivr.net/gh/Yongzz668/image@main/assets/IMG_8887.jpeg" alt="关注公众号" width="120">
</p>

**提示**：请用微信扫描二维码关注公众号

