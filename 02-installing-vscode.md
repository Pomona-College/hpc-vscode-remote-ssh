---
title: "Installing VS Code"
teaching: 10
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions

- How do I install VS Code on my operating system?
- How do I install the Remote-SSH extension?

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Install VS Code on Windows, Mac, or Linux
- Install and enable the Remote-SSH extension
- Enable the critical DUO MFA setting

::::::::::::::::::::::::::::::::::::::::::::::

## Step 1: Install Visual Studio Code

VS Code is free and available on all major operating systems.

### Windows

1. Visit [code.visualstudio.com](https://code.visualstudio.com)
2. Click the Windows download button (Windows x64 Installer)
3. Run the downloaded installer and follow the wizard (defaults are fine)
4. Verify: open PowerShell and type `code --version`

### Mac

1. Visit [code.visualstudio.com](https://code.visualstudio.com)
2. Click the Mac download button (choose Intel or Apple Silicon)
3. Open the .zip and drag "Visual Studio Code.app" to Applications
4. Verify: open Terminal and type `code --version`

### Linux (Ubuntu/Debian)

```bash
sudo apt update
sudo apt install software-properties-common apt-transport-https wget
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
sudo apt update && sudo apt install code
```

Verify: `code --version`

### Linux (Fedora/RHEL)

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
dnf check-update && sudo dnf install code
```

## Step 2: Install Remote-SSH Extension

1. Open VS Code
2. Click the Extensions icon on the left sidebar (four squares icon)
3. Search for "Remote-SSH"
4. Find **Remote - SSH** by Microsoft (the official one)
5. Click **Install**

You should now see a "Remote Explorer" icon in the left sidebar.

## Step 3: Enable Login Terminal for DUO

::::::::::::::::::::::::::::::::::::: callout

## Essential: Enable Login Terminal for DUO Authentication

Before connecting, you MUST enable one critical setting:

1. Open Settings: **File > Preferences > Settings** (Ctrl+, or Cmd+,)
2. Search for: `remote.SSH.showLoginTerminal`
3. **Check the checkbox** to enable this setting

**Why this matters:** Sagehen HPC requires DUO MFA. Without this setting, DUO
prompts appear in an invisible terminal and you cannot authenticate. This is the
number one reason people cannot connect initially.

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge: Verify Your Installation

1. Run `code --version` in your terminal. Do you get a version number?
2. Open VS Code and check Extensions. Is "Remote - SSH" installed?
3. In Settings, search `remote.SSH.showLoginTerminal`. Is it checked?

::::::::::::::::::::::::::::::::::::: solution

## Solution

1. `code --version` should print a version like `1.87.2`. If "command not found,"
   VS Code is not installed or not in your PATH.
2. Remote - SSH should appear in Extensions with an "Installed" badge.
3. The checkbox should show a checkmark next to "Show Login Terminal".

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Install VS Code from code.visualstudio.com for your operating system
- Install the Remote-SSH extension by Microsoft from the Extensions sidebar
- Enable `remote.SSH.showLoginTerminal` in settings -- this is required for DUO

::::::::::::::::::::::::::::::::::::::::::::::
