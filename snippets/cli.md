---
description: Notes specific to the terminal.
---

# CLI

### Utilities

#### Disk-related

Finding top-level largest directories:

```text
du -h / --max-depth=1 | sort -hr
```

### Dev

#### Conda

Set up environments \(example for node\):

```text
$ conda create -yn myapp nodejs
$ conda activate myapp
$ node --version
v8.11.3
$ npm --version
5.6.0
```

### Keyboard Shortcuts 

#### Mac

From the [Apple Support page](https://support.apple.com/guide/terminal/keyboard-shortcuts-trmlshtcts/mac):

| Action | Shortcut |
| :--- | :--- |
| Move the insertion point to the beginning of the line | Control-A |
| Move the insertion point to the end of the line | Control-E |
| Move the insertion point forward one word | Option-Right Arrow |
| Move the insertion point backward one word | Option-Left Arrow |
| Delete to the beginning of the line | Control-U |
| Delete to the end of the line | Control-K |
| Copy plain text | Option-Shift-Command-C |
| Paste | Command-V |
| Paste the selection | Shift-Command-V |
| Paste escaped text | Control-Command-V |
| Paste escaped selection | Control-Shift-Command-V |

