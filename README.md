# RockDesk（磐石远控）: remote desktop and remote control for people and AI agents

RockDesk is remote desktop and remote-access software. Every machine gets a 9-digit ID; machines connect peer-to-peer where possible, end-to-end encrypted, and fall back to a relay when there is no direct path, so neither side needs a public IP, port forwarding or a VPN. AI agents such as Claude Code, Codex, Gemini CLI, DeepSeek Harness, Cursor and Trae can drive it too, through its `rds` command line or its MCP server.

中文说明：[README.zh.md](README.zh.md) · Website: <https://rockdesk.io> (China: <https://rockdesk.cn>)

This repository hosts RockDesk's release packages and notes. RockDesk itself is proprietary software; see [License](#license).

## Download

Install RockDesk on **both** machines: the one you control from and the one you want to control. Each new device starts with a free trial.

| Platform | Official download (newest) | GitHub |
|---|---|---|
| Windows (64-bit) | <https://rockdesk.io/download/latest/windows> | [Releases](https://github.com/rockdesk-io/rockdesk/releases/latest) |
| macOS, Apple silicon | <https://rockdesk.io/download/latest/macos> | [Releases](https://github.com/rockdesk-io/rockdesk/releases/latest) |
| macOS, Intel | <https://rockdesk.io/download/latest/macos-x86_64> | [Releases](https://github.com/rockdesk-io/rockdesk/releases/latest) |
| Linux x86_64 (.deb: Ubuntu 20.04+, Debian 12+) | <https://rockdesk.io/download/latest/linux-amd64> | [Releases](https://github.com/rockdesk-io/rockdesk/releases/latest) |
| Linux arm64 (.deb: Ubuntu 22.04+, Debian 12+) | <https://rockdesk.io/download/latest/linux-arm64> | [Releases](https://github.com/rockdesk-io/rockdesk/releases/latest) |
| Android (64-bit ARM) | <https://rockdesk.io/download/latest/android> | [Releases](https://github.com/rockdesk-io/rockdesk/releases/latest) |
| iOS / iPadOS | [RockDesk Remote](https://apps.apple.com/app/id6788146069) on the App Store (controls other devices) | — |
| Web | <https://rockdesk.io/web/>, nothing to install | — |

In China, use rockdesk.cn instead of rockdesk.io in these links; it is faster there. Every release here lists the SHA-256 of each package.

- **Windows:** the installer is not code-signed yet. If Windows says "Windows protected your PC", click **More info**, then **Run anyway**. It installs a background service, so it asks for administrator rights. Also available through winget (pending review).
- **macOS:** open the .dmg, drag RockDesk into Applications and open it once; it asks for Screen Recording and Accessibility the first time someone views or controls the Mac. With Homebrew: `brew tap rockdesk-io/tap && brew install --cask rockdesk`.
- **Linux:** `sudo apt install ./rockdesk-<version>-linux-amd64.deb`, then open the RockDesk app. On a server without a screen: `sudo systemctl enable --now rockd`, then `sudo rds otp` prints a one-time password.

## What it does

- **Remote desktop:** AV1 between computers, hardware H.264 when a phone is being controlled, quality presets you can switch during a session.
- **Terminal:** an interactive shell, or one command with its real exit code.
- **Files:** copy and sync, or mount a remote folder as a local one.
- **Clipboard:** synced between machines, with a searchable history.
- **Network:** TCP port forwarding, a VPN into the remote network (内网穿透), serial forwarding, USB forwarding between Linux and Windows in both directions, Wake-on-LAN.
- **Unattended access:** installed as a system service it is online at boot, before anyone logs in; the login screen, the lock screen and a blanked display can be viewed and logged into remotely (Linux GNOME on Wayland or Xorg, macOS).

## For AI agents

The `rds` command line does everything the app does, so an agent can work on another computer by its ID: run commands, copy files, take screenshots, click and type, read the clipboard and forward ports.

- **Skill and plugins** (Claude Code, Codex, Gemini CLI, DeepSeek Harness, Trae, WorkBuddy and others): <https://github.com/rockdesk-io/rockdesk-skill>
- **MCP server** (18 tools): `claude mcp add -s user rockdesk -- npx -y rockdesk-mcp`, or in any MCP client:

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

If RockDesk is not installed on that computer yet, the MCP server offers an `install_rockdesk` tool: the agent asks you first, then installs it. Listed in the official MCP Registry as `io.rockdesk/rockdesk`.

Then just ask, for example: "Connect to 123456789, check its free disk space and summarize the recent errors in /var/log."

## Who can connect

The machine being controlled decides: a click on **Allow** on its screen, a one-time password, its fixed password, the same RockDesk account, or a key you trust. Terminal, files, desktop, clipboard, forwarding, serial and USB can each be switched on or off, so an agent only gets what it needs. Connections are end-to-end encrypted (QUIC / TLS 1.3).

## Pricing

Each new device starts with a free trial. Plans: <https://rockdesk.io/pricing.html> (China: <https://rockdesk.cn/pricing.html>).

## License

RockDesk is proprietary software, used under the [RockDesk Terms](https://rockdesk.io/terms.html). This repository holds RockDesk's release packages and documentation. The third-party components RockDesk uses are listed in the app (Settings → Open-source licenses) and in `THIRD-PARTY-NOTICES.txt` inside the macOS disk image.

## Contact

Questions and feedback: support@rockdesk.io · Community: [GitHub Discussions](https://github.com/rockdesk-io/rockdesk-skill/discussions)
