# emby-nginx 助手

[![Docker Pulls](https://img.shields.io/docker/pulls/yantaocheng/emby-nginx.svg)](https://hub.docker.com/r/yantaocheng/emby-nginx)
[![GitHub stars](https://img.shields.io/github/stars/Yongzz668/emby-nginx.svg)](https://github.com/Yongzz668/emby-nginx/stargazers)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

**emby-nginx 助手** 是一款专为115网盘、123云盘登录，Emby媒体服务器设计的专业级 Nginx 直链反代工具，支持 Docker、Windows安装 多网盘登录，多媒体服务器直链播放及 STRM 文件极速生成。

🌐 emby-nginx 助手 官方网站：
[https://6080808.xyz](https://6080808.xyz)

---

## 📄 版本更新日志
[📄 emby-nginx更新日志](./CHANGELOG.md)

## 📌 tg群 / 教程

[![Telegram](https://img.shields.io/badge/Telegram-加入群-blue?logo=telegram)](https://t.me/Embynginx)  
[![Bilibili](https://img.shields.io/badge/B站-教程-red?logo=bilibili)](https://b23.tv/pwru3We)  
[![腾讯文档](https://img.shields.io/badge/腾讯文档-教程-green?logo=tencentdocs)](https://docs.qq.com/doc/DTHVTcHRwb3pJdk1D)

---
## 核心功能 

### 🔒 安全保护
- 启用程序自锁机制，超过五次输错密码程序自锁，需手动重启容器
- 网盘 Cookie、账号密码、API 密钥默认防查看、防复制，保护密保不被泄露

### ⚡ 自动化配置
- 扫 115 网盘二维码登录 Cookie 各端  
- 支持官方认证 115 网盘 Open 与 123 云盘 Open  
- 支持115 网盘或 123 云盘直链播放及strm极速生成 
- 直接解析openlist生成的网盘 STRM 文件直链播放
- 支持生成保存在网盘的所有音乐格式对应strm文件
  
### 🔍 实时监控
- 基于事件通知实时监控 115 网盘文件变动  
- 实时同步生成或删除 STRM 文件  
- 基于 CD2Webhook 实时监控生成/删除 123 云盘 STRM 文件  
- STRM 文件增减秒级驱动 Emby 刷新海报墙

### 📱 多平台支持
- 完美适配 Emby、Jellyfin、飞牛影视、极影视  
- 支持芝度、绿联、Infuse、Vidhub 等主流播放器

### 🎬 媒体信息探测
- 实时生成 STRM 追更探测文件媒体信息  
- 支持网盘存放字幕图片NFO文件自动下载
- 生成网盘音乐文件的strm文件

### 🤖 微信机器人
- 企业微信 Webhook 通知 STRM 生成/更新提醒  
- 发送各工具任务完成通知，追更探测媒体信息加快入库速度
- Emby 入库/播放通知，观影账户反馈登录城市 IP，避免不明异地 302 播放风控

### ☁️ WebDAV 支持
- 通过 5002 端口开启 WebDAV 服务，挂载外网STRM文件  
- 挂载给芝度、腾讯极光、Infuse、Vidhub 等播放器直接刮削封面并在线播放

### 🚀 123 云盘特别支持
- 生成 123 云盘反代直链播放，生成STRM文件  
- 支持 115 网盘资源无需下载直接离线至 123 云盘

---

## 独家高价值功能 

### 🎯 快速生成 ED2K 链接
- 独创选择模式和实时监控 115 网盘文件的 ED2K 链接  
- 多元化分享方式，记录方式

### 🔄 115 转 123 云盘
- 灵活选择 115 文件高速离线至 123 云盘  
- 跨网盘资源高速迁移，每小时1T迁移

### 👥 多设备同时播放
- 同一网盘视频文件同时支持最高 7 个设备在线播放  
- A文件复制1A 2A 3A 4A 5A 6A直链播放避免302限制

### ⚖️ 多账号负载均衡
- 多个网盘账号挂载均衡使用，避免风控  
- A号B号C号智能交替播放保证播放稳定性

### 🔄 多服务器反代
- Nginx 同时反代多个 Emby/Jellyfin 与飞牛影视  
- 同时反代多个emby服务器+飞牛影视直链播放

### 💾 硬链接轮询监控
- 利用硬链接轮询监控，实现秒传文件至网盘  
- 上传宽带0占用，避免家宽上传大被封控

### 🔧 精准媒体信息探测
- 内置 Emby 媒体文件信息探测扫描（全量 + 追更探测）  
- 加快起播速度，文件媒体信息完整展示
- 和神医助手媒体信息提取功能类似

### 🌐 远程 STRM 挂载
- 内置 WebDAV 将 STRM 文件远程挂载识别刮削  
- 实现跨设备识别与刮削

### 📄 独创扩展名STRM文件
- 同一文件夹内同名多版本视频，生成 mp4.strm、mkv.strm、iso.strm
- 保证同文件夹所有视频文件都可以生成strm文件，防生成遗漏
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

| 本地端口 | 容器端口 | 功能说明 |
|-----------|----------|----------|
| 9527      | 9527     | 管理后台访问端口，STRM 文件外网访问的前缀通道 |
| 7001      | 7001     | 反向代理 Emby/Jellyfin 的 8096 端口，实现302直链播放 |
| 5002      | 5002     | WebDAV 服务端口，支持播放器直接挂载刮削外网strm |
| 8021      | 8001     | 飞牛影视专用反代直链播放端口 |

### 📂 STRM 文件目录说明

| STRM存放目录             | 适用说明 |
|---------------------|----------|
| /strm/local          | 本机 Emby/Jellyfin 容器映射的 STRM 文件目录 |
| /strm/online         | 外部播放器使用的 STRM 文件，通过 WebDAV 挂载 |
| /strm/openlist       | 存放基于挂载在 openlist 网盘的 STRM 文件 |

## STRM 文件说明

7001直链端口可解析播放的前缀路径的 STRM 文件

### 本地与外网访问前缀

- **本地 HTTP 前缀**: [http://192.168.100.1:9527](http://192.168.100.1:9527)  
- **外网 HTTPS 前缀**: [https://ABC.xyz:9527反代端口](https://ABC.xyz:9527)  

### Cd2 挂载路径与直链

- **Cd2 挂载路径前缀**: /CloudNAS/CloudDrive  
- **Cd2 302 直链前缀**: [http://192.168.100.1:19798](http://192.168.100.1:19798)  

---

### Openlist STRM

- **Openlist 前缀**: [http://192.168.100.1:5244/d](http://192.168.100.1:5244/d)  
- Openlist 生成的 STRM 文件直接解析7001端口播放

---

### 支持安装 emby-nginx助手 的设备

- X86 架构的 NAS 或软路由  
- ARM 架构的 NAS 或软路由  
- VPS 云服务器  
- Windows 系统电脑



---
本工具为付费获取激活码本地永久激活工具，激活前有24小时所有功能无限制试用期，请安装试用期满以后再行慎重考虑是否购买激活码永久使用。
## 📱 关注微信公众号
扫码关注获取购买激活码帮助

<p align="center">
  <img src="https://cdn.jsdelivr.net/gh/Yongzz668/image@main/assets/IMG_8887.jpeg" alt="关注公众号" width="120">
</p>

**提示**：请用微信扫描二维码关注公众号

使用声明（重要）

本工具仅用于帮助使用者合理利用其自有网盘账户与相关功能，使用前请务必阅读并理解以下条款。

	1.	工具用途限定
	•	本工具仅在帮助使用者合理利用自有网盘账户文件的情况下使用，利用 .strm 特性减少网盘访问服务器压力；利用网盘的 302 重定向特性减少使用者家庭上传带宽占用；并利用 nginx 特性降低配置难度。
	2.	不承担第三方资源管理责任
	•	本工具不涉及对网盘文件本身的删除或修改，也不帮助使用者搜索或转存第三方人员文件。如因网盘文件减少或丢失导致任何损失，本工具不承担相应责任。
	3.	不涉及整理/重命名/刮削行为
	•	本工具不对（音）视频文件进行重命名、刮削元数据、或拉取相关节目（专辑）的海报与人物头像等。如有涉及侵犯版权的功能或行为，请及时联系开发者反馈处理。
	4.	无法提供 VPN 功能服务
	•	本工具不包含任何 VPN 功能，亦无法帮助解决 VPN 相关网络问题，请知晓。
	5.	激活与付费说明
	•	本工具的激活机制为：通过激活码在使用者本地进行永久激活，激活后无法远程注销或踢出使用权限。故不接受任何形式的退费请求；请在付费获取激活码前慎重考虑。
	6.	风控（封控）合规提示
	•	115 网盘与 123 云盘存在严格且严肃的异地 302 风控（封控）规则，请务必在相关网盘服务商规则范围内使用本工具并遵守其条款。
	7.	遵纪守法
	•	请务必遵守法律法规。若使用本工具主动从事任何非法活动，工具开发者或运营者对此毫不知情，则使用者自行承担相应责任。
