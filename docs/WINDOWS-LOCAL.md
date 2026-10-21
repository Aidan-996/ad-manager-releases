> **统一包 v23.2.10**：一份安装；`.lic` 解锁 Pro；覆盖保留 `data/`。旧专业版目录为 `ADManagerPro`，请迁移 `data/` 到 `ADManager` 后再装统一包。

## 系统要求

- 提供 **64 位（`windows-amd64`）** 与 **32 位（`windows-386`）** 安装包，请按系统位数下载。
- 最低：**Windows Server 2012 R2** / **Windows 8.1** 或更新（推荐 Server 2012 R2 x64 或 Windows 10 / Server 2016+）。
- 若提示「此应用无法在你的电脑上运行」：先确认下载了匹配的 amd64/386 包；仍失败请升级系统。


## 目录结构

```
ad-manager-*-windows-amd64/
  admanager.exe   # 后端（默认开启本地模式）
  启动.bat         # 推荐：检查 web/ 后启动；失败时暂停窗口
  web/            # 前端静态资源（勿改名、勿挪走；须含 index.html）
  README.md       # 本说明
  data/           # 首次运行后自动创建（配置、数据库、自签名证书）
```

> **推荐下载 `*-setup.exe` 安装包**：一键安装到 `%LOCALAPPDATA%\ADManager`，创建开始菜单快捷方式（安装向导组件页可勾选桌面快捷方式），并自动启动（会打开浏览器）。  
> 也可下载 `.zip` 解压后运行。Release 中单独的裸 `.exe`（非 setup）不含 `web/`，双击会因缺少前端而退出（现已弹窗提示）。

## 如何安装（推荐）

1. 下载 Release 中的 `ad-manager-*-windows-amd64-setup.exe`（专业版为 `ad-manager-pro-*-setup.exe`）。
2. 双击运行安装向导（无需管理员；默认安装到 `%LOCALAPPDATA%\ADManager`）。
3. 安装结束后会自动启动并打开浏览器；亦可从桌面或开始菜单的「AD 域管理平台」快捷方式启动。
4. 卸载：开始菜单 → 卸载，或「应用和功能」中卸载（默认保留 `data/` 配置与数据库）。

## 如何运行（zip 便携包）

1. 解压 zip 到任意目录（建议路径无中文空格亦可）。
2. **双击 `启动.bat` 或 `admanager.exe`**（或在 PowerShell / CMD 中运行）。
3. 程序会：
   - 在 `127.0.0.1:9443` 启动 **HTTPS**（自签名证书，保存在 `data/tls/`）
   - 自动打开系统默认浏览器访问 `https://127.0.0.1:9443/`（短欢迎页；点「进入管理界面」进入管理 SPA。包内 `README.md` 仍为解压/安装说明，不会嵌在网页里）
4. 首次打开浏览器会提示证书不受信任：选择「高级」→「继续访问」即可（仅本机自签名）。
5. 使用本地管理员 **admin** 登录；**首次初始密码固定为 `admin123`**（首次登录必须修改）。亦可打开：
   - **`data\initial-admin-password`**（相对 exe 所在目录）核对；改密后该文件自动删除。

若启动失败（缺 `web/`、端口占用、其它错误），会弹出错误对话框（无需黑 CMD 窗口）。

自 **v23.2.14** 起（侧栏「软件更新」；授权页精简）。自 **v23.2.13** 起（授权页锁定能力预览显示「需导入授权」；在线更新若 DNS 失败有中文提示，可配置镜像或上传离线包）：再次打开或覆盖安装后启动时，若 `127.0.0.1:9443` 仍被另一份 AD Manager（`admanager.exe`）占用，新进程会先结束旧实例再绑定。仅当端口被无关程序占用时提示关闭该程序或使用 `-listen`。

## 覆盖安装与「用户名或密码错误」

安装程序 / zip **默认保留 `data/`**（配置、SQLite、证书）。因此：

| 场景 | 登录方式 |
|---|---|
| **全新安装**（无 `data/` 或空库） | `admin` / `admin123`，首次登录必须改密 |
| **覆盖升级且从未改过初始密码**（`must_change=1`，含旧版随机初始密码） | 自 v23.2.3 起启动时会把仍待改密的 `admin` 同步为 `admin123`；用 `admin` / `admin123` 登录后改密 |
| **已经改过密码**（`must_change=0`） | 继续用你自己的密码；**不会**被重置为 admin123 |
| **忘记已改密码** | 见下方「重置 admin」；或退出进程后删除安装目录下整个 `data/` 再启动（等同全新安装，配置与授权均丢失） |

### 重置 admin（保留其它配置）

在安装目录打开「终端」或 PowerShell：

```text
.\admanager.exe reset-admin
```

默认将 `admin` 重置为 **`admin123`**（`must_change=1`），并写入 `data\initial-admin-password`。可选：

```text
.\admanager.exe reset-admin -password MyTempPass99
.\admanager.exe reset-admin -random
```

（GUI 子系统下若无输出，请从已打开的终端运行；密码亦可查看 `data\initial-admin-password`。）


自 v23.2.2 起，Windows 本地 exe 使用 **GUI 子系统**：双击启动**不再弹出黑色控制台**；访问日志与启动信息写入 `data/admanager.log`（不在屏幕显示）。停止服务：在任务管理器结束 `admanager.exe`，或关闭安装器/快捷方式启动的进程。配置与数据库均在 `data/` 目录，升级时保留该目录即可。

## 常用参数

