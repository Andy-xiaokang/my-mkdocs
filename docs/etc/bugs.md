---
comments: true
---

# Bugs&Questiions
## vscode
### vscodevim
In vscode settings.json add `"vim.mouseSelectionGoesIntoVisualMode": false,` to use mouse selection, however, it can't work. Just like [vim issues 1871](https://github.com/VSCodeVim/Vim/issues/1871) and [vim issues 2410](https://github.com/VSCodeVim/Vim/issues/2410), it drives me crazy, because it is a big difference between there is a mouse selecting and there isn't a mouse selection. The problem exists for nearly 2 months and it lead to me giving up using vscodevim at the beginning. However, after battle with this problem for nearly a half day I find it ==conflict with another software Youdao dictionary==. just forbid get word from the screen function. All right for vscodevim.  

## Python
### After changing user folder pyenv fault
reinstall python with the pyenv  

* `pyenv uninstall 3.11.3` you will find the `~/.pyenv/versions` remove 3.11.3
* then reinstall `pyenv install 3.11.3` 
* use `which python` and `where python` to test if pyenv work.  

