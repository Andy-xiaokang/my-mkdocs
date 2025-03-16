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

### vscode 编写C++ intelliSense 报错

* 注意添加编写 c_cpp_properties.json 文件
* 注意 includePath 添加的路径

## Python

### After changing user folder pyenv fault

reinstall python with the pyenv  

* `pyenv uninstall 3.11.3` you will find the `~/.pyenv/versions` remove 3.11.3
* then reinstall `pyenv install 3.11.3`
* use `which python` and `where python` to test if pyenv work.  

## rectangle pro

unknown for conflict with rectangle, when double click a window, the window will jump to next monitor.

## question with github

* the push record of green block was disappear when push to the remote repository  

when the local git `user.email` (the email address used for the commits ) is not associated with your account. the green block won't appear on the graph .

## Qt Creator

### getline(cin, s) don't wait user's input

![20240719173957](https://s2.loli.net/2024/07/19/NxOnu7TJGKPrLyD.png)

## Macbook

### magic trackpad 出现严重不跟手的问题

有一次发现使用 magic trackpad 出现严重不跟手的问题，尝试重启电脑无法解决，插入有线使用后明显好转，但是转而使用蓝牙也会变得不跟手、延迟很高，重启蓝牙后也无法解决，最终[重启触控板开关重新连接后恢复](https://www.v2ex.com/t/865636)  

### 终端 path 出现多余的环境变量

在 `/etc/path.d` 目录中找到对应于环境变量的文件并删除

