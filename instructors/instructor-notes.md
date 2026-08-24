---
title: 'Instructor Notes'
---

## Overview

This workshop teaches HPC practitioners how to use VS Code Remote-SSH to develop code on the Sagehen cluster. Total time: ~3 hours including breaks and challenges.

**Target audience:** Pomona College researchers and students using Sagehen HPC cluster

**Prerequisites:**
- Pomona HPC account on Sagehen
- Basic terminal familiarity (can use terminal, know how to navigate directories)
- Basic understanding of SSH
- DUO MFA enabled

## Learning Outcomes

After this workshop, learners can:

1. Install VS Code and Remote-SSH extension
2. Configure SSH to connect to Sagehen
3. Use VS Code as a remote editor for cluster files
4. Use VS Code's integrated terminal for SLURM commands
5. Install and configure extensions for their workflow
6. Manage their remote development environment

## Episode Guide

### Episode 1: Why VS Code Remote-SSH (20 min teaching + 5 min challenges)

**Main message:** VS Code Remote-SSH provides a powerful IDE experience for HPC development, balancing ease of use with professional features.

**Key points:**
- Explain the local-UI, remote-server model
- Show diagram of how VS Code connects
- Compare to nano, vim, MobaXterm, OnDemand
- Emphasize that VS Code is the recommended tool at Pomona

**Live demo (if time):**
- Show VS Code interface with remote connection open
- Open a file and highlight syntax highlighting
- Show file browser vs. command line
- Show integrated terminal

**Common misconceptions:**
- "Isn't VS Code just a text editor?" No, it has IDE features like intellisense, debugging, extensions
- "Do I need internet for Remote-SSH?" Only to connect; then you can work offline temporarily
- "Won't it be slow?" No, the UI runs locally, only file operations are remote

**If learners ask about:**
- **Cloud editors (JupyterHub, OnDemand):** Mention they're different tools for different use cases. VS Code is best for traditional HPC workflows with SLURM.
- **Local development:** Yes, you can use VS Code locally too! But this workshop focuses on remote development.
- **Why VS Code vs. alternatives:** Combination of ease of use + power + free + active community.

### Episode 2: Installation and Setup (30 min teaching + 10 min challenges)

**Main message:** Installation is straightforward; the critical part is SSH configuration and DUO setup.

**Key points:**
- VS Code installation is simple (download and install)
- SSH configuration is the "hard" part (but still easy with a template)
- **CRITICAL:** `remote.SSH.showLoginTerminal` must be checked for DUO
- Testing SSH from terminal before using VS Code is essential

**Live demo:**
- Show yourself installing VS Code (or use screenshots)
- Walk through creating ~/.ssh/config step by step
- Show the critical setting in VS Code settings
- Show successful SSH connection from terminal

**Common issues to address:**
- "I created ~/.ssh/config but I don't see it" → It's hidden, use `ls -la` or file explorer "show hidden files"
- "SSH works from terminal but not VS Code" → Check `remote.SSH.showLoginTerminal` first
- "Where do I save ~/.ssh/config?" → Show path in their file system (C:\Users\username\.ssh on Windows, ~/.ssh on Mac/Linux)
- "DUO is asking for 'Passcode or other option'" → Explain that codes expire in 30 seconds, so "call" option is helpful

**Teaching tips:**
- Have learners do this step-by-step with you
- Wait for everyone to finish each step before moving on
- Circulate and help those struggling with file editors
- Have pre-made config file on clipboard to save time

### Episode 3: Connecting to Sagehen (40 min teaching + 15 min challenges)

**Main message:** Connection process is intuitive; understanding what's happening helps troubleshoot.

**Key points:**
- Remote Explorer is the starting point
- "Select Platform" always choose Linux for Sagehen
- DUO happens in the terminal (because `showLoginTerminal` is checked)
- Status indicator shows connection state
- Disconnection and reconnection are easy

