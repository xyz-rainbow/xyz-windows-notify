<div align="center">

<img src="assets/banner.svg" width="100%" alt="XYZ Windows Notify Banner" />

# 🦄 XYZ Windows Notify

**Universal AI Agent Toast Notification Skill for Windows**

[![License: MIT](https://img.shields.io/badge/License-MIT-purple.svg)](LICENSE)
[![PowerShell](https://img.shields.io/badge/PowerShell-5.1%20%7C%207%2B-blue.svg)](https://microsoft.com/powershell)
[![Windows](https://img.shields.io/badge/Windows-10%20%7C%2011%20Compatible-0078d4.svg)](https://microsoft.com/windows)
[![skills.sh](https://img.shields.io/badge/skills.sh-xyz--windows--notify-00f2fe.svg)](https://skills.sh)
[![npx skills add](https://img.shields.io/badge/npx%20skills%20add-xyz--rainbow%2Fxyz--windows--notify-ff007f.svg)](#-one-command-installation-skills-cli)

*Supercharge AI agent workflows with native Windows toast notifications (fully compatible with Windows 10 & 11), percentage progress bars (%), bundled & AI-generated custom app logos (`-AppLogo`), non-blocking background telemetry, and sound alerts.*

</div>

---

## 📸 Visual Architecture & Lifecycle Workflow

### 🏗️ System Architecture & Smart Resolution Pipeline
<div align="center">
  <img src="assets/architecture.svg" width="100%" alt="System Architecture and Icon Resolution Pipeline" />
</div>

<br/>

### 🔄 Notification Lifecycle & Progress Milestones
<div align="center">
  <img src="assets/workflow.svg" width="100%" alt="Notification Lifecycle Workflow" />
</div>

---

## ✨ Key Features

- 🦄 **Bundled Default Branding**: Out-of-the-box unicorn logo bundled directly in `assets/unicorn.jpg` and `assets/icon.jpg`.
- 🪟 **Universal Windows Support**: Fully compatible with both **Windows 10** and **Windows 11** via the PowerShell `BurntToast` engine.
- 🤖 **AI-Driven Icon Intelligence**: AI agents can detect workflow domains, select themed icons, or suggest generating custom 256x256 icons.
- 📊 **Real-Time Progress Milestones (%)**: Send non-blocking progress updates at 10%, 25%, 50%, 75%, and 90% milestones.
- 🚀 **Full Lifecycle Coverage**: Start, In-Progress, Success (100%), and Error/Exception toast notifications.
- 🔔 **Windows Action Center Integration**: Native toasts with customizable sound effects (`-Sound 'Default'`, `'Reminder'`, `'Alarm2'`).
- 🌐 **Universal Multi-Agent Standard**: Compatible with Antigravity, Claude, GPT, Cursor, Trae, Pi, Grok, and custom subagents.

---

## 🚀 One-Command Installation (Skills CLI)

Install directly into any AI agent environment using the universal `skills` CLI:

```bash
npx skills add xyz-rainbow/xyz-windows-notify
```

*Or via full repository URL:*
```bash
npx skills add https://github.com/xyz-rainbow/xyz-windows-notify
```

---

## 🎨 Custom Icons & AI Asset Management Guide

### 1. Where to Place Your Custom Logos / Icons

You can add custom icons for your specific projects and workflows:

| Location | Purpose | Example Path |
| :--- | :--- | :--- |
| **`assets/` (Bundled)** | Default fallback branding for the skill | `assets/unicorn.jpg`, `assets/icon.jpg` |
| **`assets/icons/`** | Thematic task icons (backup, build, deploy, db) | `assets/icons/deploy.png`, `assets/icons/db.png` |
| **User Global Folder** | Personal system-wide icon repository | `U:\Pictures\Icons\unicorn.jpg` or `C:\Users\<user>\Pictures\Icons\` |
| **Custom Project Path** | One-off icon path passed directly | `C:\Projects\my-app\assets\logo.png` |

### 2. Recommended Icon Specifications

- **Format**: `PNG` or `JPG` (square 1:1 aspect ratio).
- **Dimensions**: `256x256` or `512x512` pixels.
- **Visuals**: Clean, high-contrast imagery with transparent or dark-mode friendly background.

---

### 3. AI Agent Protocol: Auto-Selection & Proactive Generation

When an AI agent executes tasks with this skill, it follows this automated decision tree:

```mermaid
graph TD
    A[AI Agent Starts Long Task] --> B{Does specific icon exist?}
    B -- Yes --> C[Use Context Icon e.g. assets/icons/build.png]
    B -- No --> D{Is it a new unique workflow?}
    D -- No --> E[Fallback to Bundled assets/unicorn.jpg]
    D -- Yes --> F[AI Proactively Suggests Creating New Icon]
    F --> G[User Approves -> Generate & Save to assets/icons/]
    G --> H[Send Notification with New Custom Icon]
    C --> I[Send Toast Notification]
    E --> I
```

#### How AI Agents Proactively Suggest New Icons:
When an agent detects a distinct recurring workflow (such as a database migration, game server sync, or media render), it will suggest:
> *"I noticed we don't have a dedicated notification icon for **Minecraft Server Backup**. Would you like me to generate a custom 256x256 icon and save it to `assets/icons/minecraft.png` for future toasts?"*

---

## ⚙️ Prerequisites & Setup

### Install PowerShell BurntToast Module
Run in PowerShell (Current User or Administrator):

```powershell
Install-Module BurntToast -Scope CurrentUser -Force -AllowClobber
```

Verify your installation:
```powershell
Import-Module BurntToast
New-BurntToastNotification -Text "BurntToast OK", "Notifications configured successfully!"
```

---

## 💻 Code Snippets & Usage Examples

### 🔹 PowerShell Integration (with Fallback Resolution)

```powershell
Import-Module BurntToast

# Smart Icon Resolution
$SkillIcon = "$PSScriptRoot\assets\unicorn.jpg"
$UserIcon  = "U:\Pictures\Icons\unicorn.jpg"

$AppLogo = if (Test-Path $SkillIcon) {
    $SkillIcon
} elseif (Test-Path $UserIcon) {
    $UserIcon
} else {
    $null
}

# Send Toast
if ($AppLogo) {
    New-BurntToastNotification `
        -Text "🦄 Backup Progress: 75%", "1,575 MB of 2,100 MB transferred" `
        -AppLogo $AppLogo `
        -Sound 'Default'
} else {
    New-BurntToastNotification `
        -Text "📊 Backup Progress: 75%", "1,575 MB of 2,100 MB transferred" `
        -Sound 'Default'
}
```

---

### 🔹 Python Integration Wrapper

```python
import subprocess
import os

def send_toast(title: str, message: str, icon_path: str = None, sound: str = "Default"):
    """
    Sends a native Windows toast notification (Windows 10 & 11) with automatic icon resolution.
    """
    candidates = [
        icon_path,
        os.path.join(os.path.dirname(__file__), "assets", "unicorn.jpg"),
        r"U:\Pictures\Icons\unicorn.jpg"
    ]
    
    selected_icon = next((c for c in candidates if c and os.path.exists(c)), None)
    
    if selected_icon:
        ps_cmd = f"Import-Module BurntToast; New-BurntToastNotification -Text '{title}', '{message}' -AppLogo '{selected_icon}' -Sound '{sound}'"
    else:
        ps_cmd = f"Import-Module BurntToast; New-BurntToastNotification -Text '{title}', '{message}' -Sound '{sound}'"
        
    subprocess.run(["powershell", "-NoProfile", "-ExecutionPolicy", "Bypass", "-Command", ps_cmd], capture_output=True)

# Example: Task Lifecycle Monitoring
if __name__ == "__main__":
    send_toast("🚀 Task Started", "Beginning backup of Kindle and Calibre libraries...")
    send_toast("📊 Progress: 50%", "Transferred 1,024 MB / 2,048 MB")
    send_toast("✅ Task Complete (100%)", "2,100 files successfully verified and stored!")
```

---

## 🌐 Multi-Agent Directory Reference

To distribute this skill across different AI agent environments on Windows:

| Agent Environment | Destination Directory |
| :--- | :--- |
| **Global Agent Skills** | `C:\Users\<user>\.agents\skills\windows-notify\` |
| **Google Antigravity / Gemini** | `C:\Users\<user>\.gemini\config\skills\windows-notify\` |
| **Anthropic Claude Code / Desktop** | `C:\Users\<user>\.claude\skills\windows-notify\` |
| **MiniMax Agent** | `C:\Users\<user>\.minimax\skills\windows-notify\` |
| **xAI Grok Agent** | `C:\Users\<user>\.grok\skills\windows-notify\` |
| **Trae IDE / Agent** | `C:\Users\<user>\.trae\skills\windows-notify\` |
| **Qwen Agent** | `C:\Users\<user>\.qwen\skills\windows-notify\` |
| **Pi / Crush Agent** | `C:\Users\<user>\.pi\agent\skills\windows-notify\` |

---

## 🏷️ Metadata & GitHub Tags

`skills-sh` `npx-skills-add` `windows` `windows10` `windows11` `toast-notifications` `burnttoast` `powershell` `ai-agent-skill` `antigravity` `custom-applogo` `notifications` `unicorn-branding` `python`

---

## 📜 License

Distributed under the **MIT License**. See [`LICENSE`](LICENSE) for details.
