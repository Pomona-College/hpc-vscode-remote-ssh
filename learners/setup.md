---
title: Setup
---

## Pre-Workshop Requirements

Before attending the workshop, please complete the following steps to ensure everything is working properly.

### 1. Install VS Code

VS Code is the IDE we'll use to connect to Sagehen.

:::::::::::::::: solution

### Windows

1. Visit [code.visualstudio.com](https://code.visualstudio.com)
2. Click "Download for Windows"
3. Run the installer
4. Follow the installation wizard (default options are fine)
5. Launch VS Code when installation completes

:::::::::::::::::::::::::

:::::::::::::::: solution

### macOS

1. Visit [code.visualstudio.com](https://code.visualstudio.com)
2. Click "Download for Mac"
3. Extract the downloaded zip file
4. Drag "Visual Studio Code.app" to your Applications folder
5. Open Applications and double-click VS Code to launch it

:::::::::::::::::::::::::

:::::::::::::::: solution

### Linux (Ubuntu/Debian)

```bash
# Install using apt (easiest)
sudo apt update
sudo apt install code

# Or download from VS Code website
# Visit https://code.visualstudio.com and download the .deb file
# Then: sudo dpkg -i code_*.deb
```

:::::::::::::::::::::::::

### 2. Install the Remote-SSH Extension

Once VS Code is installed, add the Remote-SSH extension to enable HPC cluster connections.

1. Open VS Code
2. Click the Extensions icon (left sidebar, looks like four squares)
3. Search for "Remote - SSH"
4. Find the extension by Microsoft (should be first result)
5. Click "Install"
6. Wait for installation to complete

This extension allows VS Code to connect to remote machines via SSH.

### 3. Generate or Verify SSH Key Pair

SSH keys enable secure passwordless authentication (though DUO MFA is still required).

:::::::::::::::: solution

### Option A: Generate a New Key (Recommended)

**On Windows (PowerShell):**
```powershell
ssh-keygen -t ed25519 -f $ENV:USERPROFILE\.ssh\id_sagehen
# When prompted for passphrase, press Enter (or set one if desired)
```

**On macOS/Linux:**
```bash
ssh-keygen -t ed25519 -f ~/.ssh/id_sagehen
# When prompted for passphrase, press Enter (or set one if desired)
```

This creates two files:
- `id_sagehen` (private key - keep secret!)
- `id_sagehen.pub` (public key - copy to server)

:::::::::::::::::::::::::

:::::::::::::::: solution

### Option B: Use Existing SSH Key

If you already have an SSH key pair on your system, you can use it.

Check if you have keys:

**On Windows (PowerShell):**
```powershell
ls $ENV:USERPROFILE\.ssh\
```

**On macOS/Linux:**
```bash
ls ~/.ssh/
```

Look for files like `id_ed25519`, `id_rsa`, or similar. If you find them, you can skip key generation.

:::::::::::::::::::::::::

### 4. Test SSH Connection to Sagehen

Before the workshop, verify you can log in to the Sagehen cluster.

```bash
ssh <myusername>@sagehen.hpc.pomona.edu
```

You will be prompted for:
1. Your Pomona password
2. DUO MFA authentication (choose "send push" or enter code)

Once you connect, you should see the Sagehen prompt. Type `exit` to disconnect.

**If you can't connect:**
- Verify your username and password
- Confirm your DUO is registered at https://duo.pomona.edu
- Contact its-hpc@pomona.edu for help

### 5. Create or Update SSH Config File

An SSH config file simplifies connecting to Sagehen. Create one on your local machine.

:::::::::::::::: solution

### Windows (PowerShell)

Create the file (if it doesn't exist):
```powershell
# Create .ssh directory if needed
New-Item -ItemType Directory -Force -Path $ENV:USERPROFILE\.ssh

# Open config in notepad
notepad $ENV:USERPROFILE\.ssh\config
```

Add this content (replace `your_username` with your Pomona username):
```
Host sagehen
    HostName sagehen.hpc.pomona.edu
    User your_username
    IdentityFile ~/.ssh/id_sagehen
    ServerAliveInterval 300
    ServerAliveCountMax 2
```

Save the file (Ctrl+S).

:::::::::::::::::::::::::

:::::::::::::::: solution

### macOS/Linux

Open a terminal and create/edit the config:
```bash
nano ~/.ssh/config
```

Add this content (replace `your_username` with your Pomona username):
```
Host sagehen
    HostName sagehen.hpc.pomona.edu
    User your_username
    IdentityFile ~/.ssh/id_sagehen
    ServerAliveInterval 300
    ServerAliveCountMax 2
```

Save: Ctrl+O, Enter, Ctrl+X

Set permissions:
```bash
chmod 600 ~/.ssh/config
chmod 700 ~/.ssh
```

:::::::::::::::::::::::::

### 6. Test SSH Connection with Config

Now test connecting using the simplified alias:

```bash
ssh sagehen
```

You should be able to connect with just one command. Complete the DUO authentication.

### 7. Optional: Copy SSH Public Key to Server

This step is optional but enables faster authentication (DUO MFA still required).

```bash
ssh-copy-id -i ~/.ssh/id_sagehen.pub sagehen
```

On Windows, if `ssh-copy-id` doesn't work, use PowerShell:
```powershell
type $ENV:USERPROFILE\.ssh\id_sagehen.pub | ssh sagehen "cat >> ~/.ssh/authorized_keys"
```

### 8. Copy Files to Sagehen (Optional)

You may need to copy files between your computer and Sagehen. Test with a sample file:

```bash
# Copy local file to Sagehen
scp myfile.txt sagehen:~/

# Copy from Sagehen to local
scp sagehen:~/myfile.txt ./
```

### 9. Verify OnDemand Access (Optional)

Sagehen also provides a web-based interface. You can optionally test this at:

https://ondemand.hpc.pomona.edu/

Log in with your Pomona credentials + DUO.

This is useful for file browsing and running interactive jobs, though we'll focus on VS Code in this workshop.

### Troubleshooting Pre-Workshop Issues

**"SSH: Connection refused"**
- Verify hostname: `sagehen.hpc.pomona.edu`
- Check firewall isn't blocking port 22
- Ensure VPN is connected if required

**"Authentication failed"**
- Double-check username and password
- Verify DUO is registered and your phone is nearby
- Try request a call instead of entering code

**"Remote-SSH extension not appearing"**
- Restart VS Code (File → Exit, then reopen)
- Try reinstalling the extension

**"VS Code can't find SSH key"**
- Verify key path in ~/.ssh/config is correct
- Check key file exists: `ls ~/.ssh/id_sagehen`
- Check file permissions: `chmod 600 ~/.ssh/id_sagehen`

### Getting Help Before Workshop

If you have trouble with any step:

- **Email:** its-hpc@pomona.edu
- **Subject line:** "Help with VS Code + Sagehen setup"
- **Include:**
  - Exact error message (copy-paste)
  - Your operating system
  - Which step you're stuck on
  - What you've already tried

### Summary: You're Ready When...

- VS Code is installed and launches
- Remote-SSH extension is installed
- You can SSH to Sagehen from terminal: `ssh sagehen`
- SSH config file exists at ~/.ssh/config

Once you've confirmed all these items, you're ready for the workshop!

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