**Live demo:**
- Do the full connection process on projector
- Show each prompt and explain what's happening
- Enter DUO authentication step-by-step
- Show successful connection (green indicator)
- Open a folder
- Disconnect and reconnect

**Troubleshooting during challenges:**
- If someone can't authenticate, first verify `ssh sagehen` works from terminal
- If terminal doesn't appear, check the critical setting again
- If connection hangs, it's usually DUO issue (phone not responding, account not registered)
- Have them call its-hpc@pomona.edu if needed

**Common issues:**
- "Where's the terminal?" → Bottom of screen, may be minimized. Click terminal panel or press Ctrl+`
- "DUO didn't send a code" → Click "call me" option instead
- "I typed my password wrong" → Disconnect and try again
- "It says 'Select Platform' but I only see Linux" → That's the one you want! Click it.

### Episode 4: File Editing (30 min teaching + 10 min challenges)

**Main message:** VS Code's file editing features make managing HPC projects much easier than command-line editors.

**Key points:**
- Explorer sidebar shows remote file structure
- Quick Open (Ctrl+P) is faster than file browser
- Syntax highlighting helps catch errors
- Multi-file editing with tabs is powerful
- Search/replace across files is much better than nano

**Live demo:**
- Create a new file in Explorer
- Open an existing file using Quick Open
- Show syntax highlighting
- Edit file and show IntelliSense suggestions (with Python extension)
- Split editor and show side-by-side editing
- Find and replace across files

**Tips for teaching:**
- Spend time on Quick Open; it's a game-changer
- Show drag-and-drop upload (visually impressive)
- Explain that changes auto-save (after delay) or with Ctrl+S
- Show how to compare files (useful for reviewing edits)

**Common confusions:**
- "Is the file on my computer or Sagehen?" → On Sagehen! You're editing a remote file with local UI.
- "Do I need to save?" → Yes, even though VS Code shows auto-save. Manual save with Ctrl+S is fine.
- "Can I drag files from my laptop?" → Yes! That's uploading them to Sagehen.

### Episode 5: Integrated Terminal and SLURM (35 min teaching + 15 min challenges)

**Main message:** The integrated terminal lets you manage jobs while editing code; a huge productivity boost.

**Key points:**
- Terminal runs on Sagehen (not local)
- SLURM commands (sbatch, squeue, scancel) work normally
- Multiple terminal tabs and splits help organize work
- Job monitoring while editing is powerful
- tmux adds persistence if disconnected

**Live demo:**
- Open terminal with Ctrl+`
- Show working directory is on Sagehen
- Run `whoami` and `pwd` to verify
- Submit a simple job with sbatch
- Check with squeue
- Show multiple terminals
- Show job output monitoring

**Real workflow demo:**
- Have a Python file open in editor
- Submit job in terminal
- Make changes to Python file while job runs
- Check job status in another terminal
- View results

**Tips:**
- Spend time on sbatch; this is core HPC skill
- Show the difference between interactive and batch jobs
- Explain why batch jobs are better for Sagehen (shared resource)
- tmux is advanced; only cover if time permits

**Common issues:**
- "Terminal opened but I'm still on my computer" → Wrong! You're on Sagehen. Run `whoami` to verify.
- "sbatch failed; command not found" → May need to load modules first
- "My job disappeared from squeue" → It probably finished or was canceled
- "How do I see job output?" → Tail the log file specified in SBATCH directive

### Episode 6: Extensions and Customization (35 min teaching + 10 min challenges)

**Main message:** Extensions make VS Code your personal IDE; choose ones for your workflow.

**Key points:**
- Local vs. remote extensions serve different purposes
- Python extension on remote enables intellisense for cluster code
- Other extensions enhance based on your needs
- Customization is personal; show options, let people choose

**Live demo:**
- Install Python extension on remote
- Show intellisense working with Python code
- Show different color themes
- Show keyboard shortcuts customization
- Show settings.json (JSON, not scary)

**Teaching tips:**
- Emphasize that extensions are optional (not required)
- Python/R/Jupyter are recommended but not required
- Themes are purely visual; pick what feels good
- Don't spend too much time on settings.json; UI settings are easier

