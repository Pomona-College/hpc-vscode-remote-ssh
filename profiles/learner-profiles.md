---
title: Learner Profiles
---

## Typical Participants

### Profile 1: Graduate Student Transitioning from Local Jupyter
**Name:** Sam Thompson
**Background:** 2nd year graduate student in data science

**Motivation:**
- Currently uses Jupyter notebooks locally (8-core laptop)
- Data growing too large for laptop (~50 GB datasets)
- Needs to run on Sagehen for speed and storage
- Wants familiar IDE experience, not command-line only

**Experience:**
- Proficient in Python (pandas, scikit-learn, matplotlib)
- Used Jupyter extensively for exploratory analysis
- Has a Sagehen account but only submits SLURM jobs via shell
- Comfortable with VS Code basics locally

**Pain Point:**
"Jupyter on HPC is hard to set up. I want my full IDE, debugging tools, and Git integration on the cluster, not just a notebook."

**Expected Outcome After Workshop:**
- Connect VS Code to Sagehen directly
- Edit Python code with full IDE features (autocomplete, debugging)
- Run code interactively in integrated terminal
- Access large datasets stored on `/bigdata` and `/scratch`
- Submit SLURM jobs from VS Code without SSH'ing separately

**Preference:** Python development, will use integrated terminal heavily

---

### Profile 2: Faculty Using RStudio Desktop Locally
**Name:** Dr. Maria Gonzalez
**Background:** Associate Professor of Statistics

**Motivation:**
- Uses RStudio Desktop on local Windows machine
- Lab has large datasets (genomics) that belong on HPC
- Wants to move workflow to Sagehen HPC but keep familiar tools
- Need to collaborate with students accessing same cluster data

**Experience:**
- Expert R programmer
- Familiar with RStudio features and workflow
- Never used SSH extensively
- Limited Linux command line experience

**Pain Point:**
"RStudio Server is complicated. Can't I just use VS Code to edit R files and run them?"

**Expected Outcome After Workshop:**
- Connect VS Code to Sagehen via SSH
- Open and edit R scripts on cluster
- Run R code in VS Code terminal (using Rscript or interactive R)
- Understand file paths and folder structure on Sagehen
- Know how to use Lmod to load R and R packages
- Ability to demonstrate workflow to students

**Preference:** R development, will use terminal for data processing, may try VS Code extensions for R support

---

### Profile 3: Undergraduate CS Student with VS Code Experience
**Name:** Alex Kim
**Background:** Junior computer science major

**Motivation:**
- Uses VS Code for local class projects (C++, Python)
- Starting first research experience on Sagehen
- Wants same IDE they know locally
- Interested in learning HPC and cluster tools

**Experience:**
- Comfortable with VS Code (used in algorithms class)
- Basic Python and C++ programming
- Never used a cluster before
- Familiar with Git from computer science courses

**Pain Point:**
"I know VS Code but not HPC. I want to apply what I know locally to the cluster."

**Expected Outcome After Workshop:**
- Understand how VS Code can extend to remote servers
- Set up VS Code Remote-SSH connection independently
- Recognize differences between local and HPC workflows
- Know how to use Git on Sagehen
- Understand SLURM job submission from VS Code terminal
- Foundation for deeper HPC learning

**Preference:** Interested in all aspects, good learner, will ask system-level questions

---

### Profile 4: Researcher Frustrated with SSH-Only Workflows
**Name:** Dr. James Chen
**Background:** Postdoc in computational physics

**Motivation:**
- Currently uses pure SSH + vim for Sagehen work
- Find this workflow tedious (no syntax highlighting, hard to debug)
- Wants better development experience
- Has heard VS Code can improve this

**Experience:**
- Experienced programmer (Python, C++, MATLAB)
- Very comfortable with command line and SSH
- Advanced vim user but open to trying IDE
- Never used VS Code before

**Pain Point:**
"I can code on the cluster, but debugging and refactoring are painful without IDE features. I lose time in vim."

**Expected Outcome After Workshop:**
- See how VS Code can replace vim for some tasks
- Appreciate IDE features even for HPC work (debugging, syntax checking)
- Connect VS Code to Sagehen successfully
- Decide if VS Code workflow is better than pure SSH
- Know how to use VS Code Remote-SSH extensions
- Still comfortable with SSH if VS Code doesn't work

**Preference:** Will compare VS Code to current vim workflow, appreciates technical depth

