---
name: windows-notify
description: >-
  Send Windows toast notifications (compatible with Windows 10 & 11) with custom app icons (-AppLogo), real-time
  progress percentages (%), start/completion alerts, and sound feedback using PowerShell BurntToast. Includes bundled
  branding, smart icon resolution, and AI-driven icon selection/generation guidelines.
  Use whenever a background task, backup, build, server restart, or long process requires visual notification feedback.
---

# XYZ Windows Notify — Universal AI Agent Skill

This skill enables any AI agent (Antigravity, Claude, GPT, Cursor, Trae, Pi, Grok, etc.) to trigger native **Windows Toast Notifications** (compatible with **Windows 10 & Windows 11**) using PowerShell `BurntToast` with custom branding, percentage milestones, and dynamic icon management.

---

## 🚀 Installation via Skills CLI

```bash
npx skills add xyz-rainbow/xyz-windows-notify
```

---

## 🦄 Bundled Assets & Smart Icon Resolution

This skill bundles default branding in its `assets/icons/` directory (`assets/icons/unicorn.jpg` and `assets/icons/icon.jpg`).

When sending a notification, follow this **Smart Resolution Hierarchy** (with backward compatibility):
1. **Explicit Parameter**: Path provided via `-AppLogo "path/to/custom_icon.png"`.
2. **Skill Bundled Icon**: Local path inside the skill directory (e.g. `<skill_dir>/assets/icons/unicorn.jpg`).
3. **Legacy Bundled Icon**: `<skill_dir>/assets/unicorn.jpg` (for backward compatibility).
4. **User Default Icon**: Standard user path (e.g. `U:\Pictures\Icons\unicorn.jpg` if available).
5. **Graceful Fallback**: Native Windows notification without `-AppLogo` if no file exists.

---

## 🤖 AI Agent Guidelines for Custom Icons & Generation

AI Agents operating with this skill should actively manage visual feedback:

### 1. Contextual Icon Selection
- **General / Default**: Use `assets/icons/unicorn.jpg` or `assets/icons/icon.jpg`.
- **Database / Backups**: If specialized icons exist (e.g. `assets/icons/backup.png` or `assets/icons/database.png`), prioritize them.
- **Deployments / Server**: Rocket / Server icons.
- **Errors / Critical Alerts**: Warning / Shield icons.

### 2. Suggesting & Generating New Icons
- **Where to store icons**: Store new icons in `assets/icons/<name>.png` (within the skill or repo folder) or in the user's icon directory (`U:\Pictures\Icons\`).
- **Icon Specifications**:
  - Format: `PNG` or `JPG` (square 1:1 aspect ratio).
  - Recommended dimensions: `256x256` or `512x512` pixels.
  - Transparent or clean solid background.
- **Proactive AI Protocol**:
  - When starting a new recurring workflow (e.g., a new game server monitor, video rendering pipeline, or scientific data sync), check if a matching icon exists in `assets/icons/`.
  - If no thematic icon exists, propose:
    > *"I noticed we don't have a specific toast icon for [Task Name]. Would you like me to generate a custom 256x256 icon and save it to `assets/icons/[name].png`?"*
  - Use image generation tools (e.g., `generate_image`) or fetch appropriate assets upon user approval.

---

## 💻 PowerShell Integration

```powershell
Import-Module BurntToast

# Resolve Default / Bundled Icon (with Backward Compatibility)
$CandidateIcons = @(
    "$PSScriptRoot\assets\icons\unicorn.jpg",
    "$PSScriptRoot\assets\unicorn.jpg",
    "U:\Pictures\Icons\unicorn.jpg"
)

$AppLogo = $CandidateIcons | Where-Object { Test-Path $_ } | Select-Object -First 1

# Send Notification with Fallback
if ($AppLogo) {
    New-BurntToastNotification `
        -Text "🦄 Task Milestone: 50%", "Copied 1,024 MB of 2,048 MB" `
        -AppLogo $AppLogo `
        -Sound 'Default'
} else {
    New-BurntToastNotification `
        -Text "📊 Task Milestone: 50%", "Copied 1,024 MB of 2,048 MB" `
        -Sound 'Default'
}
```

---

## 🐍 Python Integration Pattern

```python
import subprocess
import os

def send_toast(title: str, message: str, icon_path: str = None):
    # Candidate icon paths with backward compatibility
    base_dir = os.path.dirname(__file__)
    candidates = [
        icon_path,
        os.path.join(base_dir, "assets", "icons", "unicorn.jpg"),
        os.path.join(base_dir, "assets", "unicorn.jpg"),
        r"U:\Pictures\Icons\unicorn.jpg"
    ]

    selected_icon = next((c for c in candidates if c and os.path.exists(c)), None)

    if selected_icon:
        ps_cmd = f"Import-Module BurntToast; New-BurntToastNotification -Text '{title}', '{message}' -AppLogo '{selected_icon}' -Sound 'Default'"
    else:
        ps_cmd = f"Import-Module BurntToast; New-BurntToastNotification -Text '{title}', '{message}' -Sound 'Default'"

    subprocess.run(["powershell", "-NoProfile", "-ExecutionPolicy", "Bypass", "-Command", ps_cmd], capture_output=True)

# Example Usage across lifecycle
send_toast("🚀 Backup Started", "Analyzing directories in L:\\ and U:\\...")
send_toast("📊 Progress: 50%", "Transferred 1,024 MB / 2,048 MB")
send_toast("✅ Backup Completed (100%)", "2,100 files successfully synced to D:\\")
```

---

## 🌐 Multi-Agent Global Configuration

To make this skill accessible across all agents on the machine, ensure this folder is symlinked or copied into:
- Antigravity / Gemini: `~/.gemini/config/skills/windows-notify/`
- Claude Desktop / Code: `~/.claude/skills/windows-notify/`
- Cursor / Trae / Global Agents: `~/.agents/skills/windows-notify/`
