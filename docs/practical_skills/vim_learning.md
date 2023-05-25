# Vim
 
???+ abstract "Philosophy of Vim"
    When programming, you spend most of your time reading/editing, not writing. For this reason, Vim is a modal editor: it has different modes for inserting text vs manipulating text. Vim is programmable (with Vimscript and also other languages like Python), and Vim’s interface itself is a programming language: keystrokes (with mnemonic names) are commands, and these commands are composable. Vim avoids the use of the mouse, because it’s too slow; Vim even avoids using the arrow keys because it requires too much movement.

## Modal editing
Vim’s design is based on the idea that a lot of programmer time is spent reading, navigating, and making small edits, as opposed to writing long streams of text. For this reason, Vim has multiple operating modes.

* **Normal**: for moving around a file and making edits
* **Insert**: for inserting text
* **Replace**: for replacing text
* **Visual** (plain, line, or block): for selecting blocks of text
* **Command-line**: for running a command

Keystrokes have different meanings in different operating modes. For example, the letter `x` in Insert mode will just insert a literal character ‘x’, but in Normal mode, it will delete the character under the cursor, and in Visual mode, it will delete the selection.  

You change modes by pressing `<ESC>` (the escape key) to switch from any mode back to Normal mode. From Normal mode, enter Insert mode with `i`, Replace mode with `R`, Visual mode with `v`, Visual Line mode with `V`, Visual Block mode with `<C-v>` (Ctrl-V, sometimes also written `^V`), and Command-line mode with `:`.

You use the `<ESC>` key a lot when using Vim: consider remapping `Caps Lock` to `Escape` ([macOS instructions](https://vim.fandom.com/wiki/Map_caps_lock_to_escape_in_macOS)).

***

## Basics
### Inserting text
From Normal mode, press `i` to enter Insert mode. Now, Vim behaves like any other text editor, until you press `<ESC>` to return to Normal mode.  
### Buffers, tabs, and windows
Vim maintains a set of open files, called “buffers”. A Vim session has a number of tabs, each of which has a number of windows (split panes). Each window shows a single buffer.Vim maintains a set of open files, called “buffers”. A Vim session has a number of tabs, each of which has a number of windows (split panes). Each window shows a single buffer.

By default, Vim opens with a single tab, which contains a single window.  
### Command-line
Command mode can be entered by typing `:` in Normal mode.

|command|operation|
|:---:|:---:|
|`:q`|quit(close window)|
|`:w`|save(write)|
|`:wq`|save and quit|
|`:e {name of file}`|open file for editing|
|`:ls`|show open buffers|
|`:help {topic}`|open help|

`:help :w` opens help for the `:w` command  
`:help w` opens help for the `w` movement

***

## Vim’s interface is a programming language
The most important idea in Vim is that Vim’s interface itself is a programming language. Keystrokes (with mnemonic names) are commands, and these commands compose. This enables efficient movement and edits, especially once the commands become muscle memory.
### Movement
You should spend most of your time in Normal mode, using movement commands to navigate the buffer. Movements in Vim are also called “nouns”, because they refer to chunks of text.  

* Basic movement: `hjkl` (left, down, up, right)
* Words: w (next word), b (beginning of word), e (end of word)
* Lines: `0` (beginning of line), `^` (first non-blank character), `$` (end of line)
* Screen: `H` (top of screen), `M` (middle of screen), `L` (bottom of screen)  
* Scroll: `Ctrl-u` (up), `Ctrl-d` (down)
* File: `gg` (beginning of file), `G` (end of file)
* Line numbers: :{number}<CR> or {number}G (line {number})
* Misc: `%` (corresponding item)
* Find: `f{character}`, `t{character}`, `F{character}`, `T{character}`
    * find/to forward/backward {character} on the current line
    * `,` / `;` for navigating matches
* Search: `/{regex}`, `n` / `N` for navigating matches

### Selection
Visual modes:
Visual: `v`  
Visual Line: `V`  
Visual Block: `Ctrl-v`  
Can use movement keys to make selection.

### Edits
Everything that you used to do with the mouse, you now do with the keyboard using editing commands that compose with movement commands. Here’s where Vim’s interface starts to look like a programming language. Vim’s editing commands are also called “verbs”, because verbs act on nouns.  

* `i` enter Insert mode
    * but for manipulating/deleting text, want to use something more than backspace
* `o` / `O` insert line below / above
* `d{motion}` delete {motion}
    * e.g. `dw` is delete word, `d$` is delete to end of line, `d0` is delete to beginning of line
* `c{motion}` change {motion}
    * e.g. `cw` is change word
    * like `d{motion}` followed by `i`
* `x` delete character (equal do `dl`)
* `s` substitute character (equal to `cl`)
* Visual mode + manipulation
    * select text, `d` to delete it or `c` to change it
* `u` to undo, `<C-r>` to redo
* `y` to copy / “yank” (some other commands like `d` also copy)
* `p` to paste
* Lots more to learn: e.g. `~` flips the case of a character

### counts
You can combine nouns and verbs with a count, which will perform a given action a number of times.
* `3w` move 3 words forward
* `5j` move 5 lines down
* `7dw` delete 7 words

### Modifiers
You can use modifiers to change the meaning of a noun. Some modifiers are `i`, which means “inner” or “inside”, and `a`, which means “around”.
* `ci(` change the contents inside the current pair of parentheses
* `ci[` change the contents inside the current pair of square brackets
* `da'` delete a single-quoted string, including the surrounding single quotes

***

## some plugins
[recomended plugins](https://www.tabnine.com/blog/top-vim-plugins/)  
[vundle](https://github.com/VundleVim/Vundle.vim#about) it's a vim plugin manager