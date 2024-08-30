## [ffmpeg文档](https://ffmpeg.org/ffmpeg.html)
## [iPod Classic的Rockbox文档](https://download.rockbox.org/release/3.15/rockbox-ipod6g-3.15.pdf)
## [iPod Classic介绍](https://en.wikipedia.org/wiki/IPod_classic)


## iPod Classic的Rockbox里的[Mpeg Player plugin介绍](https://www.rockbox.org/wiki/PluginMpegplayer)：

  "The Mpeg Player is a video player plugin capable of playing back MPEG-1 and MPEG-2"
video streams with MPEG audio multiplexed into .mpg files.

   "The iPod Classic has a 2.5" backlit display at a resolution of 320×240."


### 单个flv文件转码为Rockbox支持的mpeg视频，代码为：
  ffmpeg -i input.flv -s 320x180 -vcodec mpeg2video -b:v 320k -b:a 192k -ac 2 -ar 44100 -acodec mp3 output.mpg 

### 批量转换文件夹下的flv为mpeg视频，代码为：
  for %%i in (.\*.flv) do ffmpeg -i "%%i" -s 320x180 -vcodec mpeg2video -b:v 320k -b:a 192k -ac 2 -ar 44100 -acodec mp3 "%%~dpni.mpg"

### 以下是2021年写的一次iPodClassic刷机体验，仅供参考

  从抽屉里翻出个旧的iPod，已经吃灰好几年了，不常听，因为它不支持无损歌曲的播放，而且每次传歌都得打开iTunes导入，iTunes打开很慢，传歌传视频也非常的慢，有时还得等它转码。

  于是看见网上有刷Rockbox的帖子，可以支持播放无损音乐。搜索了一波，发现大多都是7，8年前的帖子，步骤特别复杂，而且有些人还失败了。想到现在已经是21年了，刷机的步骤应该是越来越趋于完善了，于是登上Rockbox的官网，发现有个叫Rockbox Utility的工具，并在[Rockbox on iPod Classic](https://files.freemyipod.org/~user890104/bootloader-ipodclassic.html)网站上，看到了个18年底的刷机视频，还是双系统启动[Install Rockbox (with dual-boot bootloader) on iPod Classic using Windows](https://www.youtube.com/watch?v=e1BMqDyIGNU)，（怕失败没有驱动啥的所以提前安装好了iTunes，保证iTunes识别到iPod）。

  于是照着视频，下载了工具，选择了对应的iPod型号，选择了最新的stable固件，先勾选了除Bootloader外的所有东西，点Install刷入。

  完成后再反选，只选Bootloader，点Install刷入，等到电脑屏幕上的跳出提示，长按SELECT+MENU进入DFU模式，然后等到显示DFU Mode detected，之后再松开那两个按键，等进度条跑完，Rockbox就成功的刷入了。

  按照这个工具解释的说法，如果要进入原系统只需按住SELECT+MENU重启的同时，把Hold键改成锁定状态就行了，正常按SELECT+MENU重启就是Rockbox系统。

  接下来要折腾的就是主题和字体了，主题不用说，在Rockbox Utility的Themes右边有个Customize，选择喜欢的，下载安装即可。当然有些主题得手动解压文件，比如6M大小的比较现代的FreshOS主题，官方收录的是预览版，得自己解压。当然自己做也是可以的，使用下列官方的主题编辑器（虽然这个编辑器已经六七年没更新了）[rbthemeeditor](https://www.file-upload.net/download-14086491/rbthemeeditor.exe.html)，在[RockboxThemes](https://www.rockbox.org/wiki/RockboxThemes)可以看到主题的详细参数解释。

  字体比较头疼，里面基本都是英文字体，不支持CJK字符集，系统语言改成中文的话，就会都是方块，没法读。于是乎发现有个叫unifont的自带字体支持中文，切换后，虽然支持，但是实在不合我胃口，一通搜索看看有啥别的支持中文的字体，网上大多推荐文泉驿的wqy-microhei，但还是不合我意。

  心想能不能用自己的字体，但是发现这个Rockbox用的是专有的位图fnt格式的字体，Rockbox网站上的字体转换工具又太复杂看不懂，而且网上关于介绍Rockbox中文字体的帖子几乎没有，都是介绍文泉驿字体的。

  功夫不负有心人，知乎上搜到一篇关于[Rockbox 的字体折腾](https://zhuanlan.zhihu.com/p/70392435)的文章，提到了可以用convttf工具来转换字体，用法是convttf -p [字号] -c [字符间像素间隔] xxx.ttf。中文找个合你口味的字体即可，我找的是豆瓣上这篇[推荐几个Kindle的字体](https://www.douban.com/note/269330253/)里的華康細明體12.ttf，然后自己修改了一些标点符号的自制魔改字体，字体大佬@落霞孤鹜lxgw也分享了许多好看的字体，字号的话基本都是16，18，20三个当中看实际情况挑选，字符像素间隔为0。

  但是知乎这篇文章提到的这个工具似乎是在Linux系统下运行的，于是在[一个韩国Naver博客](https://blog.naver.com/clove7802/221225440257)，看到一个Windows下能用的程序，解压缩上面提供的convttf.zip后把字体文件放在该文件夹内，打开CMD或者PowerShell，输入上一段的命令（报错可把convttf换成convttf.exe，PowerShell需输入.\convttf.exe），进行转换，就能得到fnt字体文件了，然后放在.rockbox下面的fonts文件夹，在设置里设置字体即可。

  不过即使这样折腾了好久，不管什么主题方块字是没了，但是总是缺字，比如“主题设置”四个字就只显示“主 置”，刚开始认为是字体的缘故，于是找各种字库比较全的字体用上述方法转换之后设置仍然缺字，后来将系统设置为繁体后竟然就不缺了，怀疑是转换的时候字体里的简繁字库发生了一些变化导致显示不全。

  原本iPod的系统支持mp4，但是刷了Rockbox后只支持mpg格式，因此需要采用ffmpeg转码，可参考[这篇科普](https://www.rockbox.org/wiki/PluginMpegplayer)。

  其中的ffmpeg用法有点旧，我参考科普后采用的是ffmpeg -i input.mp4 -s 320x180 -vcodec mpeg2video -b:v 320k -b:a 192k -ac 2 -ar 44100 -acodec mp3 output.mpg，具体的参数想修改的话，可以结合ffmpeg官方文档和上面那篇科普文里ffmpeg的参数解释部分，有些视频可能长宽比有问题，可以试试320x240

  图片浏览实测能看.png/.jpg/.gif格式的图片。

  里面还有小游戏譬如2048啥的，当然还有几个3D游戏，键位没搞明白不会玩，也怕经常按按键弄坏了。

  Rockbox的截屏比较奇怪，正常情况下，USB连到电脑上，iPod会显示一个USB的图片，电脑上出现个iPod的盘符，然后你可以拷歌进去。在系统-调试模式（勿入）里将Screendump设为Enabled，电脑此时就不认iPod了，截屏操作是插入USB，每插入一趟就在根目录下生成一个当前屏幕的截图，可以到不同的界面进行这个操作，期间电脑不会有任何反应，截完屏记得改回Disabled，这种截屏方式也算是比较奇葩了。

  然后又深挖了下，发现竟然还有模拟器[Rockbox UI Simulator](https://www.rockbox.org/wiki/UiSimulator)，不过得自己编译，但是我不是学计算机的，好在2018年网上有人发过[3.13旧版Rockbox](http://rasher.dk/rockbox/simulator/)，因此得以在能够电脑上体验。
