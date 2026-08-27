---
title: "Integrated Terminal"
teaching: 20
exercises: 15
---

:::::::::::::::::::::::::::::::::::::: questions

- How do I use the integrated terminal in VS Code?
- How do I submit and monitor SLURM jobs from VS Code?
- How do I use multiple terminal panes for the edit-submit-monitor workflow?
- How do I activate conda environments and load modules cleanly?

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Open and use VS Code's integrated terminal on Sagehen HPC
- Run SLURM commands (sbatch, squeue, scancel, seff)
- Use multiple terminal tabs and split terminals for parallel workflows
- Configure a custom terminal profile that auto-loads your conda environment
- Recover gracefully from disconnects and dropped sessions

::::::::::::::::::::::::::::::::::::::::::::::

## Why the Integrated Terminal Matters for HPC

When you connect to Sagehen with VS Code Remote-SSH, the editor pane edits files on the cluster but does not, on its own, give you a way to run commands there. The integrated terminal is the bridge. It opens a real shell on the Sagehen login node, in the same SSH session your editor is using. That means everything you type in the terminal sees exactly the files you are editing, with no synchronization step.

This tight coupling is the entire reason VS Code Remote-SSH is more productive for HPC work than editing locally and rsyncing changes. The code you save is immediately the code you can run. The job you submit immediately reads the script you just changed.

## Opening the Terminal

