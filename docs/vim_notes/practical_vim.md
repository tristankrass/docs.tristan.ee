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









`y` | Change |

