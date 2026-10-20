# AD Manager · 公开文档与 Releases

本仓库**仅**托管：

- **使用教程**（Windows / macOS 本地部署、功能介绍）
- **版本迭代安装包**（[GitHub Releases](https://github.com/Aidan-996/ad-manager-releases/releases)）

**不含应用程序源码。** 源码仓库为私有：`Aidan-996/ad-manager`（基础版）、`Aidan-996/ad-manager-pro`（专业版）。

应用内「检查更新」默认查询本仓库 Releases；典型用户**无需** GitHub Token。

| 文档 | 说明 |
|---|---|
| [docs/FEATURES.md](./docs/FEATURES.md) | 功能介绍与档位对照 |
| [docs/WINDOWS-LOCAL.md](./docs/WINDOWS-LOCAL.md) | Windows 本地安装 / 更新 / 重置 |
| [docs/MACOS-LOCAL.md](./docs/MACOS-LOCAL.md) | macOS 本地包 |
| [docs/RELEASES.md](./docs/RELEASES.md) | 发版约定与在线更新说明 |

## 下载

→ **[Releases](https://github.com/Aidan-996/ad-manager-releases/releases)**（当前对外：见最新 tag）

- 基础版：`ad-manager-*`（排除 `ad-manager-pro-*`）
- 专业版：`ad-manager-pro-*`（需有效授权解锁增值功能）

推荐 Windows：`*-windows-amd64-setup.exe`（同目录覆盖安装，保留 `data/`）。

首次登录：`admin` / `admin123`（登录后强制改密）。

## 版本摘要

| 版本 | 要点 |
|---|---|
| v23.2.5+ | 在线更新指向本公开 Releases 仓；功能介绍文档对齐授权页 |
| v23.2.4 | 自签名 Authenticode；授权页档位说明 |
| v23.2.3 | 覆盖安装后 admin/admin123 可登录 |
| v23.2.2 | 登录 CSRF 修复 + Windows 无黑窗 |
| v23.2.1 | 本地欢迎页 + 初始密码 admin123 |
| v23.2.0 | 深色科技风安装包 + macOS DMG |
| v23 | 授权密钥轮换；旧 .lic 失效需重签 |

更细说明见各 Release 正文与 `docs/`。
