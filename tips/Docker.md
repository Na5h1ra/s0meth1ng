# Docker

> 自用Docker安装命令
>> 用于群晖和N1盒子。
>> 
>> N1盒子使用root权限登录，命令行安装，默认网络模式是bridge。
>> 
>> 群晖需要考虑权限问题,可添加privileged: true，user: root等命令。网络需要指定network_mode: bridge或者host，否则会创建新的桥接网络。
>> 
>> 可以使用 sudo netstat -anp | grep 端口号，来查询端口号是否被占用

## youshandefeiyang/allinone:latest
> [使用说明](https://github.com/youshandefeiyang/LiveRedirect/blob/main/Golang/README.md)
> 
```
docker run -d --name=allinone -p 35455:35455 --privileged=true --restart=always youshandefeiyang/allinone:latest
```
> 
```
services:
  allinone:
    image: youshandefeiyang/allinone:latest
    restart: unless-stopped
    user: root
    container_name: allinone
    network_mode: bridge
    ports:
      - 35455:35455
```

## pixman/pixman:latest
> [使用说明](https://pixman.io/topics/17)
> 
```
docker run -d --name=pixman -p 35456:5000 --restart=always pixman/pixman:latest
```
> 
```
name: pixman
services:
    pixman:
        image: pixman/pixman:latest
        restart: always
        container_name: pixman
        user: root
        network_mode: bridge
        ports:
            - 35456:5000

```

## herberthe0229/iptv-sources:latest
> [使用说明](https://github.com/HerbertHe/iptv-sources)
> 
```
docker run -d --name=iptv-sources -p 35457:8080 herberthe0229/iptv-sources:latest
```
> 
```
services:
  iptv-sources:
    image: herberthe0229/iptv-sources:latest
    restart: always
    container_name: iptv-sources
    user: root
    network_mode: bridge
    ports:
      - 35457:8080
```

## tindy2013/subconverter:latest
> 使用SSH进入后台，键入`curl http://localhost:25500/version`，出现`subconverter vx.x.x backend`说明搭建成功
>   
> [使用说明](https://github.com/tindy2013/subconverter/blob/master/README-cn.md)
>
```
docker run -d --name=subconverter -p 25500:25500 --restart=always tindy2013/subconverter:latest
```
> 
```
services:
  subconverter:
    image: tindy2013/subconverter:latest
    restart: always
    container_name: subconverter
    user: root
    network_mode: bridge
    ports:
      - 25500:25500
```

## p3terx/aria2-pro:latest
> [使用说明](https://p3terx.com/archives/docker-aria2-pro.html)
> 
> Docker CLI命令详见[这篇文章](https://p3terx.com/archives/synology-nas-docker-advanced-tutorial-deploy-aria2-pro.html)，注意-v 映射的文件夹是否正确
```
services:
  aria2-pro:
    container_name: aria2-pro
    image: p3terx/aria2-pro:latest
    user: root
    environment:
      - RPC_SECRET=nash1ra
      - RPC_PORT=6800
      - LISTEN_PORT=6888
    volumes:
      - /volume1/docker/aria2/configs:/config
      - /volume1/Download/ariaDLs:/downloads
    network_mode: bridge
    ports:
      - 6800:6800
      - 6888:6888
      - 6888:6888/udp
    restart: unless-stopped
    logging:
      driver: json-file
      options:
        max-size: 1m
```

## deluan/navidrome:latest
> [使用说明](https://www.navidrome.org/docs/installation/docker/)，注意-v 映射的文件夹是否正确
>
```
docker run -d --name navidrome --restart=unless-stopped --user $(id -u):$(id -g) -v /mnt/mydisk/Music/Songs:/music -v /mnt/mydisk/data/NavidromeSettings:/data -p 4533:4533 -e ND_LOGLEVEL=info deluan/navidrome:latest
```
> 
```
services:
  navidrome:
    container_name: navidrome
    ports:
      - "4533:4533"
    user: root
    restart: unless-stopped
    network_mode: bridge
    volumes:
      - "/volume1/docker/navidrome/configs:/data"
      - "/volume1/1-Backup/Phones/K70/Music/Songs:/music:ro"
    image: deluan/navidrome:latest
```

## alexta69/metube:latest
> [使用说明](https://github.com/alexta69/metube)，注意-v 映射的文件夹是否正确。
> 
> 这个项目用的不是传统的PUID和PGID，N1我默认就是root用户，没啥问题。但是群晖默认可能会报权限错误，根据文档说明，需要添加两个环境变量UID和GID并设为0，将会以root权限写入文件。
```
docker run -d --name=metube -p 35550:8081 -v /mnt/mydisk/DLs/metubeDLs:/downloads ghcr.io/alexta69/metube:latest
```
> 
```
services:
  metube:
    image: alexta69/metube:latest
    container_name: metube
    environment:
      - UID=0
      - GID=0
    network_mode: bridge
    restart: unless-stopped
    ports:
      - "35500:8081"
    volumes:
      - /volume1/Download/metubeDLs:/downloads
```

## nyanmisaka/jellyfin:latest
> [使用说明](https://hub.docker.com/r/nyanmisaka/jellyfin)，注意-v 映射的文件夹是否正确，注意映射/dev/dri以便于硬解。
>
> [来源](https://registry.hub.docker.com/r/nyanmisaka/jellyfin/)：latest-legacy标签用于旧硬件，latest-rockchip标签用于arm64的硬件，latest标签用于新硬件。
> 
> 群晖下需要一些[操作](https://anerg.com/2023/05/17/how-to-set-hard-decoding-for-jellyfin-built-by-docker-in-synology.html)，“需要获取权限，ssh进入终端，sudo -i提升至root用户，输入ll /dev/dri，可以看到核显信息，然后需要获取renderD128这个设备的用户组，也就是videodriver的GID，常规情况下，即普通Linux下应该使用如下命令getent group render | cut -d: -f3，但是群晖是没有这个命令的，所以需要变通一下，使用下面的命令：synogroup --get videodriver，查询得GID为937。” 
```
docker run -d --name jellyfin -p 8098:8096 -p 8922:8920 -v /mnt/myemmc/jellyfin/config:/config -v /mnt/myemmc/jellyfin/cache:/cache -v /mnt/sda1/Videos:/media --device /dev/dri:/dev/dri --restart=always nyanmisaka/jellyfin:latest-rockchip

```
> 
```
services:
  jellyfin:
    image: nyanmisaka/jellyfin:latest
    container_name: jellyfin
    network_mode: bridge
    user: root
    group_add:
      - "937"
    devices:
      - /dev/dri:/dev/dri
    environment:
      - "TZ=Asia/Shanghai"
    volumes:
      - "/volume1/docker/jellyfin/config:/config"
      - "/volume1/docker/jellyfin/cache:/cache"
      - "/volume1/video:/media"
    ports:
      - 8096:8096
    restart: unless-stopped
```

## xream/sub-store:latest
> [使用说明](https://hub.docker.com/r/xream/sub-store)，注意-v 映射的文件夹是否正确。
> 
> 相关的[详细教程](https://xream.notion.site/Sub-Store-Docker-8efc1aea40fa431b9a562b78994e7fb8)
>
> 用了一阵，又弃用了，还需要设置cron定时任务，不然得手动更新订阅，稍稍有点没搞明白，不像subconverter拉取的时候也会顺带更新一下订阅。主要是馋文件管理里的的 查询流量信息订阅链接，因为我的配置全在gist上，但是gist拉取的配置，代理软件不会读取配置里的proxy-provider处的订阅链接Header请求头的Subscription-Userinfo，因此在clash的订阅页面也不会显示剩余流量到期时间啥的。后来看看surge也没地方显示，surfboard更是在配置的3个小点里面的panel页面显示，还是静态的需要机场支持，单单为了几个Clash整个剩余流量显示感觉也没太大必要。不如加个分组叫机场信息，正好有节点有剩余流量到期时间等相关的信息。等到时换机场没有这种节点了再说。
```
docker run -it -d --name=sub-store --restart=unless-stopped -p 25501:3001 -v /root/sub-store-data:/opt/app/data -e SUB_STORE_FRONTEND_BACKEND_PATH=/20位的数字与字母混合字符串 -e "SUB_STORE_PUSH_SERVICE=https://api.day.app/你自己的bark的token/[推送标题]/[推送内容]?group=SubStore&autoCopy=1&isArchive=1&sound=shake&level=timeSensitive&icon=https%3A%2F%2Fraw.githubusercontent.com%2F58xinian%2Ficon%2Fmaster%2FSub-Store1.png" xream/sub-store:latest
```
> 
```
services:
  sub-store:
    image: xream/sub-store:latest
    container_name: sub-store
    restart: unless-stopped
    network_mode: bridge
    user: root
    stdin_open: true
    tty: true
    volumes:
      - /volume1/docker/sub-store/data:/opt/app/data
    environment:
      - SUB_STORE_FRONTEND_BACKEND_PATH=/20位的数字与字母混合字符串
      - SUB_STORE_PUSH_SERVICE=https://api.day.app/你自己的bark的token/[推送标题]/[推送内容]?group=SubStore&autoCopy=1&isArchive=1&sound=shake&level=timeSensitive&icon=https%3A%2F%2Fraw.githubusercontent.com%2F58xinian%2Ficon%2Fmaster%2FSub-Store1.png
    ports:
      - "25501:3001"
```

## johngong/baidunetdisk:latest
> [使用说明](https://github.com/gshang2017/docker/tree/master/baidunetdisk)，注意-v 映射的文件夹是否正确。
>
> 需要在右上角设置下载目录为/config/baidunetdiskdownload
>
> 并未在N1上部署，因为N1芯片很弱，假如下载拉满，带宽不足，很有可能N1的后台都进不去，故无Docker CLI,不过可以自己用[这个网站](https://www.decomposerize.com)来转换
> 
```
services:
  baidunetdisk:
    image: johngong/baidunetdisk:latest
    container_name: baidunetdisk
    network_mode: bridge
    user: root
    environment:
      - NOVNC_LANGUAGE="zh_Hans"
    ports:
      - 5250:5800
      - 5900:5900
    volumes:
      - /volume1/docker/baidunetdisk/configs:/config
      - /volume1/docker/baidunetdisk/bdDLs:/config/baidunetdiskdownload
    restart: unless-stopped
```

## ghcr.io/gethomepage/homepage:latest
> [使用说明](https://gethomepage.dev/latest/)，注意-v 映射的文件夹是否正确。
>
> 图标来自[需这个网站](https://wiki.slarker.me/application/homepage.html)
>
> 并未在N1上部署，可用[这个网站](https://www.decomposerize.com)进行转换
> 
```
services:
  homepage:
    image: ghcr.io/gethomepage/homepage:latest
    container_name: homepage
    ports:
      - 35450:3000
    volumes:
      - /volume1/docker/homepage/config:/app/config
      - /volume1/docker/homepage/public/images/:/app/public/images
      - /var/run/docker.sock:/var/run/docker.sock
```
> Service.yaml示例，注意yaml有非常严格的缩进，不正确的缩进会疯狂报错。widget可在[这里](https://gethomepage.dev/latest/widgets/)查看，注意缩进。
```
- 我的设备:
    - 路由器名称:
        icon: /images/dashboard_icons/xiaomi.png
        href: 路由器ip
        description: 路由器
        siteMonitor: 路由器ip

- 文件服务:
    - Alist on PC:
        icon: /images/HD-Icons-main/svg/Alist_A.svg
        href: Alist地址
        description: 网盘挂载

- 实用工具:
    - Metube:
        icon: /images/HD-Icons-main/circle/Youtube-dl_A.png
        href: Metube地址
        description: 视频下载

- 影音视听:
    - Jellyfin:
        icon: /images/dashboard_icons/svg/jellyfin.svg
        href: jellyfin地址
        description: 影视媒体库
        container: jellyfin
        widget:
          type: jellyfin
          url: jellyfin地址
          key: 可去jellyfin后台申请
          enableBlocks: true
          enableNowPlaying: true
          enableUser: false
          showEpisodeNumber: false
          expandOneStreamToTwoRows: false
    - Navidrome:
        icon: /images/dashboard_icons/svg/navidrome.svg
        href: Navidrome地址
        description: 音乐库
        container: navidrome
        widget:
          type: navidrome
          url: Navidrome地址
          user: 用户名
          token: 可用F12刷新后查看
          salt: 可用F12刷新后查看
```
> settings.yaml示例，详细设置可在[这里](https://gethomepage.dev/latest/configs/settings/)查询
```
theme: dark

background:
  image: /images/background.jpg
  blur: sm

layout:
  我的设备:
    style: row
    columns: 5

  文件服务:
    style: column
    columns: 5

  实用工具:
    style: column
    columns: 5

  影音视听:
    style: column
    columns: 5

language: zh-CN

hideVersion: true
```