**Extensions discussion:**
- Ask: "What are you coding in?" and recommend accordingly
- Python users → Python extension essential
- R users → R extension essential
- Jupyter users → Jupyter extension
- All users → GitLens useful if using Git
- Show that Markdown Preview is useful for documentation

**Customization ideas:**
- Show a few themes and let people pick
- Suggest popular shortcuts (Go to Line)
- Mention Settings Sync for keeping setup consistent across machines

## Timing and Pacing

Use this timeline:

| Time | Activity | Duration |
|------|----------|----------|
| 0:00-0:05 | Opening, goals, setup check | 5 min |
| 0:05-0:30 | Episode 1 (Why VS Code) | 25 min |
| 0:30-1:00 | Episode 2 (Installation) | 30 min |
| 1:00-1:10 | Break | 10 min |
| 1:10-1:50 | Episode 3 (Connecting) | 40 min |
| 1:50-2:20 | Episode 4 (Editing) | 30 min |
| 2:20-2:30 | Break | 10 min |
| 2:30-3:05 | Episode 5 (Terminal) | 35 min |
| 3:05-3:40 | Episode 6 (Extensions) | 35 min |
| 3:40-3:50 | Wrap-up, Q&A | 10 min |

**Flexibility:**
- If people are comfortable with SSH, speed up Episode 2
- If many people already use VS Code locally, speed up Episode 1
- If cluster is down, use pre-recorded videos or slides
- Episode 6 can be shortened if time is tight

## Contingencies

### What if Sagehen is down?

1. Use screenshots and pre-recorded videos
2. Show the connection process conceptually
3. Discuss how to handle disconnections and reconnections
4. Have learners install VS Code and Remote-SSH locally
5. Show them how to connect to other systems (GitHub Codespaces, personal server)

### What if someone can't connect?

1. Have them pair with a neighbor
2. Continue with the workshop
3. Troubleshoot after with email follow-up
4. Document the issue to improve future workshops

### What if network is unstable?

1. Have offline materials (printed guides, screenshots)
2. Pre-stage example files so people can edit locally
3. Record the session for those who lose connection
4. Have discussion-based content prepared as backup

### What if DUO isn't working?

1. Contact its-hpc@pomona.edu immediately
2. Teach terminal-based workflow instead
3. Discuss how to troubleshoot MFA issues
4. Plan follow-up session when DUO is working

## Learner Questions and Answers

**Q: Can I use VS Code for local development too?**
A: Absolutely! VS Code is great for local development. When working locally, you don't use Remote-SSH; you just edit files directly. The principles are the same.

**Q: What if I already know vim? Should I learn VS Code?**
A: They're different tools. Vim is powerful but has a learning curve. VS Code is more intuitive but less keyboard-centric. Both are valid; use what works for you!

**Q: Do I need to pay for VS Code?**
A: No! VS Code is completely free and open-source. Some extensions are also free; some premium ones exist but aren't necessary.

**Q: Will my workflow be slower if I use VS Code instead of terminal editors?**
A: Usually faster! You spend less time figuring out editor commands and more time coding.

**Q: Can I use VS Code on my laptop AND the cluster?**
A: Yes! Install VS Code locally for local development, then use Remote-SSH to connect to clusters. It's the best of both worlds.

**Q: What about collaborative coding?**
A: VS Code Live Share extension allows real-time collaboration. Not covered in this workshop but worth exploring.

**Q: Do I need to learn all the extensions?**
A: No. Start with Python or R extension for your language, then add others as you need them.

**Q: Is VS Code suitable for all programming languages?**
A: Yes! VS Code supports virtually all languages through extensions. Not all have built-in support, but they're available.

## Facilitator Tips

### Before the Workshop
- Test your setup end-to-end the day before
- Have slides or handouts printed
- Know the cluster status (email its-hpc@pomona.edu)
- Have contact info ready for troubleshooting
- Silence your phone

