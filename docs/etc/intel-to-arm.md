---
comments: true
---

# macbook M3pro 16inches migrate form intel to arm
## step1 back up old time machine from intel macbook
here is a small problem, the new macbook pro only has thunderbolt interface, and my old macbook pro only has a HDD with USB-A interface, i need buy a USB type-c to USB-A converting cable.  
## step2 命令行中的一些错误
* homebrew由于arm版路径变化需要重新安装，首先需要[重新安装comman-line-tools](https://sleele.com/2019/08/11/command-line-tools/)，然后根据这个[homebrew 迁移教程](https://aheadcreative.co.uk/articles/move-homebrew-to-arm-mac-from-an-intel-mac/)执行操作，具体思路是  
    1. `brew bundle dump` 生成一份 brewfile 的配置文件
    2. Uninstall Brew from old location
    3. Install Brew to new location(opt/homebrew)
    4. `brew budle` Reinstall config
* 通过 `pip` 安装的部分 sitepackages 报错
    `/Library/Frameworks/Python.framework/Versions/3.11/lib/python3.11/site-packages/` 路径下找到对应的 sitepackages 删除后通过 `pip` 重新安装
*  通过 `pyenv` 管理对应的Python版本
    这中间有个小插曲错误我不能理解，开始我卸载 Python 和 pyenv 后想看看在新环境下是否能够使用，于是通过 homebrew 安装 pyenv 后再次重新安装 Python3.11.3 时总是报错，说什么 use zlib from xcode, python-build error 之类的，我无法解决，但是睡了一觉后就好了。pyenv 常用的几个命令非常简单，总之就是先安装对应的 python 版本，然后设置为全局。
## step3 卸载 intel 版本的软件并重新安装，并处理一些软件问题
在通用/存储空间/应用程序中可以找到所有 intel 版本的软件，卸载后重新安装。 有的软件有 homebrew 可以直接安装的话就直接在命令行中一行命令安装。不可以的话就找官网。 
![20240304170254](https://s2.loli.net/2024/03/04/bAevLSmpWoNEqz8.png)

* Alfread 中的 workflow 失效，需要重新安装 alfread 后删除对应的 workflow 并重新安装和配置 workflow。
* Adguard 需要[关闭 SIP](https://developer.apple.com/documentation/security/disabling_and_enabling_system_integrity_protection)。 有一点出入的是输入命令后还需要输入管理员账户和密码。 此外不知道为何安装的脚本丢失了一个去网页去广告的脚本，可以去 geeksfork 下载想要的脚本并托管在Adguard中。比如可以去除 Youtube 首页的推荐广告。
* webcatalog 中安装的所有软件需要重新安装 比如我常用的 chatgpt X spotify 
* Qt creator 虽然是通用版，但打开后还是全屏报错，需要运行 maintennace 工具卸载后重新安装
* 其他最常用软件设置详见[mac tips](./mactips.md)
## step4 卸载一切不需要的软件和系统垃圾清理空间
* 卸载所有不需要的软件，可以借助 cleanmymacX 来卸载，并且可以清理系统缓存和应用缓存这两个部分，另外一些垃圾也可以清理。
* ~/Library/caches 和 /Library/caches 分别是系统缓存和应用缓存，可以全部清理也不会有什么影响。

## step5 更改显示字体大小
这台macbookpro 显示器是 16英寸(3456 × 2234) 可能由于分辨率太高，导致默认字体看起来非常小，这点在[reddiet](https://www.reddit.com/r/macbookpro/comments/quz1qt/text_size_is_a_bit_too_small_on_my_16_inch/)上也有讨论，我给出的回答是  
> here I suffered the same problem, When I get my new M3 macbook-pro 16inches with screen resolution(3456 × 2234), I find the font size displayed on my screen  are much more smaller compared with my old macbook, such as in settings, finder, vscode etc..., however in google chrome it's normal.  
here is my solutition

* in accessibility of settings the default font size is 12, change it to 13 applied to all the applications you can select.
* in vscode, go to preference and change the font size to 13.
* the default font size of google chrome is 16 so you don't need change it. that's what suitable solution for me, just offered for reference.  
另外有一点需要注意的是 MacOS 系统的字体大小单位是 pt, 而浏览器中的字体大小的单位是 px。这两者之间的区别是  
![20240305142339](https://s2.loli.net/2024/03/05/wphzTC3t7MXUZ2W.png)

## step6 更改、阅读、熟悉系统设置  
因为从老 mac 更新过来后系统设置界面 UI 发生了很大变化，很多地方需要熟悉或者更改成适合自己的  

1. 通用
    1. 关于本机
        macbook 简介，系统版本，显示器及设置（点击后可进入显示器设置），存储空间及设置（点击后可进入存储空间设置界面）
    2. 存储空间
        可以查看各种文件存储数据，在详细信息界面内还可以显示细则
        ![20240304192340](https://s2.loli.net/2024/03/04/GBWFQw6ApqDM5TJ.png)  
    3. 登录项
        登录项中可以管理登录自动打开的程序，以及管理后台程序
        ![20240304192537](https://s2.loli.net/2024/03/04/wWz8pTHiYueJgQ1.png)
    4. 时间机器
        时间机器可以选择时间机器进行备份
    5. 迁移或还原
        可以打开`迁移助理`进行数据迁移，也可以打开`抹掉助理`抹掉所有内容和设置
    6. 启动磁盘
        在启动磁盘中也可以选择启动电脑的磁盘和系统
2. 外观选择`浅色`，强调色为`多色`，边栏图标大小为`中`
3. 辅助功能中可以调节文字大小
    ![20240304194858](https://s2.loli.net/2024/03/04/Gn84oLmYdTNCeh9.png)
4. 控制中心尽可能设置简洁，只将部分必须使用的放入菜单栏，并关闭台前调度
    ![20240304195445](https://s2.loli.net/2024/03/04/w2USiOok8lGYcpb.png)
5. 隐私与安全性中可以设置应用权限，此外为方便安装软件`允许从以下位置下载的应用程序`设置为`任何来源`
6. 桌面与程序坞中可以设置程序坞的大小和效果，调度中心，以及触发角
    ![20240304200151](https://s2.loli.net/2024/03/04/fTt6hyFSgzwQq5D.png)
    将调度中心设置成`使窗口按应用程序分组`
    ![20240304200233](https://s2.loli.net/2024/03/04/JrDSozReM3PbAEq.png)
    并将触发角的左下角设置成`屏幕保护程序`方便进行隐私管理，此功能也集成在 alfred 系统功能中，关键词为`lock`触发锁屏。右下角保持系统默认 `快捷新建备忘录`。
7. 触控板中开启`单指轻点`，跟踪速度调整至最快，并开启所有的更多手势和滚动缩放功能。
