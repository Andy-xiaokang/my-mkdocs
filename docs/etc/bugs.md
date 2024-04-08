---
comments: true
---

# Bugs && Questiions
## vscode
### vscodevim
In vscode settings.json add `"vim.mouseSelectionGoesIntoVisualMode": false,` to use mouse selection, however, it can't work. Just like [vim issues 1871](https://github.com/VSCodeVim/Vim/issues/1871) and [vim issues 2410](https://github.com/VSCodeVim/Vim/issues/2410), it drives me crazy, because it is a big difference between there is a mouse selecting and there isn't a mouse selection. The problem exists for nearly 2 months and it lead to me giving up using vscodevim at the beginning. However, after battle with this problem for nearly a half day I find it ==conflict with another software Youdao dictionary==. just forbid get word from the screen function. All right for vscodevim.  
### vscode 终端 path 环境变量的问题
在我下载好 homebrew 和 pyenv 后发现系统自带的 terminal.app 输出的 `$PATH` 与 vscode 终端中的 path 不一致，导致 vim 不能使用 `opt/homebrew/bin/vim` 中的vim, 以至于版本不一致导致的错误。解决方式，重新设置 vscode 中终端的环境变量与系统保持一致，进入 settings.json 文件，添加  
``` json
    "terminal.integrated.inheritEnv": false,
```
## Python
### After changing user folder pyenv fault
reinstall python with the pyenv  

* `pyenv uninstall 3.11.3` you will find the `~/.pyenv/versions` remove 3.11.3
* then reinstall `pyenv install 3.11.3` 
* use `which python` and `where python` to test if pyenv work.  

