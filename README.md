# Hijackey

Hijackey stands for hijacked keys.

Standard terminals are missing a lot of key combinations (eg Shift Enter).
Hijackey uses custom escape sequences to emulate the extra keys.

This requires the terminal to be configured to the escape sequences.

Currently only iTerm2 (osx) and Konsole (linux) are capable of sending custom
escape sequences.

This repo contains the configurations for iTerm2, Konsole, bash, emacs, and vim.

Xterm escape sequences are explained in
See http://invisible-island.net/xterm/ctlseqs/ctlseqs.html

The hijacked escape sequences uses the `CSI ~ encoding` (normally for function keys with modifiers). Hijackeys uses the following format:

```
CSI 72 ; decimal_ascii_code ; modifier ~
```
```
   Code     Modifiers
---------+---------------------------
   2     | Shift
   3     | Alt
   4     | Shift + Alt
   5     | Control
   6     | Shift + Control
   7     | Alt + Control
   8     | Shift + Alt + Control
```

eg.
Shift TAB is `CSI 72 ; 9 ; 2 ~`
Control Shift A is `CSI 72 ; 97 ; 6 ~`

`CSI 72` is used because 72 appears to be unused in
http://invisible-island.net/xterm/terminfo.html
and it is also ACII for H (for Hijackey).

# Non printables

```
ESC : escape
RET : return
BSC : backspace
DEL : delete
SPC : spacebar
```
These will all be hijacked to have all the modifier combinations unless noted below.

# Numbers

Numbers will be hijacked to have a C-number, C-M-number, but not C-S-number or C-S-M-number.
NB. M-number combination preexists as ESC-number.

# Non hijacked keys
## Standard
Keys with standard representations do not use hijacked code, but the standard codes. Hijackey configs will make sure iTerm is not missing any of these standard bindings.

Some of these are:
```
S-TAB : \E[Z    # In default Konsole (linux)
S-RET : \EOM    # In default Konsole (linux)
A-RET : \Ex0a   # In default linux
M-BSC : \E\x7f  # This is \E^? which is backward delete word in bash.
S-SPC : \x00    # In default linux
```

## Alt & Alt Shift
By default, xterm already has M-printable and M-S-printable.
M-printable is just ESC-printable and M-S-printable is actually just ESC-shifted_printable.

## Control
By default, xterm already has C-alphas and the following:
```
C-_
C-[ # This is ESC
C-]
C-\
C-^
C-@ # This is null \x00
```
#  iTerm2

You'll have to use the iTerm "Bulk copy from selected profile" to copy
the keys copy the Hijackey keys into another profile, then
delete the conflicting hijackey keys for your iTerm app shortcuts to work.
Konsole doesn't have this problem.

# Equivalent keys
```
M-[ : ESC [ , ie. CSI
C-m : RET
C-i : TAB
```