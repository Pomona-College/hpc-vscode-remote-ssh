---
title: 'VS Code Remote-SSH for HPC'
---

## About This Workshop

This is a complete Carpentries Workbench workshop on using Microsoft VS Code with the Remote-SSH extension to develop code on the Pomona College Sagehen HPC cluster.

**Workshop 19** in Pomona College's HPC training series.

- **Target Audience:** Pomona College researchers and students using Sagehen cluster
- **Level:** Beginner to intermediate
- **Duration:** ~3 hours (including breaks and hands-on challenges)
- **Format:** In-person workshop with live demonstrations and hands-on challenges

## Learning Outcomes

After completing this workshop, you will be able to:

- Install VS Code and the Remote-SSH extension
- Configure SSH to connect securely to Sagehen cluster
- Edit remote files using VS Code's full IDE features
- Use VS Code's integrated terminal for SLURM job submission and monitoring
- Install and configure extensions for Python, R, and Jupyter development
- Customize VS Code for your HPC workflow

## Workshop Structure

### 6 Episodes

1. **Why VS Code Remote-SSH** (20 min) - Understand why VS Code is recommended for HPC work and how it compares to alternatives
2. **Installation and Setup** (30 min) - Install VS Code and configure SSH for Sagehen connection
3. **Connecting to Sagehen** (40 min) - Make your first connection and authenticate with DUO
4. **Remote File Editing** (30 min) - Edit, create, and manage files on Sagehen
5. **Integrated Terminal and SLURM** (35 min) - Use the terminal to submit and monitor jobs
6. **Extensions and Customization** (35 min) - Enhance VS Code with extensions and personalize your environment

### Supporting Materials

- **setup.md** - Pre-workshop setup for learners and instructors
- **reference.md** - Quick reference for commands, shortcuts, and troubleshooting
- **instructors/instructor-notes.md** - Detailed guide for teaching the workshop
- **instructors/learner-profiles.md** - Understanding your audience and their needs

## Quick Start for Learners

1. **Before the workshop:** Complete the checklist in [setup.md](setup.md)
2. **During the workshop:** Follow along with each episode, complete challenges
3. **After the workshop:** Refer to [reference.md](reference.md) for commands and troubleshooting

## Quick Start for Instructors

1. **Prepare:** Read [setup.md](setup.md) for classroom setup
2. **Understand your audience:** See [instructors/learner-profiles.md](instructors/learner-profiles.md)
3. **Teach:** Follow [instructors/instructor-notes.md](instructors/instructor-notes.md) for guidance
4. **Reference:** Use [reference.md](reference.md) for accurate commands and settings

## Key Features

### What You'll Learn

- **Modern IDE for Remote Work**: Use VS Code's full feature set (intellisense, debugging, file browser) while working on Sagehen
- **Integrated Workflow**: Edit code, monitor jobs, and access the file system all in one window
- **SLURM Integration**: Submit batch jobs and monitor progress without leaving the editor
- **Extensibility**: Add support for Python, R, Jupyter, Git, and more
- **Cross-Platform**: Works on Windows, Mac, and Linux

### What Makes This Workshop Special

- **Hands-on**: Every concept has a practical challenge you complete
- **Pomona-specific**: Examples, contact info, and cluster details for Sagehen
- **Comprehensive**: Covers installation, configuration, usage, and troubleshooting
- **Instructor-friendly**: Detailed notes, timing guides, and troubleshooting strategies
- **Accessible**: No assumptions about prior VS Code or HPC experience

## Requirements

### For Learners

- **Computer**: Windows, Mac, or Linux laptop
- **Account**: Active Pomona College HPC account on Sagehen
- **Credentials**: Pomona username and password
- **Authentication**: DUO MFA registered and working
- **Software**: VS Code (will install during workshop)

### For Instructors

- **All of the above**, plus
- **Testing**: Verify Sagehen access and DUO works before workshop
- **Materials**: Print or share digital copies of reference materials
- **Support**: Have contact info for its-hpc@pomona.edu ready

## Customizing for Your Institution

