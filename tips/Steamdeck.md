# SteamDeck备忘录

## 更新时间 2024.09.11
## 来源与相关文章

  B站搜索的拆机教学
  
  [败家君的游戏屋](https://space.bilibili.com/3493075198412853)
  
  [拜托了小峰峰](https://space.bilibili.com/885826)
  
  [灵翼MAGICWING](https://space.bilibili.com/55739750)
  
  [初之音的博客：Steam Deck 初步上手指南](https://www.himiku.com/archives/steamdeck.html)

## 语言切换
  最早开始我记得是切不了语言，只能用英文，后来应该是能改了。
  
  进入Regional Settings，进入Regional&Lan­guage，Language改成中文，并Apply应用，重启后就变成中文了

## SSH连接
  这个是真不知道可以SSH，以前都是Steam＋X唤起键盘硬输命令的（需要Steam打开，不然虚拟键盘无法唤醒），字也小。开启方法来自[初之音的博客：Steam Deck 初步上手指南](https://www.himiku.com/archives/steamdeck.html)

  先去设置用户密码，终端输入passwd更改密码，然后输`systemctl enable sshd`以及`systemctl start sshd`即可。再输入`systemctl status sshd`，若显示`Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; preset: disabled) ，Active: active (running)`等类似提示则说明开启成功，然后就可以用ssh在电脑或者别的设备远程连接deck了

## 修改商店软件源
  比如上海交大源，终端中输入`sudo flatpak remote-modify flathub --url=https://mirror.sjtu.edu.cn/flathub`，改回原来默认源为`sudo flatpak remote-modify flathub --url=https://flathub.org/repo/flathub.flatpakrepo`

## 安装插件系统Decky-Loader
  [官方安装命令](https://github.com/SteamDeckHomebrew/decky-loader)：`curl -L https://github.com/SteamDeckHomebrew/decky-installer/releases/latest/download/install_release.sh | sh`

  但没有代理环境大概率装不了，使用[国内的源](https://github.com/YukiCoco/ToMoon)进行安装：`curl -L http://dl.ohmydeck.net | sh`

  安装完了顺便安装[Tomoon代理插件](https://github.com/YukiCoco/ToMoon)：`curl -L http://i.ohmydeck.net | sh`
## 截屏

游戏模式下是Steam＋R1截屏，不知道保存在哪，但可以保存一份副本，进入桌面模式，打开桌面模式下的 Steam，进入设置-游戏中-截图 部分的设置，勾选 保存一份我的截图的未压缩副本，并设置未压缩截图文件夹

## 开启SMB
  以前都是用Usermode FTP Server传的，比较麻烦
  
  可用[初之音](https://www.himiku.com/archives/steamdeck.html)大佬的脚本一键开启，命令如下
  
 `sh -c "$(curl -fsSL https://raw.githubusercontent.com/mikusaa/steamdeck-samba-server/main/script.sh)"`
## 安装Emudeck
  是一个前端，整合了各种模拟器后端，可根据[安装教程](https://emudeck.github.io/how-to-install-emudeck/steamos/)慢慢安装，最好先打开Tomoon开启代理，再去桌面模式下安装
