---
title: Reference
---

## VS Code Keyboard Shortcuts

### Essential Shortcuts for Remote Development

| Action | Windows/Linux | macOS |
|--------|---------------|-------|
| Command Palette | Ctrl+Shift+P | Cmd+Shift+P |
| Quick Open (find file) | Ctrl+P | Cmd+P |
| Save file | Ctrl+S | Cmd+S |
| Toggle Sidebar | Ctrl+B | Cmd+B |
| Toggle Terminal | Ctrl+` | Cmd+` |
| Open terminal | Ctrl+Shift+` | Cmd+Shift+` |
| Split editor | Ctrl+\ | Cmd+\ |
| New terminal | Ctrl+Shift+` | Cmd+Shift+` |
| Go to line | Ctrl+G | Ctrl+G |
| Find | Ctrl+F | Cmd+F |
| Find in files | Ctrl+Shift+F | Cmd+Shift+F |
| Find and replace | Ctrl+H | Cmd+H |

## Remote-SSH Configuration

### SSH Config Syntax

Located at `~/.ssh/config` on your local machine:

```
Host sagehen
    HostName sagehen.hpc.pomona.edu
    User your_username
    IdentityFile ~/.ssh/id_sagehen
    ServerAliveInterval 300
    ServerAliveCountMax 2
```

Key options:
- **Host** - Alias you use in VS Code
- **HostName** - Full cluster domain
- **User** - Your Pomona username
- **IdentityFile** - Path to your SSH private key
- **ServerAliveInterval** - Keep connection alive (300 = 5 minutes)
- **ServerAliveCountMax** - Max missed pings before disconnect (2)

### Connecting to Sagehen from VS Code

1. Click the Remote Explorer icon (left sidebar)
2. Select "SSH Targets" from dropdown (if not already selected)
3. Find "sagehen" in the list
4. Click the connect icon (or right-click → Connect to Host)
5. When prompted, choose "Linux" as the platform
6. Wait for VS Code to initialize remote connection
7. A new window opens connected to Sagehen

### Tips for SSH Connection

- **First connection takes longer** - VS Code installs server components
- **DUO authentication** - Watch terminal for prompts, approve on phone
- **Connection drops** - VS Code reconnects automatically
- **Multiple windows** - Open many VS Code windows, each connected

## VS Code Extensions for HPC Work

### Recommended Extensions

| Extension | Publisher | Purpose |
|-----------|-----------|---------|
| Remote - SSH | Microsoft | Connect to remote servers |
| Python | Microsoft | Python development, debugging, linting |
| Pylance | Microsoft | Advanced Python intelligence |
| Git Graph | mhutchie | Visualize Git history |
| Better Comments | Aaron Bond | Color-code comments |
| Trailing Spaces | Sharla Grayson | Highlight trailing whitespace |
| SLURM Helper | (if available) | SLURM syntax highlighting |

### Installing Extensions

**On remote system:**
1. Open Remote Explorer (Ctrl+Shift+P → "Remote Explorer")
2. Click Extensions icon in left sidebar
3. Search for extension name
4. Install directly - it installs on Sagehen automatically

**On local system:**
- Same process, but extensions install locally (for local use)

### Recommended Settings for HPC

Edit settings (Ctrl+, or Code → Settings):

```json
{
    "editor.fontSize": 13,
    "editor.formatOnSave": false,
    "editor.autoSave": "afterDelay",
    "editor.autoSaveDelay": 2000,
    "editor.rulers": [79, 120],
    "files.trimTrailingWhitespace": true,
    "files.insertFinalNewline": true,
    "terminal.integrated.fontSize": 12,
    "terminal.integrated.scrollback": 5000,
    "[python]": {
        "editor.defaultFormatter": "ms-python.python",
        "editor.formatOnSave": true
    },
    "remote.SSH.showLoginTerminal": true,
    "remote.SSH.useLocalServer": false
}
```

Key settings for HPC:
- **autoSave** - Save regularly without asking
- **rulers** - Vertical guides at 79/120 chars (PEP8 standards)
- **terminal.scrollback** - Keep more terminal history
- **showLoginTerminal** - Show authentication prompts (critical!)

## Common VS Code Remote-SSH Tasks

### Opening a Folder on Sagehen

1. Click File → Open Folder (Remote)
2. Type the path: `/rhome/<myusername>/myproject`
3. Click "OK"
4. VS Code opens the folder

### Editing Files on Sagehen

Once connected:
- **File Explorer** (Ctrl+Shift+E) shows remote file tree
- Click files to open and edit them
- Changes sync in real-time
- File icons show status (white = unsaved)

### Running Code in Terminal