---

### Profile 5: Undergraduate First-Time HPC User
**Name:** Jordan Rodriguez
**Background:** Senior undergrad physics major

**Motivation:**
- Taking computational physics course that uses HPC
- First time using a cluster
- Professor said "use VS Code to connect"
- Wants accessible, user-friendly introduction

**Experience:**
- Comfortable with Python from coursework
- Used VS Code in CS electives
- Never SSH'd into anything
- Gets overwhelmed by Linux complexity

**Pain Point:**
"Terminal stuff intimidates me. I want a GUI. How do I even start?"

**Expected Outcome After Workshop:**
- Successfully connect VS Code to Sagehen
- Understand basics of remote development concept
- Edit Python files for class assignments
- Understand storage paths and file organization
- Know where to get help for further HPC learning
- Confidence that they're not "doing it wrong"

**Preference:** Needs clear step-by-step guidance, appreciates analogies to local VS Code

---

## Common Learner Characteristics

### What They Know
- VS Code (at least basics) or similar IDE
- Basic command-line operations (ls, cd, cat)
- How to manage files on their computer
- How to run code or scripts they write

### What They Don't Know
- How SSH remote access works conceptually
- Difference between "local" and "remote" files
- SLURM job submission (most will learn this separately)
- Module system and loading software
- How to navigate Sagehen's file structure

### What They Value
- **Familiarity** - Want to use tools they already know
- **Visual Feedback** - GUI > command line for new users
- **Speed** - Want to solve research problems, not learn systems
- **Reliability** - Connection must work consistently
- **Documentation** - Clear instructions, not assumptions

### What They Fear
- **"I'll break something"** - "Is the cluster fragile?"
- **"It's too hard"** - "Will I understand this?"
- **"I'll lose my data"** - "Where do files actually live?"
- **"SSH is complicated"** - "Command-line stuff is scary"
- **"It won't work"** - "What if I can't connect?"

---

## Learner Diversity

### By Research Field
- **Data Science** - Jupyter users, large datasets
- **Statistics** - RStudio users, collaborative analysis
- **Computer Science** - Familiar with VS Code, want to learn systems
- **Physics** - Computational simulations, need performance
- **Biology** - Pipeline development, data processing

### By Career Stage
- **Undergraduate** - First time, needs support and reassurance
- **Graduate Student** - Scaling up from laptop, knowledge gaps
- **Postdoc** - Experienced coder, wants better tools
- **Faculty** - Teaching students, needs to understand system

### By Technical Comfort
- **Very Comfortable** - May know more than instructor (Dr. Chen)
- **Moderately Comfortable** - Can troubleshoot (Sam, Alex)
- **Less Comfortable** - Needs clear steps, encouragement (Jordan)
- **Transitioning** - Expert in one tool (Dr. Gonzalez)

### By Programming Language
- **Python** - Most common (Sam, Alex, Jordan)
- **R** - Statistical focus (Dr. Gonzalez)
- **C/C++** - Performance computing (Dr. Chen)
- **MATLAB** - Some backgrounds

---

## Design Philosophy

This workshop bridges the gap between **"I know VS Code locally"** and **"I want to use it on HPC."**

Key assumptions:
- Participants have some IDE experience (usually VS Code)
- Participants may not know SSH or Linux well
- Participants have real HPC work to do (not just learning)
- Participants want minimal setup time before working

The workshop emphasizes:
- **"How do I set this up?"** - Clear setup instructions, troubleshooting
- **"What's different from local?"** - Highlight conceptual differences
- **"Can I do my actual work?"** - Real examples, not toy projects
- **"What if it breaks?"** - Reassurance and support

By end of day, participants should have:
1. Successfully connected VS Code to Sagehen
2. Opened a real project and made edits
3. Run code in the integrated terminal
4. Confidence to continue learning independently

---

## Accessibility Considerations

Workshop should accommodate:
- **Visual** - Large text in screenshots, clear colors
- **Auditory** - Written transcript of demos, captions if recording
- **Motor** - Keyboard shortcuts alternatives, no fast-paced typing
- **Cognitive** - Clear language, step-by-step process, breaks
- **Technical** - Good WiFi, contingency plans if Sagehen down

Provide materials in multiple formats:
- Printed reference cards
- Online documentation
- Video walkthrough (optional)
- Accessible code examples with comments

