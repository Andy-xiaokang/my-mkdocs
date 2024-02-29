---
comments: true
---

# Mac tips 
## good software
### system efficiency tool
* [Alfread](https://www.alfredapp.com/)  
    Alfred is an award-winning app for macOS which boosts your efficiency with hotkeys, keywords, text expansion and more. Search your Mac and the web, and be more productive with custom actions to control your Mac.
* [Homebrew](https://brew.sh/)  
    The Missing Package Manager for macOS (or Linux)
* [cheatsheet](https://www.mediaatelier.com/CheatSheet/)  
    CheatSheet is a free utility app that lets you see keyboard shortcuts with a press of a button. (CheatSheet has been discontinued because it no longer works with macOS 14 Sonoma. [KeyCue](https://www.ergonis.com/keycue/switching/cheatsheet) is still available.)
* [maccy](https://github.com/p0deje/Maccy)  
    Maccy is a lightweight clipboard manager for macOS.
* [customShortcuts](https://www.houdah.com/customShortcuts/download.html)  
    Customize Mac Menu Keyboard Shortcuts
* [rectangle](https://rectangleapp.com)  
    Move and resize windows in macOS using keyboard shortcuts or snap areas
* [webCatalog](https://webcatalog.io/en/desktop/)  
    Transform websites into desktop apps with WebCatalog Desktop, and access a wealth of exclusive apps for Mac, Windows, Linux. Use spaces to organize apps, switch between multiple accounts with ease, and boost your productivity like never before.  
    I can add X, spotify, chatgpt etc to local and corordinate with alfread to swith those app local
* [Karabiner-Elements](https://karabiner-elements.pqrs.org/)  
    A powerful and stable keyboard customizer for macOS.

### system experience enhancement tools
* [ClashX](https://github.com/yichengchen/clashX)  
    A rule based proxy For Mac base on [Clash](https://dreamacro.github.io/clash/).
* [ClashX-Pro](https://github.com/Loyalsoldier/clash-rules/tree/master?tab=readme-ov-file).  
    proxy-providers and rule-providers
* [Adguard](https://adguard.com/en/welcome.html)  
    Surf the Web ad-free and safely. Shield up!  
    in settings open 助手 for safari and chrome.
* [Bartender](https://www.macbartender.com/)  
    Bartender is an award-winning app for macOS that superpowers your menu bar, giving you total control over your menu bar items, what's displayed, and when, with menu bar items only showing when you need them.
    Bartender improves your workflow with quick reveal, search, custom hotkeys and triggers, and lots more.
* [BetterTouchTool](https://folivora.ai/)  
    BetterTouchTool is a great, feature packed app that allows you to customize various input devices on your Mac.
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
* `fn` switch input method


## configuration
* [mac set up guide](https://sourabhbajaj.com/mac-setup/)
* [my dotfiles](https://github.com/Andy-xiaokang/dotfiles)  
* [some new mac settings](https://www.youtube.com/watch?v=WbklMGq59DU)  

## change user home folder name `~`  
* [change home folder name](https://support.apple.com/zh-cn/HT201548)  
* [ennable root user login](https://support.apple.com/zh-cn/HT204012)  
after log out or restart select others  
then user name fill in `root`  
password fill in password for `root`  

## use time machine backup system and replace SSD  
* [create external booter](https://support.apple.com/zh-cn/HT201372)  
* [youtube replace SSD reference](https://www.youtube.com/watch?v=KT3IKRYqEJU&list=PLXNz0NSnoTFYvmbM0W1DWUuUWo20cQYN9)  
* [use time machine backup mac](https://support.apple.com/zh-cn/HT201250)  
after backup when restart the new mac select use time machine restore datas  
* [mac 启动组合键](https://support.apple.com/zh-cn/102603)  

## proxy
* telegram 
data and storage > use proxy > socks5 host: 127.0.0.1  port: 7890 (which is the port for clashX)
### Spotify
when counter with country and region are different from your information  
use proxy in the login interface go settings  
use proxy socks5 host: 127.0.0.1   port: 7890   

* [clashX allow LAN](https://blog.mebi.me/post/clash-speed-other-devices#%E4%BB%8B%E7%BB%8D), to let other devices to go though the GFW without download clash and purchase proxy service, and you can turn off the DHCP 
    1. let your Computer and devices connected to the same LAN  
    2. turn on the allow lan button of clashX
    3. open the network settings and remember the ip address 
    4. open ipad network settings -> proxy configuration -> mannual select
    5. fill in the ip address and port is 7890 (clashX port)  

## [chatgpt](https://chat.openai.com/)
* [webCatalog](https://webcatalog.io/en/)  
    Transform websites into desktop apps with WebCatalog, and access a wealth of exclusive apps for Mac,  
    then you can pack the chatgpt website in local and revoke chatgpt with Alfred  
* [SMS activate](https://sms-activate.org/en)  
    register a chapgpt account then you can use the free chatgpt version.
* proxy group  add `- DOMAIN-SUFFIX,chat.openai.com,动画疯` or `- DOMAIN-SUFFIX,chat.openai.com,电报吹水` in the configuration file, the ip address will be changed to taiwan to use ChatGpt, and ban **auto update** in 配置/托管配置

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

## font
* iterm2 `Droid Sans Mono Slashed for Powerline`
* terminal `SM Mono Regular`
* mkdocs `Roboto Slab`

## keyboard 
* in settings keyboard -> keyboard `when stoke fn key, change input method`.  
* in settings keyboard -> modifier keys(修饰键) -> `caps lock : escape`.  
* in karabiner-elements  
    * find all devices set `caps lock: escape` and `escape: caps lock`.
    * Apple internal keyboard set `caps lock : escape` and `escape : caps lock`.  
    * bluetooth usb host controller `caps lock : escape` and `escape: caps lock`.

## github 免密 push
* [gh](https://github.com/cli/cli) `brew install gh`
* `gh auth login` 按照提示采用 ssh  

## store web resources
* 视频下载：`yt-dlp`
* `youtube-dl -a videos.txt`
* 扒课程页面所有资源： `wget -mkEpnp --no-check-certificate`  链接

## mac reference website
* [技术规格](https://support.apple.com/zh_CN/specs/maclaptops)
* [command line tools 下载](https://sleele.com/2019/08/11/command-line-tools/)  

## clashX-pro rule-set proxy-set
由于最开始买的一家机场跑路，让我不得不在 github 上接触到了 [clashX-pro](https://github.com/Loyalsoldier/clash-rules), 对clashX pro 的 [proxy-providers](https://clash.wiki/configuration/outbound.html#proxy-providers-%E4%BB%A3%E7%90%86%E9%9B%86) 和 [rule-providers](https://clash.wiki/premium/rule-providers.html) 这两样功能产生了强烈兴趣，但同时也遇到了不少问题。  

* `unmarshal errors` 可能是由于机场提供的链接并非是clash订阅链接，需要进行[订阅转换](https://acl4ssr-sub.github.io/)  
    [常见错误](https://github.com/githubvpn007/ClashX?tab=readme-ov-file#%E5%B8%B8%E8%A7%81%E9%94%99%E8%AF%AF)
    ![20240228204957](https://s2.loli.net/2024/02/28/4yiBOXN8GkFZEHx.png)
* 除了 `proxy-providers` 的 `provider` 可以使用 `filter:` 字段外，`proxy-groups` 中也可以在使用 `use` 字段后使用 `filter` 字段，例如
    ```yaml
    proxy-providers:
      provider2:
        type: http
        url: url2
        interval: 86400
        path: ./proxyset/provider2.yaml
        filter: '^(?!.*12).*'  # golang 负向前瞻（negative lookahead）排除那些倍率为12 的很坑的节点
        health-check:
          enable: true
          interval: 600
          url: http://www.gstatic.com/generate_204


    proxy-groups:
      - name: 美国
        type: url-test
        url: http://www.gstatic.com/generate_204
        interval: 500
        use: 
          - provider1
        filter: '美国' # golang regrex 匹配外部代理集 provider1 中那些节点名称中包含美国的节点
    ```
* 还有其他很多小问题和功能可以探索，就不一一列举了
