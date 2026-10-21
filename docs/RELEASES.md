# 发版与在线更新（公开 Releases）

本仓库是**唯一对外**的教程 + 安装包托管处；**不含源码**。当前对外版本：**v23.2.12**。

## 原则

- **所有客户面向的检查更新 / 下载**默认走本仓库  
  [`Aidan-996/ad-manager-releases`](https://github.com/Aidan-996/ad-manager-releases/releases)  
  **不需要** `ADMANAGER_GH_TOKEN`。
- **统一包**（v23.2.10+）同一 tag 主推：
  - **主安装包**：`ad-manager-*`（setup.exe / zip / dmg）— 含 Pro 代码；导入授权解锁
  - **过渡别名**（可选）：`ad-manager-pro-*`（与主包同内容）
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


## 升级路径（→ 统一包）

| 来源 | 做法 |
|---|---|
| 旧基础版（`ADManager`） | 运行新 `ad-manager-*-setup.exe` 覆盖同一目录；保留 `data/` |
| 旧专业版（`ADManagerPro`） | 退出进程 → 复制 `data/` 到 `%LOCALAPPDATA%\ADManager\data` → 安装统一 setup；勿并行运行（端口 9443） |
| 授权 | 已导入的 `.lic` 随 `data/` 保留 |
