# AD Manager · 公开文档与 Releases

本仓库**仅**托管：

- **使用教程**（Windows / macOS 本地部署、功能介绍、发版约定）
- **版本迭代安装包**（[GitHub Releases](https://github.com/Aidan-996/ad-manager-releases/releases)）

**不含应用程序源码。** 源码仓库为私有：`Aidan-996/ad-manager`（基础版）、`Aidan-996/ad-manager-pro`（专业版）。

应用内「检查更新」默认查询本仓库 Releases；典型用户**无需** GitHub Token。当前对外：**v23.2.10**。

| 文档 | 说明 |
|---|---|
| [docs/FEATURES.md](./docs/FEATURES.md) | 功能介绍与档位对照 |
| [docs/WINDOWS-LOCAL.md](./docs/WINDOWS-LOCAL.md) | Windows 本地安装 / 更新 / 重置 |
| [docs/MACOS-LOCAL.md](./docs/MACOS-LOCAL.md) | macOS 本地包 |
| [docs/RELEASES.md](./docs/RELEASES.md) | 发版约定与在线更新说明 |
| [docs/architecture.md](./docs/architecture.md) | 三仓与交付模型公开摘要 |

## 下载

→ **[Releases](https://github.com/Aidan-996/ad-manager-releases/releases)**（当前 tag：**v23.2.10**）

- 基础版：`ad-manager-*`（排除 `ad-manager-pro-*`）
- 专业版：`ad-manager-pro-*`（需有效授权解锁增值功能）

推荐 Windows：`*-windows-amd64-setup.exe`（同目录覆盖安装，保留 `data/`）。  
推荐 macOS：`*-darwin-*.dmg`。

首次登录：`admin` / `admin123`（登录后强制改密）。

## 版本摘要

| 版本 | 要点 |
|---|---|
| v23.2.10 | **统一安装包**：单一 setup；.lic 解锁 Pro；保留多点 live 重验签 |
| v23.2.9 | 多点授权闸门（live 重验签，防单点 bypass） |
| v23.2.8 | API 令牌（Bearer）；脚本免 CSRF 调用 REST |
| v23.2.7 | 仪表盘待处理卡片；NSIS 组件页/卸载删 data；一键应用更新 |
| v23.2.6 | 默认更新源为本仓；源码仓改回私有；旧客户端需手动下载一次 |
| v23.2.5 | 在线更新指向本公开 Releases；功能介绍文档对齐授权页 |
| v23.2.4 | 自签名 Authenticode；授权页档位说明 |
| v23.2.3 | 覆盖安装后 admin/admin123 可登录 |
| v23.2.2 | 登录 CSRF 修复 + Windows 无黑窗 |
| v23.2.1 | 本地欢迎页 + 初始密码 admin123 |
| v23.2.0 | 深色科技风安装包 + macOS DMG |
| v23 | 授权密钥轮换；旧 .lic 失效需重签 |

更细说明见各 Release 正文与 `docs/`。

许可证：本仓文档与教程文件见根目录 [LICENSE](./LICENSE)；应用程序按安装包所附许可与商业条款。
