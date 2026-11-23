# RockDesk（磐石远控）：人和 AI 都能用的远程桌面、远程控制

RockDesk 是远程桌面和远程控制软件。每台设备一个 9 位 ID，能直连就点对点，打不通自动走中继，内容端到端加密，两台电脑都不需要公网 IP、不用开端口、不用配 VPN。Claude Code、Codex、Trae、DeepSeek Harness、WorkBuddy、Gemini CLI、Cursor 等 AI 工具也能直接用它操作另一台电脑：通过 `rds` 命令行，或者它自带的 MCP 服务。

English: [README.md](README.md) · 官网：<https://rockdesk.cn>（海外：<https://rockdesk.io>）

这个仓库放 RockDesk 的发布安装包和说明。RockDesk 本身是专有软件，见文末「许可」。

## 下载

两台电脑都要装：你用来控制的这台，和要被控制的那台。每台新设备有免费试用期。

| 平台 | 官网直链（始终是最新版） | GitHub |
|---|---|---|
| Windows（64 位） | <https://rockdesk.cn/download/latest/windows> | [Releases](https://github.com/rockdesk-io/rockdesk/releases/latest) |
| macOS（Apple 芯片） | <https://rockdesk.cn/download/latest/macos> | [Releases](https://github.com/rockdesk-io/rockdesk/releases/latest) |
| macOS（Intel） | <https://rockdesk.cn/download/latest/macos-x86_64> | [Releases](https://github.com/rockdesk-io/rockdesk/releases/latest) |
| Linux x86_64（.deb：Ubuntu 20.04+、Debian 12+） | <https://rockdesk.cn/download/latest/linux-amd64> | [Releases](https://github.com/rockdesk-io/rockdesk/releases/latest) |
| Linux arm64（.deb：Ubuntu 22.04+、Debian 12+，树莓派 64 位系统也行） | <https://rockdesk.cn/download/latest/linux-arm64> | [Releases](https://github.com/rockdesk-io/rockdesk/releases/latest) |
| 安卓（64 位 ARM） | <https://rockdesk.cn/download/latest/android> | [Releases](https://github.com/rockdesk-io/rockdesk/releases/latest) |
| iOS / iPadOS | App Store 搜「RockDesk Remote」（用来控制别的设备） | — |
| 网页版 | <https://rockdesk.cn/web/>，不用安装 | — |

国内用 rockdesk.cn 的链接更快；海外把链接里的 rockdesk.cn 换成 rockdesk.io。每个 Release 都列了各个安装包的 SHA-256。

- **Windows：** 安装包还没有代码签名。如果弹出「Windows 已保护你的电脑」，点「更多信息」，再点「仍要运行」。它会装一个后台服务，所以要管理员权限。
- **macOS：** 打开 .dmg，把 RockDesk 拖进「应用程序」，打开一次；第一次被看屏幕、被控制时会请你允许「屏幕录制」和「辅助功能」。用 Homebrew：`brew tap rockdesk-io/tap && brew install --cask rockdesk`。
- **Linux：** `sudo apt install ./rockdesk-<版本>-linux-amd64.deb`，再打开 RockDesk。没有桌面的服务器：`sudo systemctl enable --now rockd`，再用 `sudo rds otp` 看一次性密码。

## 能做什么

- **远程桌面：** 电脑之间用 AV1，控制手机时用硬件 H.264，画质档位连接中随时切换。
- **终端：** 交互式 shell，或者跑一条命令拿到真实退出码。
- **文件：** 复制、同步，或者把远程目录挂成本地文件夹。
- **剪贴板：** 多台设备之间同步，带可搜索的历史。
- **网络：** TCP 端口转发、内网穿透、串口转发、Linux 和 Windows 之间双向 USB 转发、网络唤醒。
- **无人值守：** 装成系统服务后开机就在线，不用先登录；登录界面、锁屏、息屏都能远程看、远程输密码登录（Linux GNOME 的 Wayland / Xorg、macOS）。

## 给 AI 用

`rds` 命令行能做 App 能做的所有事，AI 按 ID 就能在另一台电脑上跑命令、传文件、截屏、点鼠标打字、读剪贴板、转发端口。

- **Skill 和插件**（Claude Code、Codex、Gemini CLI、DeepSeek Harness、Trae、WorkBuddy 等）：<https://github.com/rockdesk-io/rockdesk-skill>
- **MCP 服务**（18 个工具）：`claude mcp add -s user rockdesk -- npx -y rockdesk-mcp`，或者在任何 MCP 客户端里加：

```json
{
  "mcpServers": {
    "rockdesk": {
      "command": "npx",
      "args": ["-y", "rockdesk-mcp"]
    }
  }
}
```

本机还没装 RockDesk 的话，这个 MCP 服务会先提供 `install_rockdesk` 工具：AI 先问你，你同意后它替你装好。官方 MCP Registry 里的名字是 `io.rockdesk/rockdesk`。

接好以后直接用中文说，例如：「连上 123456789，看看磁盘还剩多少，把 /var/log 里最近的错误整理给我。」

## 谁能连进来

被控的那台说了算：在它屏幕上点「允许」、一次性密码、固定密码、同一个 RockDesk 账号，或者你信任的密钥。终端、文件、桌面、剪贴板、转发、串口、USB 可以分别开关，给 AI 只开需要的。连接端到端加密（QUIC / TLS 1.3）。

## 价格

每台新设备有免费试用期，套餐见 <https://rockdesk.cn/pricing.html>（海外：<https://rockdesk.io/pricing.html>）。

## 许可

RockDesk 是专有软件，按 [RockDesk 用户条款](https://rockdesk.cn/terms.html) 使用。这个仓库放的是 RockDesk 的发布安装包和说明。RockDesk 用到的第三方组件列在 App 的「设置 → 开源许可」里，macOS 安装镜像里也有一份 `THIRD-PARTY-NOTICES.txt`。

## 联系

问题和反馈：support@rockdesk.io · 社区讨论：[GitHub Discussions](https://github.com/rockdesk-io/rockdesk-skill/discussions)
