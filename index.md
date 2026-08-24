---
title: 'VS Code Remote-SSH for HPC'
subtitle: 'A modern IDE for working on the Sagehen HPC cluster'
---

## Welcome!

This workshop teaches you how to use Microsoft VS Code with the Remote-SSH extension to develop and run code on the Pomona College Sagehen HPC cluster. VS Code Remote-SSH provides a full integrated development environment (IDE) experience while working on remote systems, combining the power of a modern editor with direct access to your HPC cluster.

## Why take this workshop?

After this workshop, you will be able to:

- Install and configure VS Code with the Remote-SSH extension
- Connect securely to the Sagehen HPC cluster using DUO MFA
- Edit remote files using VS Code's powerful editor features
- Use VS Code's integrated terminal to run SLURM commands and monitor jobs
- Install and use extensions for Python, R, Jupyter, and Git workflows
- Understand when VS Code Remote-SSH is the right tool for HPC work

## What you'll need

- **Your own laptop** (Windows, Mac, or Linux)
- **A Pomona College HPC account** on Sagehen cluster
- **VS Code installed** on your local machine
- **SSH access credentials** for the cluster
- **DUO MFA enabled** on your account (required by Sagehen)
- **30-45 minutes** for the full workshop

## Workshop structure

This workshop is organized as follows:

| Episode | Time | Topic |
|---------|------|-------|
| 1 | 15 min + 5 ex | Why VS Code Remote-SSH? Comparison with alternatives |
| 2 | 20 min + 10 ex | Installation and configuration on all platforms |
| 3 | 25 min + 15 ex | Connecting to Sagehen with DUO authentication |
| 4 | 20 min + 10 ex | Editing files, creating projects, file management |
| 5 | 20 min + 15 ex | Using the integrated terminal and SLURM commands |
| 6 | 25 min + 10 ex | Adding extensions and customizing your environment |

**Total teaching time: ~2 hours** (plus exercises)

## Getting help

If you encounter issues during the workshop:

- **Email**: its-hpc@pomona.edu
- **Slack**: #hpc-help (Pomona CS Slack)
- **Office hours**: See ITS-HPC website for Andrew Wilson's availability
- **Known issues**: See the reference section for common problems and solutions

## Before you begin

Please complete the following:

1. **Ensure you have an HPC account**: Log into [Sagehen cluster documentation](https://pomona-college.github.io/) to verify your account status
2. **Enable DUO MFA**: If you haven't already, register your device at duo.pomona.edu
3. **Test SSH access**: From your terminal, try: `ssh <myusername>@sagehen.hpc.pomona.edu` (this will confirm your access works)
4. **Download VS Code**: From [code.visualstudio.com](https://code.visualstudio.com)

Ready to get started? Let's dive into why VS Code is such a powerful tool for HPC work!

---

**Questions or suggestions?** Please contact its-hpc@pomona.edu or open an issue on our GitHub repository.

<!-- highlight <labname>/<myusername> placeholders in code blocks; remove if the varnish theme handles this natively -->
<script>(function(){var CSS='.sh-placeholder{color:#c2410c;font-weight:700}[data-bs-theme="dark"] .sh-placeholder,html.dark .sh-placeholder{color:#fdba74}@media (prefers-color-scheme: dark){[data-bs-theme="auto"] .sh-placeholder{color:#fdba74}}';var RX=/<labname>|<myusername>/g;function firstMatch(el){var w=document.createTreeWalker(el,NodeFilter.SHOW_TEXT,null),nodes=[],full='';while(w.nextNode()){nodes.push({n:w.currentNode,s:full.length});full+=w.currentNode.nodeValue;}RX.lastIndex=0;var m;while((m=RX.exec(full))){var s=m.index,e=s+m[0].length,inSpan=false,parts=[];for(var j=0;j<nodes.length;j++){var ns=nodes[j].s,ne=ns+nodes[j].n.nodeValue.length;if(ne<=s||ns>=e)continue;parts.push({node:nodes[j].n,a:Math.max(s-ns,0),b:Math.min(e-ns,nodes[j].n.nodeValue.length)});var p=nodes[j].n.parentNode;while(p&&p!==el){if(p.classList&&p.classList.contains('sh-placeholder')){inSpan=true;break;}p=p.parentNode;}}if(!inSpan&&parts.length)return parts;}return null;}function wrapParts(parts){for(var i=parts.length-1;i>=0;i--){var t=parts[i].node,txt=t.nodeValue,a=parts[i].a,b=parts[i].b;var span=document.createElement('span');span.className='sh-placeholder';span.textContent=txt.slice(a,b);var f=document.createDocumentFragment();if(a>0)f.appendChild(document.createTextNode(txt.slice(0,a)));f.appendChild(span);if(b<txt.length)f.appendChild(document.createTextNode(txt.slice(b)));t.parentNode.replaceChild(f,t);}}function run(){var st=document.createElement('style');st.textContent=CSS;document.head.appendChild(st);document.querySelectorAll('pre,code').forEach(function(el){var guard=0,parts;while((parts=firstMatch(el))&&guard++<500){wrapParts(parts);}});}if(document.readyState==='loading'){document.addEventListener('DOMContentLoaded',run);}else{run();}})();</script>
