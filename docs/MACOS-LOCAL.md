# macOS 本地版（.app / DMG）

本包将 AD 域系统管理平台以 macOS 应用形式运行在本机，**无需 nginx / 无需 Linux 服务器**。

Copyright (c) 2026 AD Manager

## 推荐：DMG 安装

1. 下载 Release 中的 `ad-manager-*-darwin-arm64.dmg`（Apple Silicon）或 `*-darwin-amd64.dmg`（Intel）。
2. 打开 DMG，将 **AD Manager.app** 拖到 **Applications**。
3. 首次打开：若提示未验证开发者，可在「系统设置 → 隐私与安全性」中允许，或右键 → 打开。
4. 启动后自动在浏览器打开 `https://127.0.0.1:9443/`（短欢迎页；点「进入管理界面」进入管理 SPA。自签名证书需「继续访问」。包内 README 不会嵌在网页里）。

专业版资源名为 `ad-manager-pro-*-darwin-*.dmg`，应用名为 **AD Manager Pro.app**。

## 便携 zip

解压 `ad-manager-*-darwin-*.zip` 后，可双击包内 `启动.command`，或直接打开 `.app`。

## 目录结构（.app）

```
AD Manager.app/Contents/
  MacOS/admanager     # 后端（默认本地模式）
  MacOS/data/         # 首次运行后自动创建（配置、数据库、证书）
  Resources/web/      # 前端静态资源
  Resources/LICENSE
  Resources/README.md
  Info.plist          # 含 NSHumanReadableCopyright
```

## 登录

- 用户名：**admin**
- 初始密码：**固定为 `admin123`**（首次登录必须修改）；亦可查看
  `AD Manager.app/Contents/MacOS/data/initial-admin-password`
- **覆盖升级**：保留 `data/`。若 admin 仍待改密（含旧版随机初始密码），v23.2.3+ 启动时会同步为 `admin123`；已改密账号不变。忘记密码：`reset-admin`（默认 admin123）或删除 `data/`。

## 常用参数

在终端中：

```bash
"/Applications/AD Manager.app/Contents/MacOS/admanager" -http
"/Applications/AD Manager.app/Contents/MacOS/admanager" -listen 127.0.0.1:8443
"/Applications/AD Manager.app/Contents/MacOS/admanager" fingerprint
```

## 与 Windows 本地版

行为与 [WINDOWS-LOCAL.md](WINDOWS-LOCAL.md) 一致：本机 HTTPS、自动打开浏览器、配置在可执行文件旁 `data/`。无服务器部署步骤。