Open the integrated terminal (Ctrl+`) and run commands:

```bash
# Load modules
module load miniconda3

# Run Python script
python my_script.py

# Run Python interactively
python

# Check cluster status
sinfo
squeue -u $USER
```

### Working with Git

VS Code has excellent Git integration even on remote systems:

1. Open Source Control (Ctrl+Shift+G)
2. Initialize repo: "Initialize Repository"
3. Stage files, write commit messages, push/pull

Or from terminal:
```bash
git clone https://github.com/user/repo.git
cd repo
# Edit files...
git add .
git commit -m "message"
git push
```

## Sagehen-Specific Information

### File Paths on Sagehen

```bash
/rhome/<myusername>       # Your home directory (100GB, backed up)
/bigdata/lab/<labname>       # Lab storage (1TB shared, backed up)
/scratch/your_username     # Fast temporary (SSD, not backed up)
/tmpfs                     # RAM-based temp (ultra-fast, not backed up)
```

For this workshop, edit files in `/rhome/<myusername>`.

### Module System (Lmod)

Load software tools in terminal:

```bash
# View available modules
module avail
module avail python
module avail gcc

# Load modules
module load miniconda3
# gcc is available system-wide on Sagehen -- no module load needed
module load openmpi

# See what's loaded
module list

# Unload
module unload gcc
module purge              # Remove all

# Save/restore environments
module save myenv
module restore myenv
```

### SLURM Job Submission

From the VS Code terminal, submit jobs:

```bash
# Simple job
sbatch my_script.sbatch

# Check queue
squeue -u $USER

# Job details
scontrol show job JOB_ID

# Cancel job
scancel JOB_ID

# View completed jobs
sacct -u $USER --format=jobid,jobname,state,elapsed
```

### Sample SBATCH Script

Create a file `my_job.sbatch`:

```bash
#!/bin/bash
#SBATCH --job-name=analysis
#SBATCH --output=logs/job_%j.log
#SBATCH --time=01:00:00
#SBATCH --cpus-per-task=4
#SBATCH --mem=8G
#SBATCH --partition=amd

module load miniconda3
python my_analysis.py --input data.csv
```

Submit with: `sbatch my_job.sbatch`

## Troubleshooting Connection Issues

### General Troubleshooting Steps

1. **Verify local SSH works** first:
   ```bash
   ssh sagehen
   # (type exit to disconnect)
   ```

2. **Check VS Code output**:
   - View → Output
   - Select "Remote-SSH" from dropdown
   - Look for error messages

3. **Try reconnecting**:
   - Click Remote indicator (bottom-left)
   - Select "Close Remote Connection"
   - Reconnect

4. **Restart VS Code**:
   - File → Exit
   - Reopen VS Code
   - Reconnect

### Common Issues and Solutions

| Issue | Cause | Solution |
|-------|-------|----------|
| "Could not establish connection" | SSH config or network issue | Verify `ssh sagehen` works in terminal |
| "Authentication failed" | Wrong password or expired DUO code | Check caps lock, try new DUO code |
| "Permission denied (publickey)" | SSH key problem | Try password-only auth, check key permissions |
| "Operation timed out" | Network/firewall blocking | Check WiFi, try USB tether, contact IT |
| "VS Code hangs at login" | Remote-SSH not showing terminal | Enable `remote.SSH.showLoginTerminal` in settings |
| "Terminal commands not found" | Modules not loaded | Run `module load miniconda3` in terminal |

### Debug Information to Collect

If contacting HPC support:

1. **Error message** - Copy the exact text from VS Code Output panel
2. **Your setup** - OS, VS Code version, Remote-SSH version
3. **What works** - Can you `ssh sagehen` from terminal?
4. **Steps taken** - What have you already tried?

Contact: **its-hpc@pomona.edu**

## File Transfer Between Local and Sagehen

### Using SCP from Terminal

```bash
# Copy local file to Sagehen home
scp myfile.txt sagehen:~/

# Copy from Sagehen to local
scp sagehen:~/myfile.txt ./

# Copy entire directory
scp -r sagehen:~/myproject ./myproject_copy

# Copy with progress
scp -v sagehen:~/largefile.tar.gz ./
```

### Using VS Code File Explorer

1. Open folder on Sagehen (File → Open Folder Remote)
2. Right-click a file → "Download..." to get it locally

Or drag-and-drop files between VS Code window and file explorer.

## Python Development on Sagehen

### Selecting Python Interpreter

1. Open Command Palette (Ctrl+Shift+P)
2. Type "Python: Select Interpreter"
3. Choose from available environments
4. Or choose "Enter interpreter path..." for custom

### Running Python Code

**Interactive terminal:**
```bash
python
>>> import numpy as np
>>> np.array([1, 2, 3])
```

**Run script:**
```bash
python my_script.py
```

**Debug (set breakpoints):**
1. Click left of line number to set breakpoint (red dot)
2. Press F5 (or click Run)
3. VS Code stops at breakpoint
4. Use Debug Console to inspect variables

### Virtual Environments

Create and use Python venvs:

```bash
# Create venv
python -m venv myenv

# Activate
source myenv/bin/activate

# Install packages
pip install numpy pandas scipy

# Deactivate
deactivate
```

VS Code's interpreter picker finds and uses venvs automatically.

## Resources and Support

### Documentation
- **VS Code Remote-SSH**: https://code.visualstudio.com/docs/remote/ssh
- **VS Code Settings**: https://code.visualstudio.com/docs/getstarted/settings
- **SLURM Manual**: https://slurm.schedmd.com/sbatch.html
- **Sagehen Cluster**: https://pomona-college.github.io/

### Getting Help
- **Email**: its-hpc@pomona.edu
- **Instructor**: Andrew Wilson
- **OnDemand**: https://ondemand.hpc.pomona.edu/ (web interface alternative)

### Useful Commands

```bash
# Check cluster status
sinfo

# Your account info
sacctmgr show user $USER

# Disk usage
du -sh /rhome/$USER
du -sh /scratch/$USER

# Check modules
module avail

# View recent jobs
sacct -u $USER --format=jobid,jobname,state,elapsed --units=M
```

## Tips for Productive HPC Workflow

1. **Use terminal in VS Code** - Stays in your project folder
2. **Keep files on Sagehen** - Avoid syncing large files locally
3. **Test scripts locally first** - Easier debugging on your machine
4. **Use SLURM for real work** - Terminal is for testing
5. **Monitor jobs frequently** - Catch errors early with `squeue`
6. **Save logs** - Use `#SBATCH --output` to capture job output
7. **Backup important files** - Use `/rhome` (backed up) not `/scratch`

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
