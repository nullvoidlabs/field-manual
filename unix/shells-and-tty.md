# unix/shells-and-tty.md

## Spawn an interactive PTY (bash)
    python3 -c 'import pty; pty.spawn("/bin/bash")'

## Fix TERM for interactive tools
    export TERM=xterm

## Set TTY size (match your local terminal)
    stty rows 40 columns 120

## Stabilize a shell with job control (common upgrade flow)
1) Background the shell:
    Ctrl+Z

2) On your local terminal, set raw mode and foreground:
    stty raw -echo; fg