Press **Ctrl+`** (backtick, the key above Tab on most keyboards) to open the integrated terminal. When connected to Sagehen, the prompt confirms you are on the cluster:

```
<myusername>@sagehen-login-1:~$
```

This is your Sagehen login node shell. The terminal starts in your home directory (`/rhome/<myusername>`). Your usual `.bashrc` or `.zshrc` runs, so any aliases, PATH additions, or `module load` lines you have configured take effect.

::::::::::::::::::::::::::::::::::::: callout
**Login node etiquette**

The integrated terminal runs on the **login node**, not a compute node. The login node is shared by every Sagehen user and is meant for editing, submitting jobs, light file operations, and small tests. Do not run heavy compute, training, or data processing in this terminal. If you need an interactive compute environment, request one with `srun --partition=short --time=00:30:00 --pty bash` and the terminal will move to a compute node for the duration of that session.
::::::::::::::::::::::::::::::::::::::::::::::::

## Running SLURM Commands

The five commands you will use most:

### Submit a job

```bash
sbatch my_script.sh
# Output: Submitted batch job 12345
```

### Check job status

```bash
squeue -u $USER              # All your jobs
squeue -j 12345              # Specific job
squeue -u $USER --start      # Estimated start times for pending jobs
```

### Monitor output in real time

```bash
tail -f slurm-12345.out      # Watch output; Ctrl+C to stop
```

### Cancel a job and check history

```bash
scancel 12345                # Stop one job immediately
scancel -u $USER             # Stop all of your jobs (use with care)
sacct -u $USER --format=jobid,jobname,state,elapsed,maxrss  # Recent jobs
seff 12345                   # CPU and memory efficiency of completed job
```

`seff` is the unsung hero of resource tuning. After a job completes, `seff JOBID` reports actual CPU efficiency, memory used vs requested, and wall time. Running it on every completed job for a week will reshape how you write SLURM scripts; most users overestimate memory by 4 to 10x.

![`seff` on a finished test job: near-zero CPU and memory efficiency is your cue to shrink the next request. (This example ended in TIMEOUT because the test deliberately overran its 5-minute limit.)](fig/07-seff-job-efficiency.png){alt='Terminal output of seff for a job on cluster hpc. The job ended in TIMEOUT state after five minutes of wall-clock time, used zero percent of its CPU core-walltime across two cores, and utilized under four megabytes of the one gigabyte requested.'}

## Multiple Terminals for the Real Workflow

A single terminal forces you to choose between editing focus and monitoring focus. Multiple terminals let you do both at once.

### Multiple terminal tabs

Click the **+** icon next to the terminal name to open additional terminals. Each is an independent shell on Sagehen.

A common configuration: one terminal for submitting jobs, a second for `watch squeue -u $USER` to see queue state update every 2 seconds, a third running `tail -f slurm-*.out` to watch the active job's output.

### Split terminal

Right-click the terminal area and choose **Split Terminal**, or press **Ctrl+Shift+5**, to put two shells side-by-side in the same panel. Both run independently on Sagehen. This is especially useful when you want to compare two log files or two job outputs at the same time without flipping tabs.

### Renaming and reordering

Right-click a terminal name to rename it ("submit", "monitor", "logs"). Drag tabs in the terminal sidebar to reorder. With four or five terminals open, named tabs are the difference between a productive session and a confusing one.

## Custom Terminal Profiles

By default, the integrated terminal runs `bash` (or `zsh`) with your default profile. You can define custom profiles that auto-activate a conda environment or load specific modules. Open Settings (Ctrl+,) and search for "terminal.integrated.profiles.linux", then click "Edit in settings.json":

```json
"terminal.integrated.profiles.linux": {
    "bash (default)": {
        "path": "bash"
    },
    "ml-env": {
        "path": "bash",
        "args": ["-l", "-c", "module load miniconda3 && conda activate ml_env && exec bash"]
    },
    "gpu-interactive": {
        "path": "bash",
        "args": ["-l", "-c", "srun --partition=gpu --gres=gpu:l40s:1 --time=02:00:00 --pty bash"]
    }
}
```

Now the **+** dropdown in the terminal panel offers three profiles. Picking "ml-env" opens a terminal with conda already activated. Picking "gpu-interactive" requests an L40S for 2 hours and drops you into a shell on a compute node.

::::::::::::::::::::::::::::::::::::: callout
**Login vs interactive vs SLURM-allocated shells**

Three different shell types behave differently:

- **Login shell** (default new terminal): runs `.bash_profile` and `.bashrc`. On the shared login node. No GPU access. Good for editing and submitting.

- **Interactive shell with srun**: runs on a compute node. Allocated CPU/GPU/memory until you exit. Counts against your job allocation. Good for debugging a job that crashes inside SLURM.

- **Inside an `sbatch` script**: only runs `.bashrc`, not `.bash_profile`. If a script that works in your interactive shell fails inside `sbatch`, the difference is usually a missing `module load` or `conda activate` that lives in `.bash_profile`. Move it to `.bashrc` or load it explicitly in the SLURM script.
::::::::::::::::::::::::::::::::::::::::::::::::

## Recovering from Disconnects

The integrated terminal session lives inside the SSH connection. If your laptop sleeps, the wifi drops, or VS Code closes, the connection breaks. Two strategies for surviving disconnects:

### Reconnect quickly

VS Code's Remote-SSH extension detects the broken connection and offers to reconnect. Most of the time this works and you pick up where you left off, but commands that were running in the terminal at the moment of disconnect are killed.

### Use tmux for persistence

For longer interactive sessions where losing the terminal would hurt, run `tmux` (preinstalled on Sagehen):

```bash
tmux new -s work          # start a session named "work"
# ... do things, run commands ...
# Ctrl+b d to detach (session keeps running)

