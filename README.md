# Lingora Figma Mac 安装与更新

这里分发 Lingora Figma 插件的测试安装版本，无需 GitHub 账号、源码仓库、Node.js、Python 或 Homebrew。
编译后的插件可公开下载；安装包不包含账号、API Key 或个人设备设置。

## 安装或更新

先安装 Figma 桌面端并保存、同步设计稿，然后在终端执行：

```bash
/bin/bash -c "$(/usr/bin/curl --fail --silent --show-error --location --proto '=https' --proto-redir '=https' https://raw.githubusercontent.com/BianTaoGit/lingora-figma-releases/main/install.sh)"
```

同一命令始终安装当前发布版本。脚本自动下载、校验、正常退出 Figma、备份配置、注册插件并重新打开 Figma。
不需要导入 manifest。安装后从 Plugins → Development → Lingora localization 运行插件。
首次使用仍需填写自己的 Lingora 服务、项目和 API Key。

## 适用范围

- 仅 macOS 的 Figma 桌面端，目前接受 Figma 126.x；真实界面验证版本为 126.10.13。
- 使用 Figma 内部的开发插件注册格式，非官方安装接口；不兼容的主版本停止安装。
- macOS 首次可能询问是否允许终端控制 Figma。拒绝权限、未保存提示或退出超时会停止，绝不强制终止。
- 没有后台自动更新，重新运行命令即可更新。
- GitHub 下载地址需要能从当前网络访问；安装器不需要 GitHub 凭据。

仅检查下载与配置兼容性，不退出 Figma 或写入注册：

```bash
/bin/bash -c "$(/usr/bin/curl --fail --silent --show-error --location --proto '=https' --proto-redir '=https' https://raw.githubusercontent.com/BianTaoGit/lingora-figma-releases/main/install.sh)" -- --check
```

## 备份与恢复

版本和配置备份位于 `~/Library/Application Support/Lingora/FigmaPlugin/`。
正常退出 Figma 后，可把相应 `backups/<时间与进程号>/settings.json` 复制回
`~/Library/Application Support/Figma/settings.json` 再重启。整份备份恢复会同时还原之后修改的其他设置，
请核对时间；备份含本机设置，不要公开。安装器不会自动删除旧版本和备份。

## 验证边界

CI 在独立的 Apple Silicon 和 Intel macOS runner 上匿名下载发布包、校验摘要，并在隔离目录
运行系统 JXA 注册测试与安装器预检。CI 使用 Figma 版本配置 fixture，不代表真实 Figma 登录或 UI 验收。
成员实际机器上的安装及首次连接仍需实测。