```text
admanager.exe                      # 默认：本地 HTTPS + 打开浏览器
admanager.exe -http                # 改用 HTTP（http://127.0.0.1:9443/），Cookie 不设 Secure
admanager.exe -listen 127.0.0.1:8443
admanager.exe -no-browser          # 不自动打开浏览器
admanager.exe -web D:\path\to\web  # 指定前端目录
admanager.exe -config D:\adm-data  # 指定配置目录（默认 exe 旁 data/）
admanager.exe fingerprint          # 打印机器指纹与实例 ID（申请专业版授权用）
admanager.exe reset-admin          # 重置本地 admin 为 admin123（可用 -password / -random）
```

## 连接 Active Directory

本机需能访问域控（LDAPS 636 / StartTLS / 389）。在「系统设置 → AD 连接」中填写域控地址与绑定账号。若本机不在域内，请确保网络路由与防火墙放行。

## 与 Linux 服务器版的区别

| | Windows 本地版 | Linux 服务器版 |
|---|---|---|
| 入口 | 本机浏览器 → exe 直服 HTTPS/HTTP | nginx HTTPS → 后端 |
| 配置目录 | exe 旁 `data/` | `/etc/admanager` |
| 适用 | 单机运维、演示、小型环境 | 生产多用户、systemd 常驻 |

Linux 安装仍请使用 Release 中的 `install.sh` 包（本 zip 仅面向 Windows 本地）。

## 软件更新（应用内检查 / 下载）

1. 以本地超级管理员登录，打开侧栏「系统设置 → 软件更新」。
2. 点「检查更新」：后端查询公开仓库 [Aidan-996/ad-manager-releases Releases](https://github.com/Aidan-996/ad-manager-releases/releases)（**基础版与专业版相同**）。**无需** `ADMANAGER_GH_TOKEN`；需能访问 GitHub（企业可设代理，或用 `ADMANAGER_UPDATE_REPO` 覆盖）。
3. 若有新版本，优先选择带「推荐」标记的包：基础版为 `ad-manager-*-setup.exe`，专业版为 `ad-manager-pro-*-setup.exe`（其次 zip / dmg），点「下载到本机」。文件保存到 `data/updates/`；有 GitHub `digest` 或同名 `.sha256` 时自动校验。
4. **推荐**：下载完成后点「一键应用并重启」——自动替换安装目录中的 `admanager.exe` 与 `web/`，**保留 `data/`**，并重启进程。`*-setup.exe` 会静默覆盖安装到当前目录；zip / 裸 exe 由应用内直接替换。
5. **亦可手工**：退出进程后运行 `*-setup.exe` 覆盖到同一目录，或解压 zip 覆盖 `admanager.exe` 与 `web/`（务必保留 `data/`），再启动。
6. 仅当自行把更新源改到**私有**仓库时，才需要在进程环境设置 `ADMANAGER_GH_TOKEN`。也可用 `ADMANAGER_UPDATE_REPO=owner/name` 覆盖。令牌仅服务端使用，不会出现在界面或 API 响应中。详见 [RELEASES.md](./RELEASES.md)。

> 一键应用会替换正在运行的程序文件并重启；`data/`（配置、数据库、授权、证书）始终保留。

## 离线升级（无外网）

本机**不需要**连 GitHub 即可完成升级：在有网的机器下载 Release 中的 `*-setup.exe` 或 `.zip`，拷贝到目标机后：

1. 退出正在运行的 `admanager.exe`。
2. **setup.exe**：双击安装到原目录（向导提示升级时使用同一目录以保留 `data/`）；安装程序会结束旧进程并覆盖 `admanager.exe` / `web/`，**保留 `data/`**。
3. **zip**：解压后覆盖原目录中的程序文件与 `web/`，**不要删除 `data/`**。
4. 重新启动。配置、数据库、证书与授权文件均在 `data/`，覆盖安装后仍可用。


## 许可与换机

若更换电脑、重装系统或迁移虚拟机后提示许可不可用：在「授权与版本」复制指纹与实例 ID，联系供应商重新签发 `.lic`，再导入即可。升级安装请保留 `data/`。

## Windows SmartScreen /「未知发布者」

自 **v23.2.4** 起，发行包中的 `admanager.exe` 与 `*-setup.exe` 使用**自签名 Authenticode** 证书签名（Linux 上 `osslsigncode`；公钥见仓库 `scripts/codesign/admanager-codesign.crt`）。

请诚实预期：

- **签名可以校验**（文件属性 → 数字签名可见发布者「AD Manager」），说明安装包未被篡改。
- **SmartScreen 仍可能警告**「Windows 已保护你的电脑 / Unknown publisher」：自签名证书不在 Windows 信任链中，也**没有**微软 SmartScreen 下载声誉。自签名**不能**替代 OV/EV 商业代码签名证书。
- **真正显著减少警告**需要购买 OV/EV 代码签名证书并对安装包签名，再随下载量积累声誉；本项目默认**不购买**商业证书。
- **用户侧临时做法**：SmartScreen 对话框 → **更多信息** → **仍要运行**（仅在信任来源时使用，例如从本仓库 GitHub Releases 下载并核对 `.sha256`）。
- 自建签名：设置 `ADMANAGER_CODESIGN_PFX` / `ADMANAGER_CODESIGN_PASS` 后运行 `scripts/build-windows.sh`；详见 `scripts/codesign/README.md`。

## API 令牌（脚本）

「系统设置 → API 令牌」可创建长效 Bearer。示例：

```bash
curl -sk -H "Authorization: Bearer adm_…" https://127.0.0.1:9443/api/auth/me
```

Bearer 请求无需 CSRF；令牌保存在 `data/`（覆盖安装保留）。

