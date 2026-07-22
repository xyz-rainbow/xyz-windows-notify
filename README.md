<div align="center">

<img src="assets/banner.svg" width="100%" alt="XYZ Windows Notify Banner" />

# 🦄 XYZ Windows Notify

**Universal AI Agent Toast Notification Skill for Windows 11**

[![License: MIT](https://img.shields.io/badge/License-MIT-purple.svg)](LICENSE)
[![PowerShell](https://img.shields.io/badge/PowerShell-5.1%20%7C%207%2B-blue.svg)](https://microsoft.com/powershell)
[![skills.sh](https://img.shields.io/badge/skills.sh-xyz--windows--notify-00f2fe.svg)](https://skills.sh)
[![npx skills add](https://img.shields.io/badge/npx%20skills%20add-xyz--rainbow%2Fxyz--windows--notify-ff007f.svg)](#-one-command-installation-skills-cli)

*Elevate your AI agent workflows with native Windows 11 toast notifications, percentage progress bars (%), custom branding icons (`-AppLogo`), and non-blocking background process monitoring.*

</div>

---

## 🚀 One-Command Installation (Skills CLI)

Install this skill into any AI Agent codebase / environment instantly using `npx skills add`:

```bash
npx skills add xyz-rainbow/xyz-windows-notify
```

*Or via full repository URL:*
```bash
npx skills add https://github.com/xyz-rainbow/xyz-windows-notify
```

---

## 📸 Visual Architecture & Workflow

### System Architecture
<img src="assets/architecture.svg" width="100%" alt="System Architecture" />

### Notification Lifecycle & Progress Milestones
<img src="assets/workflow.svg" width="100%" alt="Notification Workflow" />

---

## ✨ Features

- 🦄 **Custom Branding Icons**: Attach custom `-AppLogo` images (e.g. `U:\Pictures\Icons\unicorn.jpg`).
- 📊 **Real-Time Progress (%)**: Send progress updates at 10%, 25%, 50%, 75%, 90% milestones.
- 🚀 **Lifecycle Alerts**: Start, In-Progress, Success (100%), and Error toast notifications.
- 🔔 **Windows Action Center**: Native Windows 11 visual toasts with sound feedback (`-Sound 'Default'`).
- 🤖 **Universal AI Agent Compatibility**: Works out-of-the-box with Antigravity, Claude, GPT-4, Cursor, and custom subagents.

---

## ⚙️ Prerequisites & Setup

### 1. Install PowerShell BurntToast Module
Open PowerShell as Administrator / User:

```powershell
Install-Module BurntToast -Scope CurrentUser -Force -AllowClobber
```

Verify installation:
```powershell
Import-Module BurntToast
New-BurntToastNotification -Text "BurntToast OK", "Notifications working!"
```

---

## 🌐 Global Installation Options

### Method A: `npx skills add` (Recommended)

```bash
npx skills add xyz-rainbow/xyz-windows-notify
```

### Method B: Manual Global Setup

Copy `SKILL.md` to your AI Agent's global skill folder:

```powershell
mkdir -p "C:\Users\$env:USERNAME\.gemini\config\skills\windows-notify"
copy "SKILL.md" "C:\Users\$env:USERNAME\.gemini\config\skills\windows-notify\SKILL.md"
```

---

## 💻 Code Snippets & Usage Examples

### PowerShell Command

```powershell
Import-Module BurntToast

New-BurntToastNotification `
    -Text "🦄 Backup Progress: 50%", "Copiados 1,024 MB de 2,048 MB" `
    -AppLogo "U:\Pictures\Icons\unicorn.jpg" `
    -Sound 'Default'
```

### Python Script Integration

```python
import subprocess
import os

def notify(title, message, icon=r"U:\Pictures\Icons\unicorn.jpg"):
    ps_cmd = f"Import-Module BurntToast; New-BurntToastNotification -Text '{title}', '{message}' -AppLogo '{icon}' -Sound 'Default'"
    subprocess.run(["powershell", "-NoProfile", "-ExecutionPolicy", "Bypass", "-Command", ps_cmd], capture_output=True)

# Example Usage
notify("🚀 Backup Started", "Copying Kindle L:\\ and Calibre U:\\ to D:\\")
notify("📊 Progress: 70%", "1,450 MB / 2,100 MB transferred")
notify("✅ Backup Complete (100%)", "2,100 files successfully saved!")
```

---

## 🏷️ GitHub Tags & Metadata

`skills-sh` `npx-skills-add` `windows11` `toast-notifications` `burnttoast` `powershell` `ai-agent-skill` `antigravity` `notifications` `unicorn-icon`

---

## 📜 License

Distributed under the MIT License. See `LICENSE` for more information.
