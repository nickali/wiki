# Tmux

If none of keys combos work for you, it's because I've changed them from the defaults. [Check out my .tmux.conf](https://github.com/nickali/configs/blob/master/tmux/tmux.conf).

The prefix used is _**Ctrl-a**_.

### Session Management

New session:

```text
Ctrl-a Ctrl-c
```

Rename session:

```text
Ctrl-a $
```

Previous session:

```text
Ctrl-a (
```

Next session:

```text
Ctrl-a )
```

List sessions:

```text
Ctrl-a s
```

Kill session from inside tmux:

```text
Ctrl-a x
```

Kill session from shell prompt:

```text
$ tmux ls # will list out sessions with numbers
$ tmux kill-session -t <number>
```

### Windows

New window:

```text
Ctrl-a c
```

Rename window:

```text
Ctrl-a ,
```

Next window:

```text
Ctrl-a Ctrl-l
```

Previous window:

```text
Ctrl-a Ctrl-h
```

List windows:

```text
Ctrl-a :list-windows
```

Switch windows by number:

```text
Ctrl-a 0..9
```

Kill current window:

```text
Ctrl-a &
```

### Panes

Split horizontally:

```text
Ctrl-a -
```

Split vertically:

```text
Ctrl-a _
```

Pane navigation:

```text
Ctrl-a h    # move left
Ctrl-a j    # move down
Ctrl-a k    # move up
Ctrl-a l    # move right
```



