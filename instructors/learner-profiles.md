---
title: 'Learner Profiles'
---

## Typical Workshop Participants

Understanding who takes this workshop helps instructors tailor the experience.

### Profile 1: Novice Researcher (Most Common - 40%)

**Background:**
- New to Pomona HPC or first-time HPC user
- Primarily uses VS Code locally, unaware of Remote-SSH
- May have used nano or never edited remote files
- Excited but intimidated by command line

**Experience Level:**
- Comfortable with basic terminal navigation (pwd, cd, ls)
- May not fully understand SSH yet
- Unfamiliar with SLURM
- May not have DUO set up

**Learning Goals:**
- Learn a better way to edit remote files
- Get productive quickly on Sagehen HPC
- Feel confident submitting jobs

**Common Challenges:**
- Getting SSH configured correctly
- Understanding DUO authentication
- Conceptualizing local vs. remote
- File paths and directory structure

**Teaching Approach:**
- Start from basics (what is SSH, what is SLURM)
- Show VS Code solving concrete problems (no more nano!)
- Celebrate small wins
- Have extra help with Episode 2 ready

**Success Indicator:**
- Completes first connection successfully
- Edits a file and runs `sbatch`
- Understands that extensions run on cluster

### Profile 2: Experienced HPC User (25%)

**Background:**
- Already comfortable with SLURM and terminal
- Uses vim or nano successfully
- Curious about whether VS Code would be faster
- Possibly uses MobaXterm or other tools

**Experience Level:**
- Very comfortable with SSH and terminal
- Understands cluster file structure well
- Familiar with SLURM concepts
- May have already optimized their workflow

**Learning Goals:**
- Evaluate if VS Code improves their productivity
- Learn new features (intellisense, debugging)
- Possibly replace their current editor

**Common Challenges:**
- Skeptical that GUI is better than vim
- May prefer keyboard-only workflows
- Wondering if it's worth changing habits

**Teaching Approach:**
- Show productivity gains (quick open, find/replace across files)
- Don't criticize vim/nano; acknowledge they're valid
- Focus on what VS Code uniquely offers
- Let them move faster through Ep 1-2

**Success Indicator:**
- Experiments with Python extension
- Uses split editor
- Integrates it into their workflow or consciously decides against it

### Profile 3: Collaborating Student (20%)

**Background:**
- Works in a lab or research group
- May share code with lab mates
- Wants tools that help collaboration
- Possibly using shared project folders

**Experience Level:**
- Moderate terminal skills
- May not be familiar with Git
- Learning how to do "research computing"
- Adapting to lab's existing practices

**Learning Goals:**
- Use tool that lab mates also use
- Manage shared projects better
- Possibly integrate with Git workflows

**Common Challenges:**
- Comparing with what lab mates use
- Understanding file permissions and sharing
- Git integration (not covered but relevant)
- Coordinating with others

**Teaching Approach:**
- Show how VS Code helps manage shared projects
- Mention GitLens for code review
- Discuss workspace settings (can be committed with code)
- Talk about how to help lab mates onboard

**Success Indicator:**
- Understands project structure in VS Code
- Can open shared projects
- Comfortable enough to help lab mate

### Profile 4: Developer Coming to HPC (10%)

**Background:**
- Professional or serious programmer
- VS Code expert, uses it daily locally
- New to HPC (first time using Sagehen)
- Wants to develop on cluster but maintain local workflow

**Experience Level:**
- Very comfortable with VS Code already
- May not understand SLURM at all
- Strong terminal skills but different from HPC
- Clear about what they want to do

**Learning Goals:**
- Quickly get Remote-SSH working
- Understand SLURM for job submission
- Integrate HPC into their development workflow
- Possibly use extensions they already use

**Common Challenges:**
- SLURM is very different from their normal environment
- Module system unfamiliar
- Cluster resource constraints (memory, time limits)
- Translating their local dev practices to HPC

**Teaching Approach:**
- Move quickly through VS Code parts (they know it)
- Spend more time on SLURM and cluster paradigm
- Show how to adapt their workflow to batch jobs
- Be prepared for advanced questions

**Success Indicator:**
- Successfully submits batch job
- Understands why interactive development must adapt
- Plans to integrate VS Code into their project

## Common Misconceptions by Profile

### Misconception 1: "VS Code will be slow over SSH"
**Who thinks this:** Experienced HPC users, Developers
**Reality:** VS Code runs UI locally, only files are remote; very responsive
**Teaching approach:** Show live editing, emphasize local UI

### Misconception 2: "I have to use the mouse a lot in VS Code"
**Who thinks this:** vim users, keyboard enthusiasts
**Reality:** VS Code is very keyboard-centric (Ctrl+P, Ctrl+H, etc.)
**Teaching approach:** Emphasize shortcuts, show terminal integration

