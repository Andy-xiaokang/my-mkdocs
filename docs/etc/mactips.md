---
comments: true
---

# Mac tips 
## good software
### system efficiency tool
* [Alfread](https://www.alfredapp.com/)  
    Alfred is an award-winning app for macOS which boosts your efficiency with hotkeys, keywords, text expansion and more. Search your Mac and the web, and be more productive with custom actions to control your Mac.
* [cheatsheet](https://www.mediaatelier.com/CheatSheet/)  
    CheatSheet is a free utility app that lets you see keyboard shortcuts with a press of a button. (CheatSheet has been discontinued because it no longer works with macOS 14 Sonoma. [KeyCue](https://www.ergonis.com/keycue/switching/cheatsheet) is still available.)
* [maccy](https://github.com/p0deje/Maccy)  
    Maccy is a lightweight clipboard manager for macOS.
* [customShortcuts](https://www.houdah.com/customShortcuts/download.html)  
    Customize Mac Menu Keyboard Shortcuts
* [rectangle](https://rectangleapp.com)  
    Move and resize windows in macOS using keyboard shortcuts or snap areas

### system experience enhancement tools
* [ClashX](https://github.com/yichengchen/clashX)  
    A rule based proxy For Mac base on [Clash](https://dreamacro.github.io/clash/).
* [Adguard](https://adguard.com/en/welcome.html)  
    Surf the Web ad-free and safely. Shield up!
* [Bartender](https://www.macbartender.com/)  
    Bartender is an award-winning app for macOS that superpowers your menu bar, giving you total control over your menu bar items, what's displayed, and when, with menu bar items only showing when you need them.
    Bartender improves your workflow with quick reveal, search, custom hotkeys and triggers, and lots more.
* [AppCleaner](https://freemacsoft.net/appcleaner/)  
    AppCleaner is a small application which allows you to thoroughly uninstall unwanted apps.
### software reference website 
* [appstorrent](https://appstorrent.ru/)
* [xclient](https://xclient.info/s/)

## shortcuts 
* cheatsheet `command` 2s view the shortcuts of application's menu bar 
* `shift + command + .` 打开隐藏文件夹
* 开机键 + `command + R` 从内建 macOS 恢复系统启动
* 开机键 + `option` 启动进入“启动管理器”，您可以从中选取其他可用的启动磁盘或宗卷
* [mac 的 启动组合键](https://support.apple.com/zh-cn/HT201255)
* `option +delete`  delete a word
* `command + delete` delete a line
* `enter` rename the file or folder


## configuration
### [mac set up guide](https://sourabhbajaj.com/mac-setup/)
### [my dotfiles](https://github.com/Andy-xiaokang/dotfiles)  
### [some new mac settings](https://www.youtube.com/watch?v=WbklMGq59DU)  

## change user home folder name `~`  
### [change home folder name](https://support.apple.com/zh-cn/HT201548)  
### [ennable root user login](https://support.apple.com/zh-cn/HT204012)  
after log out or restart select others  
then user name fill in `root`  
password fill in password for `root`  

## use time machine backup system and replace SSD  
### [create external booter](https://support.apple.com/zh-cn/HT201372)  
### [youtube replace SSD reference](https://www.youtube.com/watch?v=KT3IKRYqEJU&list=PLXNz0NSnoTFYvmbM0W1DWUuUWo20cQYN9)  
### [use time machine backup mac](https://support.apple.com/zh-cn/HT201250)  
after backup when restart the new mac select use time machine restore datas  
### [mac 启动组合键](https://support.apple.com/zh-cn/102603)  

## proxy
### telegram 
data and storage > use proxy > socks5 host: 127.0.0.1  port: 7890 (which is the port for clashX)
### Spotify
when counter with country and region are different from your infrmation  
use proxy in the login interface go settings  
use proxy socks5 host: 127.0.0.1   port: 7890  
### [clashX allow LAN](https://blog.mebi.me/post/clash-speed-other-devices#%E4%BB%8B%E7%BB%8D)  
to let other devices to go though the GFW without download clash and purchase proxy service  
and you can turn off the DHCP 

* let your Computer and devices connected to the same LAN  
* turn on the allow lan button of clashX
* open the network settings and remember the ip address 
* open ipad network settings -> proxy configuration -> mannual select
* fill in the ip address and port is 7890 (clashX port)  

## [chatgpt](https://chat.openai.com/)
* [webCatalog](https://webcatalog.io/en/)  
    Transform websites into desktop apps with WebCatalog, and access a wealth of exclusive apps for Mac,  
    then you can pack the chatgpt website in local and revoke chatgpt with Alfred  
* [SMS activate](https://sms-activate.org/en)  
    register a chapgpt account then you can use the free chatgpt version.
* proxy group  add `- DOMAIN-SUFFIX,chat.openai.com,动画疯` in the configuration file, the ip address will be changed to taiwan to use ChatGpt, and ban **auto update** in 配置/托管配置

## [picture bed](https://github.com/Molunerfinn/PicGo/releases/tag/v2.3.1)
upload image you can  

1. use **PicGo** extension for vscode use `option+command+u` to upload the image  
      1. select extension->installed->PicGo->settings: `picgo> pic bed> current: smms`
      2. `picgo> pic bed> smms> tokens: `  add your [sm.ms token](https://smms.app/home/apitoken) 
2. [use github for your picture bed (not recommend )](https://juejin.cn/post/7031461637986975757)    

## auto fill passphase for ssh  
`ssh-add` then fill in the passphase  
`ssh-agent` to auto fill passphase  

## set off ipv6 Wi-Fi 
`sudo networksetup -listallnetworkservices`  
`sudo networksetup -setv6off Wi-Fi`  
then the wifi ip will changed from ipv6 to ipv4  

