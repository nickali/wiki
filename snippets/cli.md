---
description: Notes specific to the terminal.
---

# CLI

## Utilities

### Disk-related

Finding top-level largest directories:

```bash
du -h / --max-depth=1 | sort -hr
```

## Environments

### Conda

Set up environments \(example for node\):

```bash
$ conda create -yn myapp nodejs
$ conda activate myapp
$ node --version
v8.11.3
$ npm --version
5.6.0
```

## Keyboard Shortcuts

### Mac

From the [Apple Support page](https://support.apple.com/guide/terminal/keyboard-shortcuts-trmlshtcts/mac):

| Action | Shortcut |
| :--- | :--- |
| Move the insertion point to the beginning of the line | Control-A |
| Move the insertion point to the end of the line | Control-E |
| Move the insertion point forward one word | Option-Right Arrow |
| Move the insertion point forward one word | Option-w |
| Move the insertion point backward one word | Option-Left Arrow |
| Move the insertion point backward one word | Option-b |
| Delete to the beginning of the line | Control-U |
| Delete to the end of the line | Control-K |
| Copy plain text | Option-Shift-Command-C |
| Paste | Command-V |
| Paste the selection | Shift-Command-V |
| Paste escaped text | Control-Command-V |
| Paste escaped selection | Control-Shift-Command-V |

[And more](https://github.com/you-dont-need/You-Dont-Need-GUI/blob/master/readme.md):

Peek in a zip file:
```shell
$ unzip -l archive_name.zip
```

Display calendar:
```shell
$ cal
```


Display specific month and year calendar
```shell
$ cal 11 2018
```

Display future date
```shell
date -d "+7 days"
```

Calculator:
```shell
$ bc
```
Current DNS servers being used:
```
scutil --dns | grep 'nameserver\[[0-9]*\]'
```

Random
```
$ !! # run last command
$ sudo !! # run last command as root
$ !<word> # run last command starting with <word>
$ !<word>:P # show last command starting with <word> but don't run
```