### Misconception 3: "DUO is complicated"
**Who thinks this:** Beginners unfamiliar with MFA
**Reality:** Simple once set up; just enter code or approve on phone
**Teaching approach:** Walk through DUO step carefully, explain MFA concept

### Misconception 4: "Remote extensions are complicated to install"
**Who thinks this:** Beginners
**Reality:** Click install button, choose "remote"; VS Code does the rest
**Teaching approach:** Show it's the same process as local extensions

### Misconception 5: "I need to understand all features to use VS Code"
**Who thinks this:** Perfectionists, Developers
**Reality:** Learn as you go; start with editing, add extensions later
**Teaching approach:** Frame workshop as "introduction"; deep dives later

## Accessibility Considerations

### Vision
- Recommend 13pt minimum font size
- Ensure color themes have adequate contrast
- Describe visual elements in text (don't just say "click the blue button")
- Provide materials in text and PDF format

### Motor/Dexterity
- Keyboard shortcuts can reduce mouse usage
- Show multiple ways to do things (menu and keyboard)
- Allow breaks without penalty
- Remind people to take breaks during long session

### Neurodiverse
- Some learners may need more time for concepts to sink in
- Being explicit about expectations (what will happen next)
- Respecting different learning paces
- Accepting questions even if repeated

### Language
- Non-native English speakers may need extra time
- Provide glossary of technical terms
- Speak clearly, avoid idioms
- Written materials are helpful reference

## How to Adapt for Different Groups

### For Mostly Beginners
- Spend extra time on Episode 1 (why this matters)
- Go slowly through Episode 2 (take no shortcuts)
- Have lots of help ready for Episode 3 (connection)
- Practice patience and celebration of wins

### For Mostly Advanced Users
- Speed through Ep 1-2
- Focus on Ep 5-6 (terminal and extensions)
- Have advanced topics ready (debugging, Live Share, etc.)
- Encourage them to become peers and help others

### For Mixed Group (Most Likely)
- Pair beginners with advanced users as "buddy helpers"
- Let advanced users move at own pace, check in with beginners
- Have optional advanced content for fast learners
- Be clear which parts are essential vs. optional

### For Very Small Group (< 5 people)
- More interactive, conversational
- Can customize to individual interests
- Have 1-on-1 follow-up time
- Spend time on specific use cases

### For Large Group (> 30 people)
- Have multiple instructors/helpers
- Pre-screen learners to understand experience levels
- Have explicit seating for "beginners" and "advanced"
- Prepare for longer Q&A sections
- Have practice problems people can do independently

## Scenario-Based Teaching

Consider showing these realistic scenarios:

### Scenario 1: Novice Researcher
"I just got access to Sagehen and need to run some Python scripts. I want to edit files without learning vim. How do VS Code?"

### Scenario 2: Lab Collaboration
"My advisor uses VS Code and our lab shares a project folder. I want to be able to edit the same files."

### Scenario 3: Publishing Results
"I need to run an analysis that takes 48 hours. I want to see the progress while continuing other work on my laptop."

### Scenario 4: Debugging
"My script has a bug I can't find. I want to use VS Code's debugging tools to trace through the code on Sagehen."

These scenarios make the workshop feel relevant to participants' actual work.

## Creating an Inclusive Learning Environment

### Do:
- Use inclusive language ("folks" instead of "guys")
- Welcome questions at any level
- Acknowledge different backgrounds
- Celebrate mistakes as learning opportunities
- Provide materials in multiple formats
- Take breaks when needed
- Ask "any questions?" and wait longer than feels comfortable

### Don't:
- Assume prior knowledge
- Make fun of struggles
- Use jargon without explanation
- Make learners feel rushed
- Judge people's current skill level
- Assume everyone has same resources (not everyone has GitHub, etc.)

## Measuring Success by Profile

| Profile | Success Looks Like |
|---------|-------------------|
| Novice | Connects to cluster, edits file, submits job |
| Experienced | Evaluates tool, may adopt for some workflows |
| Student | Understands how to use tool in lab context |
| Developer | Integrates VS Code with HPC development |

## Ongoing Support

Beyond the workshop, different profiles need different support:

### Novice → Follow-up
- Check in after 1 week (did they use it?)
- Office hours for troubleshooting
- Pair with experienced user for first real project

### Experienced → Follow-up
- Advanced workshop on debugging/extensions
- Peer-to-peer learning with lab mate
- Documentation of best practices

### Student → Follow-up
- Integration with lab on-boarding
- Shared workspace settings for lab
- Git integration workshop

### Developer → Follow-up
- Advanced topics (remote debugging, live share)
- Integration with their development processes
- Feedback for improving VS Code + HPC integration

Remember: Each person brings value. Beginners ask good questions that help refine teaching. Experienced users help others and keep things moving. Everyone deserves respect and support.
