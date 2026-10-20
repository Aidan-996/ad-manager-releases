# 发版与在线更新（公开 Releases）

本仓库是**唯一对外**的教程 + 安装包托管处；**不含源码**。当前对外版本：**v23.2.6**。

## 原则

- **所有客户面向的检查更新 / 下载**默认走本仓库  
  [`Aidan-996/ad-manager-releases`](https://github.com/Aidan-996/ad-manager-releases/releases)  
  **不需要** `ADMANAGER_GH_TOKEN`。
- 基础版与专业版**共用同一 tag**（如 `v23.2.6`）的 Release；用资源名区分：
  - 基础版：`ad-manager-<ver>-windows-amd64-setup.exe` / `.zip` / `darwin-*.dmg` …
  - 专业版：`ad-manager-pro-<ver>-windows-amd64-setup.exe` / `.zip` / `darwin-*.dmg` …
- 源码在私有仓 `ad-manager` / `ad-manager-pro`；**产物只上传到本公开 Release**。
- 企业若必须改仓库：环境变量 `ADMANAGER_UPDATE_REPO=owner/name`；私有仓再设 `ADMANAGER_GH_TOKEN`。

## 应用内行为

| 构建 | 查询仓库 | 选用资源 |
|---|---|---|
| 基础版 | `Aidan-996/ad-manager-releases` | 前缀 `ad-manager-`（排除 `ad-manager-pro-`） |
| 专业版（`-tags pro`） | 同上 | 前缀 `ad-manager-pro-` |

无 Token 时下载优先使用 GitHub `browser_download_url` 直链。

## 维护者上传步骤（摘要）

1. 本仓打 tag / 建 Release（中文说明）。
2. 上传基础版 `ad-manager-*` 与对应 `.sha256`。
3. 私有仓产出 `ad-manager-pro-*` 后，**附到同一本仓 Release**。
4. 客户在「授权与版本 → 检查更新」即可拉取；若该 tag 尚无对应前缀资源，界面提示无适合安装包。

## 相关文档

- [WINDOWS-LOCAL.md](./WINDOWS-LOCAL.md) · [MACOS-LOCAL.md](./MACOS-LOCAL.md) · [FEATURES.md](./FEATURES.md) · [architecture.md](./architecture.md)
