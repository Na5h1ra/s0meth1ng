# UTM虚拟机安装的一些尝试

## 更新时间 2025.05.08
## iStoreOS

  参考了[悟空的日常](https://space.bilibili.com/250915741)的[这个视频](https://www.bilibili.com/video/BV1uf5EzdEvu)
  
  其中评论区有转换好的iStoreOS的arm架构的qcow2[镜像](https://github.com/wukongdaily/armbian-installer/releases/tag/iStoreOS-Installer-x86_64-ISO)

  可以像视频中那样加个串行以便在终端中粘贴命令，iStoreOS基本不需要，进入时候输入quickstart来配置，用户名为`root`，密码为`password`
  
## fnOS

  参考了这个[视频](https://www.bilibili.com/video/BV168d3Y7EzD)
  
  由于是x86架构，所以使用模拟，选Linux，载入飞牛的iso后一路默认(当然有些设置可以调低点)，显示可以选`VGA`，设置里网络选`桥接`，选一个网口比如`en1`是wifi，就能获得路由器下同网段的IP了,保存并启动，安装飞牛OS即可
  
## Syno1ogy

  这个没参考，纯粹尝试一下，其实和物理机安装差不多，竟然也能成功
  
  先下载rr引导的img版本尝试了下启动，无法启动黑屏，猜测是格式问题
  
  使用qemu-img工具转换为qcow2格式
  
  Windows下可以用[这个](https://cloudbase.it/qemu-img-windows/)，Mac可以安装Homebrew后`brew install qemu`
  
  这里在Windows下把rr.img放在了同目录下，打开Powershell，命令为`./qemu-img.exe convert -f raw -O qcow2 rr.img rr.qcow2`

  由于是x86架构，使用模拟，选择其他
  
  不勾选UEFI启动
  
  内存根据rr的要求最好4G以上，CPU核心多点可能比较好，因为选了2核心，发现模拟出来的CPU空载都占用21%

  输入里的`USB共享`不知道有没有用，先不勾选了

  显示尝试使用`virtio-VGA`

  可以加个串行以便查看运行时的log

  网络同样可以选`桥接`表示WiFi的`en1`

  驱动器第一个应该是默认的`接口`为`IDE`的`rr.qcow2`的`磁盘镜像`，这里把它想象成物理上的那个U盘引导

  显然还需要硬盘，由于是模拟,索性使用`NVME`
  
  `NVME`硬盘大小最好默认的64G（或者25G以上，因为安装完了，进入系统创建存储空间的时候可用空间是10G起步，太小的话像我填了个15G，没法下一步的）

  启动，进入rr引导，选中文，选型号为支持固态的SA6400，选版本号，为了使用固态，还需添加3个插件 `HDDdb`，`NvmeSystem`，`NvmeVolume`

  编译后启动，其实和普通的物理机安装差不多

## Win 7

  下载官方[模板](https://github.com/utmapp/vm-downloads/releases/download/windows-template/windows-7-x64-utm.zip)，下载指定版本的Win 7，才能运行

  有点卡顿，都是模拟出来的，没有硬件加速，扫雷都卡
  
## Win 11

  这个下载arm版本的iso安装即可，安装完可移除安装前的iso，勉强能用一用
