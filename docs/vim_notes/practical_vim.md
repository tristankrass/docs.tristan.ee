# Vim 


## Essential vim

`essential.vim`
 set nocompatible
 filetype plugin on


 Launching the vim
 `vim -u code/essential.vim`

## Notations

Notation | Meaning |
--- | --- |
`<C-n>` | While holding <Ctrl> press n |
`g<C-]>` | Press g, then while holding <Ctrl> press ] |
`<C-r>0` | While holding <Ctrl> press r, then release <Ctrl> and press 0 |
`<C-w><C-=>` | While holding <Ctrl> press w then = |




## Commands

| Command | Description |
--- | --- |
`*` | searches for the word under cursor | 
`.` | Repeat the last action | 
`>>` | Indents line |
`s` | delete single character |


## Compound commands

| Compound Command | Eqiovalent Longhand |
--- | --- |
`C` | `c$` |
`s` | `cl` |
`S` | `ˆs` |
`A` | `$a` |
`o` | `A<CR>`|
`O` | `ko` |

NB! They all switch from *normal* mode to *insert* mode.

## Repeatable actions and how to Reverse them

| Intent | Act | Repeat | Reverse | 
--- | --- | --- | --- | 
Make a change | {edit} | `.` | `u` |
Scan line for next character | f{char}/t{char} | `;` | `,` |
Scan line for previous character | F{char}/T{char} | `;` | `,` |
Scan document for next match  | `/pattern<CR>` | `n` | `N` |
Scan document for previous match  | `?pattern<CR>` | `n` | `N` |
Perform substitution | :s/target/replacement | `&` | `u` |
Execute a sequence of changes | `qx{changes}q` | `@x` | `u` |


## Vim oprators commands

| Trigger| Effect | 
--- | --- |
`c` | Change |
`d` | Delete |
`y` | Yank register |
`g~` | Swap case |
`gu` | Make lowercase |
`gU` | Make Uppercase |
`>` | Shift right |
`<` | Shift left |
`=` | Autoindent |
`!` | Filter{motion lines through an external program}|
`<C-h>` | Delete back on character (backspace) |
`<C-w>` | Delete back one word |
`<C-u>` | Delete back to start of line |
`K` | Look up the man pages under the cursor |
`J` | Join the current and the next lines togehter |
`r` | Replace the word under cursor | 
`R` | Go to replace mode | 


## Inserting unusuual Characters

| Keystrokes | Effect |
--- | --- |  
`<C-v>{123}` | Insert a character by decimal code |
`<C-v>u{123}` | Insert a character by hexadecimal code |
`<C-v>{nondigit}` | Insert nondigit literally |
`<C-k>{char1}{char2}` | Insert character represented by {char1}{char2} diagraph |


Inside insert mode press `<C-o>zz` to move the screen to zenter
Inside insert mode press `<C-r>=`10+10`<CR>`
Inside insert mode press `<C-v>065`will insert `A`
Inside insert mode press `<C-v>u00bf`will insert `¿`


## Enabling visual modes

| Command | Effect |
--- | --- |  
`v` | Enable character-wise Visual mode |
`V` | Enable line-wise Visual mode |
`<C-v>` | Enable block-wise Visual mode |
`gv` | Reselecet the last visual selection |


## Command line mode


| Command | Effect |
--- | --- | 
`:6t.` | Copy line 6 to just below the current line |
`:6t.` | Copy the current line to just below line 6 |
`:t.` | Duplicate the current line (similar to Normal mode yyp) |
`:t$` | Copy line 6 to just below the current line |
`:’<,’>t0` | Copy the visually selected lines to the start of the file | 
`q/` | Open the command-line window with history of searches | 
`q:` | Open the command-line window with history of Ex commands | 
`crtl-f` | Switch from Command-Line mode to the command-line window | 