# Later, after a disconnect:
tmux attach -t work       # resume the session
```

`tmux` keeps your shell, processes, and scrollback alive on the login node even after VS Code disconnects. This is the only reliable way to run a long-running interactive command (such as `python -i` for an analysis session) without fear of losing it. Note that `tmux` does not protect SLURM jobs themselves; those run on compute nodes and are managed by SLURM regardless of your terminal state.

## Terminal Keyboard Shortcuts

| Action | Windows/Linux | Mac |
|--------|---------------|-----|
| Toggle terminal | Ctrl+` | Cmd+` |
| New terminal | Ctrl+Shift+` | Cmd+Shift+` |
| Split terminal | Ctrl+Shift+5 | Cmd+Shift+5 |
| Switch between terminals | Alt+Up/Down | Cmd+Up/Down |
| Clear screen | Ctrl+L | Cmd+K |
| Kill terminal | (close icon) | (close icon) |
| Reverse search history | Ctrl+R | Ctrl+R |

## The Edit-Submit-Monitor Workflow

::::::::::::::::::::::::::::::::::::: callout

## Integrated Development and Job Monitoring

1. **Edit** your script in the VS Code editor
2. **Submit** with `sbatch` in terminal 1
3. **Monitor** queue state with `watch squeue -u $USER` in terminal 2
4. **Tail** output with `tail -f slurm-JOBID.out` in terminal 3
5. **Review** results when the job completes
6. **Iterate**: edit your script and resubmit

This tight loop is why VS Code Remote-SSH is so productive for HPC work.

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge: Submit and Monitor a Job

1. Create `simple_job.sh` in the editor:

   ```bash
   #!/bin/bash
   #SBATCH --job-name=test_job
   #SBATCH --partition=short
   #SBATCH --time=00:05:00
   #SBATCH --cpus-per-task=1
   #SBATCH --mem=1G

   echo "Hello from $(hostname)"
   sleep 30
   echo "Job complete!"
   ```

2. In the terminal: `chmod +x simple_job.sh && sbatch simple_job.sh`
3. Open a second terminal tab and run `watch -n 2 squeue -u $USER`
4. When the job runs, open a third tab: `tail -f slurm-*.out`
5. After completion, run `seff JOBID` to see efficiency

::::::::::::::::::::::::::::::::::::: solution

## Solution

![The whole workflow in three split terminals: sbatch on the left, squeue in the middle, `tail -f` on the log at right.](fig/07-three-terminals-submit-monitor-tail.png){alt='VS Code's terminal panel split into three panes, all connected to Sagehen. The left pane creates and submits a job script to the short partition, the middle pane shows squeue output with the job running on node a002, and the right pane tails the slurm output files ending with Job complete.'}

After `sbatch`, you see "Submitted batch job 12345". The watch terminal shows the job with state `PD` (pending) briefly and then `R` (running). The tail terminal shows "Hello from a005" (or another node) and after 30 seconds "Job complete!". `seff 12345` reports CPU efficiency near 0% (the job mostly slept) and memory near 0 KB. This is exactly what `seff` is for: identifying jobs that overrequested resources so you can right-size future submissions.

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge: Configure a Conda Profile

Define a custom terminal profile in VS Code that opens a bash shell with a specific conda environment activated. Verify it works by checking `which python` shows the env's interpreter, not the system default.

::::::::::::::::::::::::::::::::::::: solution

## Solution

In settings.json:

```json
"terminal.integrated.profiles.linux": {
    "research-env": {
        "path": "bash",
        "args": ["-l", "-c", "module load miniconda3 && conda activate research-env && exec bash"]
    }
}
```

Open the **+** dropdown in the terminal panel, choose "research-env", and run `which python`. The output should be `/rhome/<myusername>/miniconda3/envs/research-env/bin/python` (or wherever your env lives), not `/usr/bin/python3`.

If `which python` still shows the system Python, the most common cause is that `module load miniconda3` did not run because the profile uses `-c` instead of `-l -c`. The `-l` makes bash a login shell so it sources `/etc/profile`, where the module command is defined.

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- The integrated terminal (Ctrl+`) runs on Sagehen, not your local machine
- The login node is for editing and submission only; use srun for interactive compute
- Use sbatch to submit jobs and squeue to check status from the terminal
- Multiple terminal tabs let you edit, submit, and monitor simultaneously
- Custom terminal profiles can auto-load conda envs or request interactive compute nodes
- Use `tmux` to keep interactive sessions alive across VS Code disconnects
- `seff JOBID` after job completion reveals over-provisioned resources
- The edit-submit-monitor workflow makes VS Code ideal for iterative HPC work

::::::::::::::::::::::::::::::::::::::::::::::

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