### During the Workshop
- Start on time, end on time (respect attendees' schedules)
- Do live demos; they're more engaging than slides
- Pause for challenges and give sufficient time (10 min for challenges)
- Walk around during challenges to help and observe
- Ask for questions frequently; create psychologically safe environment
- Use the projector to troubleshoot issues (if appropriate) so others learn
- Call on different people so everyone feels engaged

### Handling Difficulties
- If someone struggles with SSH, it's probably a path or permissions issue
- If someone struggles with DUO, have them verify registration first
- If someone can't connect, suggest pairing while you troubleshoot email
- If you make a typo or mistake, own it! "Oops, I meant X. Good catch if you noticed!"

### After the Workshop
- Send follow-up email with resources and links
- Ask for feedback (survey)
- Note any issues that came up
- Offer office hours for additional questions
- Iterate for next workshop based on feedback

## Assessment

### Informal Assessment (during workshop)
- Observe learners during challenges
- Note who completes them quickly vs. struggles
- Ask clarifying questions: "What does this step do?"
- Look for signs of understanding or confusion

### Formal Assessment (optional)
- Quick quiz on key concepts (optional)
- Have learners demonstrate: connect to Sagehen, edit file, run command in terminal
- Collect feedback survey

### Sample Survey
1. What was the most useful part of this workshop?
2. What was confusing or difficult?
3. Will you use VS Code for your HPC work? (Yes/No/Maybe)
4. What other topics would help you?
5. Overall, how helpful was this workshop? (1-5 scale)

## Resources for Instructors

- **VS Code Docs**: https://code.visualstudio.com/docs/
- **Remote-SSH Docs**: https://code.visualstudio.com/docs/remote/ssh
- **SLURM Documentation**: https://slurm.schedmd.com/sbatch.html
- **Sagehen HPC Docs**: https://pomona-college.github.io/
- **Git/GitHub Guides**: https://guides.github.com/

## Customizing for Other Clusters

To adapt this workshop for another HPC cluster:

### Search and replace:
- "sagehen" → "your_cluster_name"
- "sagehen.hpc.pomona.edu" → "your_cluster_hostname"
- "Pomona College" → "Your Institution"
- "its-hpc@pomona.edu" → "Your HPC support email"
- "/rhome/" → "Your home directory path"

### Modify content:
- Replace DUO references with your MFA system
- Update SLURM references if using different job scheduler
- Change module system examples if different
- Update resource limits and partition names

### Add institution-specific content:
- Your cluster policies
- Your specific examples and data
- Your support structures
- Local examples and use cases

## Notes on Specific Topics

### DUO Authentication
- Some learners won't have DUO registered yet; have them do it before workshop
- DUO codes expire in 30 seconds; emphasize urgency if using codes
- "Call me" option is more forgiving for network issues
- Some phones may have issues with DUO app; test beforehand

### SSH Keys
- Optional but recommended for frequent users
- Many beginners struggle with SSH keys; provide good template
- Can generate keys after workshop in follow-up session
- Don't make keys required; password + DUO works fine

### SLURM
- Different cluster may have different partitions, resources, modules
- Show `sinfo` output so learners understand what's available
- Resource limits vary; adjust examples accordingly
- Some clusters may have different job submission syntax

### Python/R Extensions
- Python extension requires Python installed on remote
- May need `pip install pylint` or similar for linting
- R extension requires R installed on remote
- Some extensions may require additional configuration

## Final Tips

1. **Be patient**: Some learners will struggle with terminal/SSH concepts. That's normal.
2. **Celebrate progress**: When someone connects successfully, acknowledge it!
3. **Provide support**: You're not just teaching VS Code; you're enabling better HPC workflows.
4. **Iterate**: Each workshop improves the next one based on learner feedback.
5. **Have fun**: This is genuinely useful stuff; enthusiasm is contagious!

Remember: The goal isn't to make everyone an expert in 3 hours. It's to introduce VS Code as a tool and get learners comfortable enough to explore on their own.
