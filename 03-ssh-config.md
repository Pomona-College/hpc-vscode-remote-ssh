---
title: "Setting Up SSH Config"
teaching: 10
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions

- What SSH configuration do I need for Sagehen HPC?
- How do I set up SSH keys for passwordless authentication?

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Configure ~/.ssh/config with proper Sagehen credentials
- Set correct file permissions on SSH files
- Optionally generate SSH keys (Ed25519 recommended)
- Verify SSH connectivity from the terminal

::::::::::::::::::::::::::::::::::::::::::::::

## Create or Edit ~/.ssh/config

VS Code Remote-SSH uses your system's SSH configuration to connect. You need
an entry for Sagehen in `~/.ssh/config`.

**On Windows (PowerShell):**

```powershell
New-Item -ItemType Directory -Force -Path $HOME\.ssh | Out-Null
notepad $HOME\.ssh\config
```

**On Mac/Linux (Terminal):**

```bash
mkdir -p ~/.ssh && chmod 700 ~/.ssh
nano ~/.ssh/config
```

### Add the Sagehen HPC Entry

::::::::::::::::::::::::::::::::::::: callout

## SSH Configuration for Sagehen HPC

Add this to your `~/.ssh/config` (replace `<myusername>` with your Pomona username):

```
Host sagehen
    HostName sagehen.hpc.pomona.edu
    User username
    ServerAliveInterval 300
    ServerAliveCountMax 2
```

| Setting | Purpose |
|---------|---------|
| `Host sagehen` | Friendly name for the connection |
| `HostName sagehen.hpc.pomona.edu` | Actual cluster address |
| `User username` | Your Pomona username |
| `ServerAliveInterval 300` | Keep connection alive every 300 seconds |
| `ServerAliveCountMax 2` | Disconnect after 2 unanswered keepalives |

::::::::::::::::::::::::::::::::::::::::::::::

### Set File Permissions (Mac/Linux)

```bash
chmod 600 ~/.ssh/config
chmod 700 ~/.ssh
```

## Optional: Generate SSH Key

For passwordless connections (DUO still applies), generate an SSH key. Ed25519
is recommended; RSA-4096 is also acceptable.

**Generate a key:**

```bash
ssh-keygen -t ed25519 -C "your-email@pomona.edu"
```

Press Enter for default location. You may set a passphrase or leave blank.

**Copy to Sagehen (Mac/Linux):**

```bash
ssh-copy-id -i ~/.ssh/id_ed25519 sagehen
```

**Copy to Sagehen (Windows PowerShell):**

```powershell
Get-Content $HOME\.ssh\id_ed25519.pub | Set-Clipboard
# SSH into Sagehen manually, then:
# mkdir -p ~/.ssh && echo "PASTE_KEY_HERE" >> ~/.ssh/authorized_keys
# chmod 600 ~/.ssh/authorized_keys
```

## Test Your SSH Connection

Before using VS Code Remote-SSH, verify from your terminal:

```bash
ssh sagehen
```

**Expected sequence:**

1. Password prompt: `<myusername>@sagehen.hpc.pomona.edu's password:`
2. Enter your Pomona password
3. DUO prompt appears
4. Complete DUO authentication
5. You see: `[<myusername>@sagehen-login-1 ~]$`

Type `exit` to disconnect.

**If this fails:** Check your username in `~/.ssh/config`, verify Pomona
credentials and DUO registration, and contact its-hpc@pomona.edu if needed.

::::::::::::::::::::::::::::::::::::: challenge

## Challenge: Verify SSH Configuration

1. Open `~/.ssh/config` and check the sagehen entry
2. Run `ssh -G sagehen` to display your effective SSH configuration
3. Run `ssh sagehen` and complete DUO authentication
4. Once connected, run `uname -a` and `whoami`, then `exit`

::::::::::::::::::::::::::::::::::::: solution

## Solution

`ssh -G sagehen` should show:

```
hostname sagehen.hpc.pomona.edu
user yourname
serveraliveinterval 300
serveralivecountmax 2
```

![Verifying the effective config on Windows: `ssh -G sagehen` filtered through `Select-String`.](fig/03-ssh-config-verify-windows.png){alt='A PowerShell window where ssh -G sagehen is piped to Select-String to filter key settings. The output shows the username, hostname sagehen.hpc.pomona.edu, serveralivecountmax 2, and serveraliveinterval 300.'}

After connecting, `uname -a` shows a Linux kernel version and `whoami` shows
your Pomona username. If `whoami` returns the wrong name, fix the `User` line in
`~/.ssh/config`. If the connection hangs at the DUO two-factor login prompt, verify DUO registration.

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Configure ~/.ssh/config with a `Host sagehen` entry and your Pomona username
- Set proper file permissions (600 for config, 700 for .ssh directory)
- SSH keys (Ed25519 recommended) are optional but convenient for frequent users
- Always test `ssh sagehen` from a terminal before using VS Code Remote-SSH

::::::::::::::::::::::::::::::::::::::::::::::

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
