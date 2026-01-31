# qol/misc-tricks.md

## Windows 11 install without Microsoft account (OOBE)
⚠️ Review: This relies on Windows setup behavior and may change across builds.
- When prompted to sign in with a Microsoft account:
  1) Press `Shift + F10` to open Command Prompt
  2) Run:
        ipconfig /release
  3) Continue setup (disconnecting network allows local install flow)

## Vim quick actions (high-signal)
Reference: https://vim.rtorr.com/

### Help / panes / terminal
    :h[elp] keyword
    :sav[eas] file
    :clo[se]
    :ter[minal]
    K

### Splits + tabs
    Ctrl-w h
    Ctrl-w l
    Ctrl-w j
    Ctrl-w k
    :tabnew filename
    gt
    gT

### Misc
    .
    Ctrl-g
    :%!command
    :set number
    :set nonumber
    :syntax on
    :syntax off

### Practice
    vimtutor
