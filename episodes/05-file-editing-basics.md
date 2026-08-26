---
title: "File Editing Basics"
teaching: 10
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions

- How do I create and edit files on the remote cluster?
- What are VS Code's core editing features?

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Create, open, edit, and save files on Sagehen HPC
- Use syntax highlighting and code completion
- Navigate files with Quick Open and Go to Line
- Upload files from your local computer via drag-and-drop

::::::::::::::::::::::::::::::::::::::::::::::

## The Remote File Browser

The Explorer sidebar displays your remote file system. Click arrows to expand
folders. Hover over a file to see its full path and size.

## Creating Files

**Explorer sidebar:** Right-click > **New File**, type the filename
(including extension like `script.py`), press Enter.

**Keyboard:** Ctrl+Alt+N (Windows/Linux) or Cmd+Shift+N (Mac).

**File menu:** File > New File, then save with Ctrl+S and choose location.

## Opening Files

- **Single-click** a file in Explorer to preview it (shown in italics)
- **Double-click** to open for editing

::::::::::::::::::::::::::::::::::::: callout

## Pro Tip: Use Quick Open for Speed

Press **Ctrl+P** (or Cmd+P on Mac), start typing the filename, and VS Code
shows matching files. This is the fastest way to navigate large projects.

Use **Ctrl+G** to jump to a specific line number.

::::::::::::::::::::::::::::::::::::::::::::::

## Editing Features

- **Syntax highlighting**: VS Code detects file type and colors code accordingly
  (Python, R, Markdown, C/C++, and many more)
- **Code completion (IntelliSense)**: Suggestions appear as you type. Press
  Ctrl+Space to trigger manually.
- **Line numbers**: Click a line number to select the entire line

## Saving Files

| Action | Windows/Linux | Mac |
|--------|---------------|-----|
| Save | Ctrl+S | Cmd+S |
| Save All | Ctrl+Shift+S | Cmd+Shift+S |
| Auto Save | File > Auto Save | File > Auto Save |

Files save to Sagehen, not your local machine.

## Uploading Files from Your Computer

::::::::::::::::::::::::::::::::::::: callout

## Drag-and-Drop Upload

Drag files from your local file explorer (Windows Explorer, Finder) into the
VS Code Explorer sidebar. They upload directly to Sagehen in the currently
open folder. Multiple files can be dragged at once.

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: challenge

## Challenge: Create and Edit a Python File

1. Create a new file called `hello_world.py`
2. Type this code:

   ```python
   #!/usr/bin/env python3
   """My first Python script on Sagehen."""

   name = input("What's your name? ")
   print(f"Hello, {name}!")
   ```

3. Save with Ctrl+S
4. Verify syntax highlighting colors the code

::::::::::::::::::::::::::::::::::::: solution

## Solution

The file tab shows `hello_world.py` without a dot (indicating saved). Python
syntax highlighting colors `#!/usr/bin/env python3` in one color, the docstring
in another, and `print` as a built-in keyword. Verify the file exists on
Sagehen by opening the terminal (Ctrl+\`) and running `ls -l hello_world.py`.

If there is no syntax highlighting, the Python extension may not be installed
yet (covered in the Extensions episode).

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: keypoints

- Use the Explorer sidebar or Quick Open (Ctrl+P) to navigate remote files
- Create files with right-click > New File or keyboard shortcuts
- VS Code provides syntax highlighting and IntelliSense automatically
- Save with Ctrl+S; files save to Sagehen, not your local machine
- Drag files from your computer into the Explorer sidebar to upload them

::::::::::::::::::::::::::::::::::::::::::::::
