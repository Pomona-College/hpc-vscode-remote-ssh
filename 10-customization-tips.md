---
title: "Customization and Tips"
teaching: 10
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions

- How do I customize VS Code's appearance and keyboard shortcuts?
- What workspace settings help HPC development?
- How do I sync settings across machines?

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Customize color themes, icons, and keyboard shortcuts
- Create workspace settings for HPC projects
- Use Settings Sync to keep configurations consistent
- Apply recommended settings for productive HPC work

::::::::::::::::::::::::::::::::::::::::::::::

## Color Themes

1. Press **Ctrl+K Ctrl+T** (or File > Preferences > Color Theme)
2. Preview themes by arrowing through the list
3. Press Enter to select

Popular themes for long coding sessions: **Dark Modern** (default), **Dracula**,
**Nord**, **One Dark Pro**.

Install additional themes from the Extensions marketplace by searching "theme."

## File Icon Themes

File > Preferences > File Icon Theme. Icons help identify file types at a glance
in the Explorer sidebar.

## Keyboard Shortcuts

View and customize shortcuts at **Ctrl+K Ctrl+S** (or File > Preferences >
Keyboard Shortcuts).

To change a shortcut:

1. Search for the command
2. Click the pencil icon
3. Press your desired key combination
4. VS Code saves it immediately

## Workspace Settings

Create project-specific settings that override global defaults:

1. In your project folder, create `.vscode/settings.json`
2. Add settings:

```json
{
    "editor.formatOnSave": true,
    "editor.autoSave": "afterDelay",
    "editor.autoSaveDelay": 2000,
    "files.trimTrailingWhitespace": true,
    "files.insertFinalNewline": true,
    "[python]": {
        "editor.defaultFormatter": "ms-python.python",
        "editor.formatOnSave": true
    },
    "terminal.integrated.scrollback": 5000
}
```

These settings apply only in this workspace and can be version-controlled with
your project.

## Settings Sync

Sync your VS Code configuration across multiple computers:

1. Click the account icon in the bottom-left
2. Sign in with Microsoft or GitHub account
3. VS Code syncs extensions, settings, keybindings, and themes

## Recommended Settings for HPC

::::::::::::::::::::::::::::::::::::: callout

## Optimized Configuration for HPC Development

```json
{
    "editor.fontSize": 13,
    "editor.formatOnSave": true,
    "files.trimTrailingWhitespace": true,
    "files.insertFinalNewline": true,
    "terminal.integrated.fontSize": 12,
    "terminal.integrated.scrollback": 5000,
    "remote.SSH.showLoginTerminal": true
}
```

::::::::::::::::::::::::::::::::::::::::::::::

## Productivity Tips

1. **Keep the terminal visible**: Resize editor so the terminal always shows
2. **Use descriptive job names**: `#SBATCH --job-name=analysis_v2`
3. **Redirect output**: `2>&1 | tee output.log` saves and displays output
4. **Check resources**: Run `sinfo` to see available nodes and partitions
5. **Use file watchers carefully**: Large remote directories can slow VS Code;
   exclude `node_modules`, `.git`, and large data directories in settings

## Additional Extensions Worth Exploring

- **Better Comments**: Highlight TODO, HACK, BUG comments in code
- **Bracket Pair Colorizer**: Color-code nested brackets
- **Path Intellisense**: Auto-complete file paths
- **Live Share**: Collaborative real-time coding

::::::::::::::::::::::::::::::::::::: challenge

## Challenge: Personalize Your VS Code

1. Open Command Palette (Ctrl+Shift+P) and type "Color Theme"
2. Try three themes and pick your favorite
3. Open Keyboard Shortcuts (Ctrl+K Ctrl+S)
4. Search "Go to Line" and note (or customize) its shortcut
5. Create `.vscode/settings.json` in your project folder with at least
   `formatOnSave` and `trimTrailingWhitespace` enabled

::::::::::::::::::::::::::::::::::::: solution

## Solution

After selecting a theme via Ctrl+Shift+P > "Color Theme," the change takes
effect immediately. "Go to Line" defaults to Ctrl+G. Creating
`.vscode/settings.json` with `"editor.formatOnSave": true` means your code
auto-formats on every save. Changes take effect immediately without restart.

If Settings Sync is enabled, these preferences carry to other machines
automatically.

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Customize themes with Ctrl+K Ctrl+T; customize shortcuts with Ctrl+K Ctrl+S
- Workspace settings in `.vscode/settings.json` apply per-project and can be
  version-controlled
- Settings Sync keeps your VS Code identical across multiple machines
- Recommended HPC settings include format-on-save, trailing whitespace trimming,
  and increased terminal scrollback

::::::::::::::::::::::::::::::::::::::::::::::