This workshop is designed for Pomona College Sagehen cluster but can be adapted:

1. Replace "sagehen.hpc.pomona.edu" with your cluster hostname
2. Replace DUO references with your MFA system
3. Update paths like "/rhome/" to your home directory structure
4. Replace contact email "its-hpc@pomona.edu" with your support contact
5. Update SLURM examples to match your cluster's partitions and resources
6. Add your institution's specific examples and policies

See [setup.md](setup.md) for customization instructions.

## Technical Details

- **Carpentries Workbench Format**: Uses standard Carpentries structure for episodes, challenges, and assessment
- **License**: CC-BY 4.0
- **Source**: https://github.com/Pomona-College/hpc-vscode-remote-ssh
- **Life Cycle**: Pre-alpha (actively developed, feedback welcome)
- **Cluster**: Sagehen HPC at Pomona College
- **Contact**: its-hpc@pomona.edu

## Files and Folders

```
vscode-remote-ssh/
├── config.yaml              # Workbench configuration
├── index.md                 # Welcome page
├── setup.md                 # Setup instructions
├── reference.md             # Quick reference guide
├── README.md               # This file
├── episodes/
│   ├── 01-why-vscode-remote.md
│   ├── 02-installation-setup.md
│   ├── 03-connecting.md
│   ├── 04-file-editing.md
│   ├── 05-integrated-terminal.md
│   └── 06-extensions-customization.md
└── instructors/
    ├── instructor-notes.md
    └── learner-profiles.md
```

## Getting Help

### For Learners

- **During workshop**: Ask the instructor!
- **After workshop**: Email its-hpc@pomona.edu
- **Slack**: #hpc-help channel (if available)
- **Documentation**: See [reference.md](reference.md) for troubleshooting

### For Instructors

- **Preparation**: Review instructor-notes.md thoroughly
- **Troubleshooting**: See troubleshooting section in reference.md
- **Issues**: Document problems to improve the workshop
- **Feedback**: Collect learner feedback to iterate

## Contributing

Found an issue? Have a suggestion? Contact its-hpc@pomona.edu with:

- What you found (typo, wrong command, unclear explanation)
- Where it is (which episode, which section)
- Your suggestion for improvement
- Your experience level (helps us understand the audience)

## Version History

### Version 1.0 (2026-03-05)
- Initial release
- 6 episodes covering VS Code Remote-SSH basics
- Instructor materials and learner profiles
- Pomona College Sagehen specific content

## Acknowledgments

**Andrew Wilson** — Director of Research Computing and Digital Scholarship,
Pomona College. Workshop design and development.

**Andrei Motchenko** — testing, editing, cleanup and screenshots across the
Pomona College HPC Workshop Series.

This workshop was developed for Pomona College's HPC training program by the ITS-HPC team.

Special thanks to:
- All the learners who provided feedback and questions
- The Carpentries community for the workshop framework

## License

This work is licensed under Creative Commons Attribution 4.0 International (CC-BY 4.0).

You are free to:
- Share and adapt this material
- Use for your own institution
- Modify for your cluster

With the requirement to:
- Give appropriate credit
- Link to the license
- Indicate changes made

## Additional Resources

### Official Documentation
- [VS Code Documentation](https://code.visualstudio.com/docs)
- [Remote-SSH Extension](https://code.visualstudio.com/docs/remote/ssh)
- [SLURM Documentation](https://slurm.schedmd.com/)

### Learning Resources
- [Python for Beginners](https://www.python.org/about/gettingstarted/)
- [R for Data Science](https://r4ds.had.co.nz/)
- [Git Basics](https://git-scm.com/book/en/v2)

### Pomona College Resources
- [Sagehen HPC Documentation](https://pomona-college.github.io/)
- [ITS Help Desk](https://www.pomona.edu/its)
- [HPC Support](https://pomona.edu/hpc)

---

**Questions?** Contact its-hpc@pomona.edu or open an issue on GitHub.

**Ready to get started?** Begin with [setup.md](setup.md) if you're new, or jump to [Episode 1](episodes/01-why-remote.md) if you're attending the workshop!
