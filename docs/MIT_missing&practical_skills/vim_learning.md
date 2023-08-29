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
* Misc: `%` (corresponding item`[]{}()`)
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
## 如何在 Vim 中复制，剪切，粘贴
### 在正常模式复制，剪切以及粘贴
当你启动 Vim 编辑器时，默认就进入了正常模式。在这个模式，你可以运行 Vim 命令，并且浏览整个文件。
从其他任何模式返回正常模式，你只需要按`Esc`键。
Vim 对于复制，剪切，粘贴有它自己的一套术语。复制被叫做 yank(`y`),剪切被叫做 delete（`d`），以及粘贴被叫做 put（`p`）。
==**复制 (Yanking)**==
想要复制文本，将光标放到你想要的地方，然后参考下面的命令按键y。下面是一些有用的命令：

* `yy` - 复制当前行，包括换行符
* `3yy` - 复制从光标所在的当前行开始的三行文本
* `y$` - 复制从光标位置到行尾的文本
* `y^` - 复制从光标位置到行首的文本
* `yw` - 复制到下一个词的开头
* `yiw` - 复制当前词
* `y%` - 复制匹配符号范围内容。默认支持的符号对是(),{},[].这个在复制括号内内容时，很有用处。

==**剪切 (Deleting)**==

在正常模式下，`d`按键是用来剪切文本的。把光标移动到想要的位置，参考下面的命令按`d`按键。下面是一些有帮助的命令：

* `dd` - 剪切当前行，包括换行符
* `3dd` - 剪切从光标位置所在行开始的 3 行文本
* `d$` - 剪切从光标位置到行尾的内容
这些命令同时适用于删除的场景。例如，`dw`可以删除到下一个词的开头。而`d^`可以删除光标位置到行首的内容。 

粘贴 (Putting)
想要粘贴被剪切的内容，先将光标移动到想要的位置，然后按`p`键可以将内容粘贴到当前光标后面，或者按`P`按键可以粘贴到当前光标前面。

### 在可视模式下复制，剪切，粘贴
Vim 可视模式下，允许你选择和操作文本。

1. 将光标放到你想要开始复制或者剪切的那一行。
2. 可视模式有三个子类型
      * 按`v`进入可视模式
      * 按`v`进入可视行模式。该模式下文本可以按行来选择。
      * 按`Ctrl+v`进入可视块模式。该模式下文本可以按照文本块来选择。
进入可视模式当然也标记了你的开始选择点。
3. 将光标移动到你想要复制或者剪切的文本最后面。你可以使用上下左右按键来进行移动。
4. 按`y`进行拷贝，按d剪切选择文本。

### 在 insert/插入模式粘贴
在 `normal` 模式按下 `i` 或者 `a` 可以进入插入模式，也就是键入内容的模式。`p` 快捷键不可用于插入模式，但是插入模式可以通过 `Ctrl+r` 来访问所有的寄存器，插入寄存器里的内容。所有剪切、拷贝、删除的内容都会存在不同的 Vim 寄存器里。比如：

* `Ctrl+r` " 插入最近一次复制/剪切/删除的内容。" 是 Vim 的匿名寄存器。
* `Ctrl+r 0` 插入最近一次复制的内容。其中 `0` 属于 Vim 的编号寄存器，保存最近一次拷贝的内容。
* `Ctrl+r 1` 插入最近一次删除的内容，其中 `1` 属于 vim 的编号寄存器，保存最近一次删除的内容。
此外寄存器还保存有当前文件名、最近一次执行的命令、最近一次搜索内容、最近一次插入文本等。可以参考 [Vim 寄存器完全手册](https://harttle.land/2016/07/25/vim-registers.html)。


## some plugins
[recomended plugins](https://www.tabnine.com/blog/top-vim-plugins/)  
[vundle](https://github.com/VundleVim/Vundle.vim#about) it's a vim plugin manager
