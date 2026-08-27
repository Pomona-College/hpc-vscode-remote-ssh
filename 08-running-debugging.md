---
title: "Running and Debugging Code"
teaching: 10
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions

- How do I run code directly in the VS Code terminal?
- How do I use tmux for persistent sessions?
- What debugging workflows work well on Sagehen HPC?

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Run Python and other scripts from the integrated terminal
- Use tmux for sessions that survive disconnections
- Debug code with interactive Python and VS Code tools
- Create complete SLURM job scripts within VS Code

::::::::::::::::::::::::::::::::::::::::::::::

## Running Code in the Terminal

### Quick tests on the login node

For short tests, run code directly in the terminal:

```bash
cd /rhome/<myusername>/project
python test_script.py --quick
```

For longer computations, always submit through SLURM to avoid overloading
the login node.

### Interactive GPU sessions

For prototyping with GPU access:

```bash
srun --partition=gpu --gres=gpu:1 --mem=16G --time=01:00:00 --pty bash
module load miniconda3
python my_gpu_script.py
```

## A Complete Job Script Workflow

Create the SLURM script in the VS Code editor, then submit from the terminal:

```bash
#!/bin/bash
#SBATCH --job-name=my_analysis
#SBATCH --time=01:00:00
#SBATCH --cpus-per-task=4
#SBATCH --mem=8G
#SBATCH --output=logs/analysis_%j.log

module load miniconda3
python analysis.py --input data.csv --output results.csv
```

After submitting, check results:

```bash
ls -lh logs/               # See log files
tail logs/analysis_45678.log    # View output
head results.csv           # Preview results
```

## Using tmux for Persistent Sessions

::::::::::::::::::::::::::::::::::::: callout

## Session Persistence with tmux

tmux is a terminal multiplexer that keeps sessions running even if VS Code
disconnects.

```bash
tmux new-session -s mywork       # Create session
# Work in tmux...
# Ctrl+B D to detach (session keeps running)
tmux attach-session -t mywork    # Reattach later
tmux list-sessions               # See all sessions
```

Useful tmux commands inside a session:

- **Ctrl+B C**: Create new window
- **Ctrl+B N/P**: Next/previous window
- **Ctrl+B D**: Detach (session continues running)

::::::::::::::::::::::::::::::::::::::::::::::

## Debugging Strategies

### Interactive Python debugging

```bash
python -i my_script.py      # Start interactive mode after script runs
>>> variable_name           # Inspect variables
>>> exit()                  # Exit
```

### VS Code debugging

With the Python extension installed (see next episode), you can:

1. Set breakpoints by clicking next to line numbers (red dots appear)
2. Press F5 to start debugging
3. Step through code with F10 (step over) or F11 (step into)
4. Inspect variables in the Debug sidebar

This works for code running on Sagehen through the Remote-SSH connection.

## Common Debugging Workflow

1. Edit `analysis.py` in the VS Code editor
2. Test with a small dataset in the terminal: `python analysis.py --test`
3. Fix errors visible in the terminal output
4. When working, submit the full job: `sbatch run_analysis.sh`
5. Check output: `tail -f logs/analysis_*.log`
6. Iterate as needed

::::::::::::::::::::::::::::::::::::: challenge

## Challenge: tmux and Job Monitoring

1. Open the terminal and create a tmux session: `tmux new-session -s workshop`
2. Inside tmux, create a second window with Ctrl+B C
3. In window 0, run: `watch -n 5 squeue -u username`
4. Switch to window 1 (Ctrl+B N) for other commands
5. Detach from tmux (Ctrl+B D)
6. Reattach: `tmux attach-session -t workshop`
7. Verify your watch command is still running

::::::::::::::::::::::::::::::::::::: solution

## Solution

After detaching and reattaching, window 0 still shows the `watch` command
running with periodic `squeue` updates. This demonstrates that tmux sessions
persist through VS Code disconnections. To kill the tmux session when done:
`tmux kill-session -t workshop`.

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Run quick tests directly in the terminal; submit longer jobs through SLURM
- Use `srun` for interactive GPU sessions for prototyping
- tmux sessions persist through disconnections -- ideal for long-running monitoring
- VS Code's debugger works remotely through Remote-SSH with language extensions
- The edit-test-submit cycle is the core HPC development workflow

::::::::::::::::::::::::::::::::::::::::::::::

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
