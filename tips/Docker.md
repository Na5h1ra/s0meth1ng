# Docker
## 更新时间 2025.10.18
> 自用Docker安装命令
>> 
>> 用于群晖和N1盒子。
>> 
>> N1盒子使用root权限登录，命令行安装，默认网络模式是bridge
>>
>> 所有 **`:`** 的左边都是外部实际的端口或者映射位置，可以按照情况更改，所有 **`:`** 的右边一定要和镜像作者写的一样，
>>
>> 注意-v映射的文件或文件夹，确保它是正确的
>>
>> 如果compose.yml相同路径下有文件夹，可简略成`./`,如`/volume1/docker/data:/data`  →→→  `./data:/data`
>>
>> depends_on参数用于定义依赖容器的启动顺序，healthcheck参数用于确保启动服务健康运行，假如有的话一般不更改原作者的这两个参数
>> 
>> 可使用`sudo netstat -anp | grep 端口号`，来查询目标端口号是否被占用
>> 
>> 群晖需要考虑权限问题,可添加`privileged: true`，`user: root`等命令，或利用`id 用户名`来确定UID和GID
>>
>> 网络需要指定`network_mode: bridge`或者`host`，否则会创建新的桥接网络。
>>
>> 或者创建一个指定名称的桥接网络，这样不用对外暴露内部端口，这在多个容器依赖时比较安全
>>
>> 可使用[这个网站](https://www.composerize.com/) 使得Docker CLI  →→→  Docker-Compose.yml
>>
>> [这个网站](https://www.decomposerize.com/)，则是逆转换 Docker-Compose.yml  →→→  Docker CLI
>>
>> 注册表镜像，可以填写[1panel](https://docker.1panel.live)和[耗子面板](https://hub.rat.dev)两个国内加速源，[来源](https://gist.github.com/y0ngb1n/7e8f16af3242c7815e7ca2f0833d3ea6)
>>

## youshandefeiyang/allinone:latest
> 作者新加了鉴权,[使用说明](https://github.com/youshandefeiyang/LiveRedirect/blob/main/Golang/README.md)
> 
```
docker run -d --name=allinone -p 35455:35455 --privileged=true --restart=always youshandefeiyang/allinone:latest -tv=true -aesKey=生成的key -userid=TG的id -token=生成的token
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
      - "35455:35455"
    command: -tv=true -aesKey=生成的key -userid=TG的id -token=生成的token
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
            - "35456:5000"

```

## 1activegeek/airconnect:latest
> [使用说明](https://github.com/1activegeek/docker-airconnect)
>
> 群晖可以安装[套件版](https://github.com/eizedev/AirConnect-Synology)，OpenWRT系统可以安装[LUCI版](https://github.com/sbwml/luci-app-airconnect)
```
docker run -d --name=airconnect --net=host 1activegeek/airconnect:latest
```
> 
```
services:
    airconnect:
        container_name: airconnect
        network_mode: host
        image: 1activegeek/airconnect:latest

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
      - "35457:8080"
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
      - "25500:25500"
```

## asdlokj1qpi23/subconverter:latest
> 使用SSH进入后台，键入`curl http://localhost:25501/version`，出现`subconverter vx.x.x backend`说明搭建成功
> 
> 支持singbox作为target，原版tindy2013的有可能会报no node错误
> 
> [使用说明](https://github.com/asdlokj1qpi23/subconverter/blob/master/README-cn.md)
>
```
docker run -d --name=subc0nverter -p 25501:25500 --restart=always asdlokj1qpi23/subconverter:latest
```
> 
```
services:
  subc0nverter:
    image: asdlokj1qpi23/subconverter:latest
    restart: always
    container_name: subc0nverter
    user: root
    network_mode: bridge
    ports:
      - "25501:25500"
```

## youshandefeiyang/sub-web-modify:latest
> [使用说明](https://github.com/youshandefeiyang/sub-web-modify)
>
> 是前端页面，但是不能选本地后端
```
docker run -d --name=sub-web-modify -p 25501:80 --privileged=true --restart=always youshandefeiyang/sub-web-modify:latest
```
> 
```
services:
  sub-web-modify:
    image: youshandefeiyang/sub-web-modify:latest
    restart: always
    container_name: sub-web-modify
    user: root
    network_mode: bridge
    ports:
      - "25502:80"
```

## p3terx/aria2-pro:latest
> [使用说明](https://p3terx.com/archives/docker-aria2-pro.html)
> 
> Docker CLI命令详见[这篇文章](https://p3terx.com/archives/synology-nas-docker-advanced-tutorial-deploy-aria2-pro.html)
```
services:
  aria2-pro:
    container_name: aria2-pro
    image: p3terx/aria2-pro:latest
    user: root
    environment:
      - RPC_SECRET=password
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

## p3terx/ariang:latest
> 此处为搭建的[详细说明](https://p3terx.com/archives/aria2-frontend-ariang-tutorial.html)
```
services:
  ariang:
    image: p3terx/ariang:latest
    container_name: ariang
    network_mode: bridge
    restart: unless-stopped
    ports:
      - 6880:6880
    logging:
        options:
            max-size: 1m
```

## deluan/navidrome:latest
> [使用说明](https://www.navidrome.org/docs/installation/docker/)
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
> [使用说明](https://github.com/alexta69/metube)
> 
> 这个项目根据文档说明，群晖需要添加两个环境变量UID和GID，并将其设为0，将会以root权限写入文件。
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
> [使用说明](https://hub.docker.com/r/nyanmisaka/jellyfin)，注意映射/dev/dri以便于硬解。
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
      - "8096:8096"
    restart: unless-stopped
```

## xream/sub-store:latest
> [使用说明](https://hub.docker.com/r/xream/sub-store)
> 
> 相关的[详细教程](https://xream.notion.site/Sub-Store-Docker-8efc1aea40fa431b9a562b78994e7fb8)
>
> 用了一阵，又弃用了，还需要设置cron定时任务，不然得手动更新订阅，稍稍有点没搞明白，不像subconverter拉取的时候也会顺带更新一下订阅。主要是馋文件管理里的的 查询流量信息订阅链接，因为我的配置全在gist上，但是gist拉取的配置，代理软件不会读取配置里的proxy-provider处的订阅链接Header请求头的Subscription-Userinfo，因此在clash的订阅页面也不会显示剩余流量到期时间啥的。后来看看surge也没地方显示，surfboard更是在配置的3个小点里面的panel页面显示，还是静态的需要机场支持，单单为了几个Clash整个剩余流量显示感觉也没太大必要。不如加个分组叫机场信息，正好有节点有剩余流量到期时间等相关的信息。等到时换机场没有这种节点了再说。
```
docker run -it -d --name=sub-store --restart=unless-stopped -p 25503:3001 -v /root/sub-store-data:/opt/app/data -e SUB_STORE_FRONTEND_BACKEND_PATH=/20位的数字与字母混合字符串 -e "SUB_STORE_PUSH_SERVICE=https://api.day.app/你自己的bark的token/[推送标题]/[推送内容]?group=SubStore&autoCopy=1&isArchive=1&sound=shake&level=timeSensitive&icon=https%3A%2F%2Fraw.githubusercontent.com%2F58xinian%2Ficon%2Fmaster%2FSub-Store1.png" xream/sub-store:latest
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
      - "25503:3001"
```

## johngong/baidunetdisk:latest
> [使用说明](https://github.com/gshang2017/docker/tree/master/baidunetdisk)
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
      - USER_ID=0
      - GROUP_ID=0
    ports:
      - 5250:5800
      - 5910:5900
    volumes:
      - /volume1/docker/baidunetdisk/configs:/config
      - /volume1/Download/bdDLs:/config/baidunetdiskdownload
    restart: unless-stopped
```

## zack357/douban-tool:latest
> [配置流程及报错解决办法](https://www.bilibili.com/opus/950624026692157449)
>
> 是B站up主`@ZDhimself`开发的观影与下载镜像
> 
```
services:
  douban-tool:
    image: zack357/douban-tool:latest
    user: root
    container_name: douban-tool
    network_mode: bridge
    ports:
      - "2346:5000"
    volumes:
      - /volume1/docker/doubantool/data:/app/data
      - /volume1/docker/doubantool/configs:/app/config
      - /volume1/Download/xunleiDLs:/downloads
    restart: unless-stopped
```

## cnk3x/xunlei:latest
> [使用说明](https://github.com/cnk3x/xunlei)
>
> 是从群晖套件里提取出来的非官方远程下载服务
>
> 并未在N1上部署，因为N1芯片很弱，假如下载拉满，带宽不足，很有可能N1的后台都进不去，故无Docker CLI,不过可以自己用[这个网站](https://www.decomposerize.com)来转换
> 
```
services:
  xunlei:
    image: cnk3x/xunlei:latest
    privileged: true
    container_name: xunlei
    network_mode: bridge
    ports:
      - "2345:2345"
    volumes:
      - /volume1/docker/xunlei/configs:/xunlei/data
      - /volume1/Download/xunleiDLs:/xunlei/downloads
    restart: unless-stopped
```

## johngong/qbittorrent:latest
> [使用说明](https://hub.docker.com/r/johngong/qbittorrent)
> 
> 此镜像可使用`QB_EE_BIN=true`启用增强版，比下面那个版本的qbittorrent优点在于可以自行设定Tracker列表
> 
> 群晖可使用`id 用户名`来查看UID和GID，此处使用的是root权限，故都为0
>
> 并未在N1上部署，因为N1芯片很弱，假如下载拉满，带宽不足，很有可能N1的后台都进不去，故无Docker CLI,不过可以自己用[这个网站](https://www.decomposerize.com)来转换
> 
```
services:
  qbittorrentee:
    image: johngong/qbittorrent:latest
    container_name: qbittorrentee
    user: root
    network_mode: bridge
    environment:
      - QB_WEBUI_PORT=8989
      - QB_EE_BIN=true
      - QB_TRACKERS_UPDATE_AUTO=true
      - QB_TRACKERS_LIST_URL=https://cdn.jsdelivr.net/gh/ngosang/trackerslist@master/trackers_all.txt
      - UID=0
      - GID=0
      - UMASK=022
      - TZ=Asia/Shanghai
    volumes:
      - /volume1/docker/qbittorrentee/configs:/config
      - /volume1/Download/doubantoolDLs:/Downloads
    ports:
      - 6881:6881
      - 6881:6881/udp
      - 8989:8989
    restart: unless-stopped
```

## superng6/qbittorrent:latest:latest
> [使用说明](https://sleele.com/2020/04/09/docker-qbittorrent-optimizing)
> 
> 此镜像为sleele大佬优化的qbittorrent。默认中文，全平台架构支持x86-64、arm64、arm32，但启动会访问Trackers的[更新列表](https://githubraw.sleele.workers.dev/XIU2/TrackersListCollection/master/best.txt)，访问不通畅会一直卡在启动容器阶段
> 
> 群晖可使用`id 用户名`来查看UID和GID，此处环境变量采用的是PUID和PGID，使用的是root权限，故都为0
>
> 并未在N1上部署，因为N1芯片很弱，假如下载拉满，带宽不足，很有可能N1的后台都进不去，故无Docker CLI,不过可以自己用[这个网站](https://www.decomposerize.com)来转换
> 
```
services:
  qbittorrentee:
    image: superng6/qbittorrent:latest
    container_name: qbittorrentee
    user: root
    network_mode: bridge
    environment:
      - PUID=0
      - PGID=0
      - TZ=Asia/Shanghai
    volumes:
      - /volume1/docker/qbittorrentee/configs:/config
      - /volume1/Download/doubantoolDLs:/downloads
    ports:
      - 6881:6881
      - 6881:6881/udp
      - 8080:8080
    restart: unless-stopped
```

## ghcr.io/gethomepage/homepage:latest
> [使用说明](https://gethomepage.dev/latest/)
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
    network_mode: bridge
    ports:
      - "35450:3000"
    volumes:
      - /volume1/docker/homepage/config:/app/config
      - /volume1/docker/homepage/public/images/:/app/public/images
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      - HOMEPAGE_ALLOWED_HOSTS=IP地址或域名:端口号
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


## gotson/komga:latest
> 某大佬的[使用介绍与体验](https://www.himiku.com/archives/komga.html)
>
> 需要设置目录，注意开启文件哈希会占用很多内存，谨慎开启。刮削有点复杂，所以没搞，具体可以看大佬的博客及其评论区。
>
> 并未在N1上部署，因为在N100上光看1篇300MB的PDF，后台的java进程就飙升到了惊人的3.2G，对于只有2G内存的N1盒子实在是捉襟见肘。
>
> 由于是内网使用，邮箱密码可以随便输入
```
services:
  komga:
    container_name: komga
    image: gotson/komga:latest
    user: root
    restart: unless-stopped
    network_mode: bridge
    ports:
      - "23333:25600"
    environment:
      - "TZ=Asia/Shanghai"
    volumes:
      - "/volume1/docker/komga/config:/config"
      - "/volume1/manga:/comic"
```


## homeassistant/home-assistant:latest（未完善）
> 官方搭建[指南](https://www.home-assistant.io/installation/alternative)
>
> 后来又安装了[冬瓜OS](https://www.wghaos.com)，还在慢慢摸索
```
services:
  homeassistant:
    image: homeassistant/home-assistant:latest
    container_name: homeassistant
    restart: unless-stopped
    user: root
    network_mode: bridge
    volumes:
      - /volume1/docker/homeassistant/config:/config
    ports:
      - '8123:8123'
    environment:
      - TZ=Asia/Shanghai
```


## gitea/gitea:latest
> 官方搭建[指南](https://docs.gitea.com/zh-cn/installation/install-with-docker)
```
services:
  gitea:
    image: gitea/gitea:latest
    container_name: gitea
    restart: always
    network_mode: bridge
    user: root
    volumes:
      - /volume1/docker/gitea/data:/var/lib/gitea
      - /volume1/docker/gitea/config:/etc/gitea
    ports:
      - "8991:3000"
      - "8992:2222"
```



## advplyr/audiobookshelf:latest
> 官方搭建[指南](https://www.audiobookshelf.org/docs/#docker-compose-install)
```
services:
  audiobookshelf:
    image: advplyr/audiobookshelf:latest
    container_name: audiobookshelf
    user: root
    network_mode: bridge
    restart: unless-stopped
    ports:
      - 8990:80
    volumes:
      - /volume1/docker/audiobookshelf/audiobooks:/audiobooks
      - /volume1/docker/audiobookshelf/podcasts:/podcasts
      - /volume1/docker/audiobookshelf/config:/config
      - /volume1/docker/audiobookshelf/metadata:/metadata
    environment:
      - TZ=Asia/Shanghai
```


## hectorqin/reader:latest
> 官方搭建[指南](https://github.com/hectorqin/reader/blob/master/doc.md)，以及注释[文档](https://raw.githubusercontent.com/hectorqin/reader/master/docker-compose.yaml)
> 
> 不管配置文件如何编写，用户上限为15个
```
services:
  reader3:
    image: hectorqin/reader:latest
    container_name: reader3
    restart: always
    network_mode: bridge
    ports:
      - 8993:8080
    volumes:
      - /volume1/docker/reader3/logs:/logs
      - /volume1/docker/reader3/storage:/storage
    environment:
      - SPRING_PROFILES_ACTIVE=prod
      - READER_APP_USERLIMIT=50
      - READER_APP_USERBOOKLIMIT=1000
      - READER_APP_CACHECHAPTERCONTENT=true
      - READER_APP_SECURE=true
      - READER_APP_SECUREKEY=admin
```



## ghcr.io/haishanh/yacd:master
> 经典Clash面板
```
services:
  yacd:
    image: ghcr.io/haishanh/yacd:master
    container_name: yacd
    user: root
    network_mode: bridge
    restart: always
    ports:
      - 8995:80
```


## ghcr.io/metacubex/metacubexd
> Meta内核开发者的Clash面板
```
services:
  metacubexd:
    image: ghcr.io/metacubex/metacubexd
    container_name: metacubexd
    user: root
    network_mode: bridge
    restart: always
    ports:
      - 8998:80
```

## ghcr.io/zephyruso/zashboard:latest
> 新出的Clash面板
```
services:
  zashboard:
    image: ghcr.io/zephyruso/zashboard:latest
    container_name: zashboard
    user: root
    network_mode: bridge
    restart: always
    ports:
      - 8996:80
```


## ghcr.io/kiwix/kiwix-serve:latest
> Kiwix离线维基百科，此处为搭建的[详细说明](https://github.com/kiwix/kiwix-tools/tree/main/docker/server)
```
services:
  kiwix:
    image: ghcr.io/kiwix/kiwix-serve:latest
    container_name: kiwix
    user: root
    network_mode: bridge
    volumes:
      - "/volume2/Kiwix/data:/data"
    ports:
      - 8999:8080
    command:
      - '*.zim'
```

## stirlingtools/stirling-pdf:latest
> 本地PDF处理工具
```
services:
  stirlingpdf:
    image: stirlingtools/stirling-pdf:latest
    container_name: stirlingpdf
    network_mode: bridge
    user: root
    restart: unless-stopped
    ports:
      - '9001:8080'
    volumes:
      - /volume1/docker/stirlingpdf/trainingData:/usr/share/tessdata
      - /volume1/docker/stirlingpdf/extraConfigs:/configs
      - /volume1/docker/stirlingpdf/customFiles:/customFiles
      - /volume1/docker/stirlingpdf/logs:/logs
      - /volume1/docker/stirlingpdf/pipeline:/pipeline
    environment:
      - DOCKER_ENABLE_SECURITY=false
      - INSTALL_BOOK_AND_ADVANCED_HTML_OPS=false
      - LANGS=zh_CN
```

## amilys/embyserver:beta
> lovechen的版本应该是删库了，应该只有个/config要映射，如果有多个媒体文件夹要映射也无所谓(:后面跟具体的名字然后映射到宿主机即可)。
>
> 似乎只有beta版能硬解，注意映射/dev/dri以便于硬解。
>
> （未完善）有些参数没有搞懂怎么配置，只好找网上别人的参考一下，比如[这个](https://wiki.mynas.chat/synology/emby_decode.html)
> 
```
services:
  emby:
    image: amilys/embyserver:beta
    container_name: emby
    network_mode: bridge
    privileged: true
    restart: always
    environment:
      - UID=0
      - GID=0
      - GIDLIST=0
      - TZ=Asia/Shanghai
    volumes :
      - /volume1/docker/emby/config:/config
      - /volume1/video:/media
    ports:
      - 8097:8096
      - 8920:8920
      - 1901:1900
      - 7359:7359
    devices:
      - /dev/dri:/dev/dri
```


## yaotutu/folder2podcast:latest
> 将本地文件夹变为RSS播客的转换器，安装文档和注意事项在[这](https://github.com/yaotutu/folder2podcast)
>
> 注意BASE_URL和healthcheck是实际内网地址(假如局域网搭建的话)且需要相同，PUID和PGID由于是root用户所以为0
>
> 规范的文件目录还没搞懂如何编排，先放一放，当前只需建一个文件夹，放好音频和封面cover.jpg即可
>
> 尝试在每个文件夹下放入podcast.json，试了很久，有3个参数`"titleFormat": "full"`，`"episodeNumberStrategy": "last"`，`"useMTime": false`，需要这么设置，iOS的播客客户端才能正确识别顺序（Android端不加这些参数，序号也是对的，为了两端都兼容还是加这些参数比较好）
```
services:
  folder2podcast:
    image: yaotutu/folder2podcast:latest
    container_name: folder2podcast
    ports:
      - "9000:3000"
    volumes:
      - /volume1/docker/folder2podcast/audiobooks:/podcasts:ro
    restart: unless-stopped
    network_mode: bridge
    user: root
    environment:
      - PORT=3000
      - AUDIO_DIR=/podcasts
      - BASE_URL=内网IP
      - PUID=0
      - PGID=0
    healthcheck:
      test: ["CMD", "wget", "-q", "--spider", "内网IP/podcasts"]
      interval: 30s
      timeout: 10s
      retries: 3
```


## xxnuo/mtranserver:latest
> 安装文档和注意事项在[此](https://github.com/xxnuo/MTranServer)
>
> 小众软件论坛上看见的，基于 Firefox 模型的本地私有翻译服务，目前支持的翻译种类比较少
> 
```
services:
  mtranserver:
    image: xxnuo/mtranserver:latest
    container_name: mtranserver
    user: root
    network_mode: bridge
    restart: unless-stopped
    ports:
      - 9002:8989
    volumes:
      - /volume1/docker/mtranserver/models:/app/models
```

## freshrss/freshrss:latest
> 安装文档和注意事项在[此](https://github.com/FreshRSS/FreshRSS/tree/edge/Docker)
> 
```
services:
  freshrss:
    image: freshrss/freshrss:latest
    container_name: freshrss
    restart: unless-stopped
    network_mode: bridge
    ports:
      - 9003:80
    logging:
      options:
        max-size: 10m
    volumes:
      - /volume1/docker/freshrss/data:/var/www/FreshRSS/data
      - /volume1/docker/freshrss/extensions:/var/www/FreshRSS/extensions
    environment:
      - TZ=Asia/Shanghai
      - CRON_MIN=45
```


## linuxserver/plex:latest
> 镜像[来源](https://hub.docker.com/r/linuxserver/plex)，可以多映射几个文件夹，比如music和tv可以分开
>
> 整了个Plex Pass，试试看效果怎么样，搭建参考来源是几个博客（[初之音](https://www.himiku.com/archives/build-my-music-library-service.html)，[RIN](https://blog.hinatarin.com/2021/04/21/set-up-your-own-media-server-with-plex-and-docker/)，[Tom](https://d3ac.xlog.app/Docker-an-zhuang-Plexmd?locale=zh)和官方的[支持文档](https://support.plex.tv/articles/201543147-what-network-ports-do-i-need-to-allow-through-my-firewall/)
>
> 知乎用户x1ao4的[专栏](https://www.zhihu.com/column/c_1627108324322734080)有较为详细的使用教程
>
> Docker版的装完,才发现有[群晖版本](https://www.plex.tv/media-server-downloads/?cat=nas&plat=synology-dsm7#plex-media-server)，但我估计DSM上权限应该会收的比较紧，不一定能访问别的文件夹，就先不装群晖版本
> 
> 下面是 **`错误`** 的示例，不要使用，网络模式使用bridge方式，就是不知道错在哪了，搭完plex后台的内部网络是docker使用的172开头的IP地址（局域网设备完全没法用，一直会请求172开头的地址），而且还一直提示使用Plex中转
>

```
services:
  plex:
    image: linuxserver/plex:latest
    container_name: plex
    network_mode: bridge
    user: root
    ports:
      - 32400:32400/tcp
      - 5354:5353/tcp
      - 8324:8324/tcp
      - 32469:32469/tcp
      - 1902:1900/udp
      - 32410:32410/udp
      - 32412:32412/udp
      - 32413:32413/udp
      - 32414:32414/udp
    environment:
      - PUID=0
      - PGID=0
      - TZ=Asia/Shanghai
      - PLEX_CLAIM=申请的CLAIM代码
      - VERSION=docker
    volumes:
      - /volume1/docker/plex/config:/config
      - /volume1/video/:/tv
      - /volume1/Music/:/music
    devices:
      - /dev/dri:/dev/dri
    restart: unless-stopped
```

> 遂将网络模式换成了host（官方还有macvlan方式，感觉更加的复杂）
>
> 可以使用，重启容器之后基本正常，其中 **`设置`** -  **`网络`** - **`无需身份验证即可获得允许的 IP 地址和网络列表`** ，可以设置成 **`IP端/子网掩码`** 的形式，比如我这里使用`192.168.10.0/255.255.255.0`
>
> 示例如下
```
services:
  plex:
    image: linuxserver/plex:latest
    container_name: plex
    network_mode: host
    user: root
    environment:
      - PUID=0
      - PGID=0
      - TZ=Asia/Shanghai
      - PLEX_CLAIM=申请的CLAIM代码
      - VERSION=docker
    volumes:
      - /volume1/docker/plex/config:/config
      - /volume1/video/:/tv
      - /volume1/Music/Songs:/music
    devices:
      - /dev/dri:/dev/dri
    restart: unless-stopped
```

## hisatri/lrcapi:latest
> [使用说明](https://github.com/HisAtri/LrcApi/)
> 
> 给音流等音乐软件提供歌词和封面api的一个工具
```
services:
    lrcapi:
        image: hisatri/lrcapi:latest
        restart: unless-stopped
        container_name: lrcapi
        network_mode: bridge
        ports:
            - 9005:28883
        volumes:
            - /volume1/Music:/music
```

## makedie/noname_kill:latest
> 无名杀本地网页版，没找到官方的搭建指南，这是某网站的 [使用说明](https://newzone.top/services/dockers-on-nas/noname.html#%E9%83%A8%E7%BD%B2%E4%BB%A3%E7%A0%81)
```
services:
  nonamekill:
    image: makedie/noname_kill:latest
    restart: unless-stopped
    container_name: nonamekill
    network_mode: bridge
    ports:
      - 9006:80
```

## haroldli/xiaoya-tvbox:latest
> 小雅的tvbox版，可以顺便把tvbox源整合，以及可以生成 **`猫影视`** 使用的源， [使用说明](https://har01d.cn/#/notes/alist-tvbox)
>
> 可以搭配[Vidplay](https://apps.apple.com/us/app/vidplay-vod-player/id6467240929)使用
>
> 或者就当成普通的tvbox用
```
services:
  xiaoyatvbox:
    image: haroldli/xiaoya-tvbox:latest
    container_name: xiaoyatvbox
    user: root
    network_mode: bridge
    restart: always
    ports:
      - 5344:80
      - 4567:4567
    volumes:
      - /volume1/docker/xiaoyatvbox/xiaoya:/data
    environment:
      - ALIST_PORT=5344
```

## wbsu2003/drawnix:latest
> 开源思维导图/白板/流程图，可导出图片，[使用说明](https://github.com/plait-board/drawnix)
> 
```
services:
  drawnix:
    image: wbsu2003/drawnix:latest
    container_name: drawnix
    network_mode: bridge
    restart: unless-stopped
    ports:
      - 9007:7200
```

## oldiy/dosgame-web-docker:latest
> 本地搭建网页DOS游戏，[使用说明](https://poiblog.com/archives/ZHwUHFTm)
> 
> 如果要全部下载，需要在 volumes 映射 /app/static/games 到实际的目录，下载并放置游戏于文件夹内
```
services:
  dosgame:
    image: oldiy/dosgame-web-docker:latest
    container_name: dosgame
    network_mode: bridge
    ports:
      - 9008:262
```

## neosmemo/memos:stable
> 碎片化笔记备忘录memeos，类似flomo
> 
> [使用说明](https://github.com/usememos/memos)
```
services:
  memos:
    image: neosmemo/memos:stable
    container_name: memos
    network_mode: bridge
    restart: unless-stopped
    volumes:
      - /volume1/docker/memos/memos:/var/opt/memos
    ports:
      - 9009:5230
```

## lovasoa/wbo:latest
>  本地涂鸦白板
> 
>  [使用说明](https://github.com/lovasoa/whitebophir)
```
services:
  wbo:
    image: lovasoa/wbo:latest
    container_name: wbo
    network_mode: bridge
    user: root
    volumes:
      - /volume1/docker/wbo/wbo:/opt/app/server-data
    ports:
      - 9010:80
```

## jvmilazz0/kavita:latest
>  类似于komga的美漫日漫轻小说管理工具
> 
>  [使用说明](https://wiki.kavitareader.com/installation/docker/)
```
services:
  kavita:
    image: jvmilazz0/kavita:latest
    container_name: kavita
    network_mode: bridge
    restart: unless-stopped
    user: root
    ports:
      - 9025:5000
    volumes:
      - /volume1/readings:/manga
      - /volume1/readings:/comics
      - /volume1/readings:/books
      - /volume1/docker/kavita/config:/kavita/config
    environment:
      - TZ=Asia/Shanghai
```

## wukongdaily/box:latest
>  使用电脑、NAS等一切能运行docker的设备变成盒子的ADB安装助手，让你的安卓盒子用起来更加得心应手。
> 
>  [使用说明](https://github.com/wukongdaily/tvhelper-docker)
```
services:
  tvhelper:
    image: wukongdaily/box:latest
    container_name: tvhelper
    network_mode: bridge
    user: root
    restart: unless-stopped
    volumes:
      - /volume1/docker/tvhelper/apk:/data
    ports:
      - 9080:80
      - 9022:22
    environment:
      - PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/lib/android-sdk/platform-tools
```

## linuxserver/chromium:latest
>  尝试安装docker版的chromium浏览器，失败了，因为它强制了需要https访问，本地NAS没去搞证书，隔壁的firefox也是这个要求
> 
>  [使用说明](https://github.com/linuxserver/docker-chromium)
```
services:
  chromium:
    image: linuxserver/chromium:latest
    container_name: chromium
    network_mode: bridge
    user: root
    restart: unless-stopped
    shm_size: "1gb"
    security_opt:
      - seccomp:unconfined
    environment:
      - PUID=0
      - PGID=0
      - TZ=Asia/Shanghai
      - LC_ALL=zh_CN.UTF-8
    volumes:
      - /volume1/docker/chromium/config:/config
    ports:
      - 9011:3000
      - 9012:3001
    devices:
      - /dev/dri:/dev/dri
```

## johngong/anki-sync-server:latest
>  Anki的同步服务，没连接成功，AnkiDroid自定义同步服务器强制需要https
> 
>  [使用说明](https://hub.docker.com/r/johngong/anki-sync-server)
```
services:
  ankisync:
    image: johngong/anki-sync-server:latest
    container_name: ankisync
    network_mode: bridge
    user: root
    restart: unless-stopped
    environment:
      - SYNC_USER1=用户名:密码
      - UID=0
      - GID=0
      - TZ=Asia/Shanghai
      - MAX_SYNC_PAYLOAD_MEGS=2000
    volumes:
      - /volume1/docker/ankisync/syncdir:/ankisyncdir
    ports:
      - 9013:8080
```

## ghcr.io/luckyturtledev/anki
>  另一个大佬的Anki的同步服务，同样没连接成功，AnkiDroid自定义同步服务器强制需要https
> 
>  [使用说明](https://github.com/LuckyTurtleDev/docker-images/blob/main/dockerfiles/anki/README.md)
```
services:
  ankisync:
    image: ghcr.io/luckyturtledev/anki
    container_name: ankisync
    network_mode: bridge
    restart: unless-stopped
    environment:
      - SYNC_USER1=用户名:密码
      - UID=0
      - GID=0
      - MAX_SYNC_PAYLOAD_MEGS=2000
    volumes:
      - /volume1/docker/ankisync/syncdir:/data
    ports:
      - 9013:8080
```

## josh5/steam-headless:latest
>  容器内安装steam，体验类似于steamdeck，使用proton兼容层游玩游戏
> 
>  由于是N100装了群晖，在尝试特权模式失败后，采用了不带特权模式的compose文件，devices里把默认的card1改成了card0
>
>  同文件夹下还需要一个.env文件，shm_size改大一点，时区也改一改，底下的3个目录也改成实际的目录
> 
>  群晖估计大概率会有权限问题，索性直接把权限改成PUID=0，PGID=0，UMASK=022
> 
>  FORCE_X11_DUMMY_CONFIG改成了true，似乎与虚拟显示器有关
>
>  但是这样构建还是报错，提示/dev/uinput不存在，估计飞牛或者Unraid就没这个问题，索性直接删除/dev/uinput那一行，成功启动
>
>  steam启动后改中文会有乱码，先`sudo apt update`，然后`sudo apt install fonts-noto-cjk`安装中文字体
>
>  又发现sunshine的设置界面打不开，默认的firefox不知哪出了问题，索性直接安装esr版本的firefox
>
>  装完后去系统设置里，修改默认的应用程序为刚才安装的esr版本的firefox，成功打开浏览器
>
>  体验感觉并不是很好，核显还是太弱了，尝试游玩老游戏植物大战僵尸，CPU占用率从 12% 飙升到 79%，卡顿还是很明显的
>
>  估计要想体验好，还得有额外的独显才行，不过在容器里运行steam还真是一次有趣的尝试
> 
>  详细的[安装与使用说明](https://github.com/Steam-Headless/docker-steam-headless/blob/master/docs/docker-compose.md)
```
steamheadless 的 docker-compose.yml 内容：

services:
  steamheadless:
    image: josh5/steam-headless:latest
    container_name: steamheadless
    restart: unless-stopped
    shm_size: ${SHM_SIZE}
    ipc: host # Could also be set to 'shareable'
    ulimits:
      nofile:
        soft: 1024
        hard: 524288
    cap_add:
      - NET_ADMIN
      - SYS_ADMIN
      - SYS_NICE
    security_opt:
      - seccomp:unconfined
      - apparmor:unconfined
    network_mode: host
    hostname: ${NAME}
    extra_hosts:
      - "${NAME}:127.0.0.1"
    environment:
      - TZ=${TZ}
      - USER_LOCALES=${USER_LOCALES}
      - DISPLAY=${DISPLAY}
      - PUID=${PUID}
      - PGID=${PGID}
      - UMASK=${UMASK}
      - USER_PASSWORD=${USER_PASSWORD}
      - MODE=${MODE}
      - WEB_UI_MODE=${WEB_UI_MODE}
      - ENABLE_VNC_AUDIO=${ENABLE_VNC_AUDIO}
      - PORT_NOVNC_WEB=${PORT_NOVNC_WEB}
      - NEKO_NAT1TO1=${NEKO_NAT1TO1}
      - ENABLE_STEAM=${ENABLE_STEAM}
      - STEAM_ARGS=${STEAM_ARGS}
      - ENABLE_SUNSHINE=${ENABLE_SUNSHINE}
      - SUNSHINE_USER=${SUNSHINE_USER}
      - SUNSHINE_PASS=${SUNSHINE_PASS}
      - ENABLE_EVDEV_INPUTS=${ENABLE_EVDEV_INPUTS}
      - FORCE_X11_DUMMY_CONFIG=${FORCE_X11_DUMMY_CONFIG}
      - NVIDIA_DRIVER_CAPABILITIES=${NVIDIA_DRIVER_CAPABILITIES}
      - NVIDIA_VISIBLE_DEVICES=${NVIDIA_VISIBLE_DEVICES}
      - NVIDIA_DRIVER_VERSION=${NVIDIA_DRIVER_VERSION}
    devices:
      - /dev/fuse
      - /dev/dri/card0
      - /dev/dri/renderD128
    device_cgroup_rules:
      - 'c 13:* rmw'
    volumes:
      - ${HOME_DIR}/:/home/default/:rw
      - ${GAMES_DIR}/:/mnt/games/:rw
      - ${SHARED_SOCKETS_DIR}/.X11-unix/:/tmp/.X11-unix/:rw
      - ${SHARED_SOCKETS_DIR}/pulse/:/tmp/pulse/:rw
```
> .env 内容如下
```
NAME=SteamHeadless
TZ=TZ=Asia/Shanghai
USER_LOCALES=en_US.UTF-8 UTF-8
SHM_SIZE=8G
DISPLAY=:55
HOME_DIR=/volume1/docker/steamheadless/home
SHARED_SOCKETS_DIR=/volume1/docker/steamheadless/sockets
GAMES_DIR=/volume1/docker/steamheadless/games
PUID=0
PGID=0
UMASK=022
USER_PASSWORD=password
MODE=primary
WEB_UI_MODE=vnc
ENABLE_VNC_AUDIO=true
PORT_NOVNC_WEB=8083
NEKO_NAT1TO1=
ENABLE_STEAM=true
STEAM_ARGS=-silent
ENABLE_SUNSHINE=true
SUNSHINE_USER=admin
SUNSHINE_PASS=admin
ENABLE_EVDEV_INPUTS=true
FORCE_X11_DUMMY_CONFIG=true
NVIDIA_DRIVER_CAPABILITIES=all
NVIDIA_VISIBLE_DEVICES=all
NVIDIA_DRIVER_VERSION=
```


## szabis/iventoy:latest
>  docker部署PXE服务器，通过网络重装电脑系统
> 
>  [使用说明](https://hub.docker.com/r/szabis/iventoy)
```
services:
  iventoy:
    image: szabis/iventoy:latest
    container_name: iventoy
    network_mode: host
    restart: unless-stopped
    privileged: true
    user: root
    environment:
      - "67:67/udp" # DHCP Server
      - "69:69/udp" # TFTP Server
      - "10809:10809" # NBD Server (NBD)
      - "16000:16000" # PXE Service HTTP Server (iVentoy PXE Service)
      - "26000:26000" # PXE GUI HTTP Server (iVentoy GUI)
    volumes:
      - /volume1/docker/iventoy/data:/opt/iventoy/data
      - /volume1/docker/iventoy/iso:/opt/iventoy/iso
      - /volume1/docker/iventoy/log:/opt/iventoy/log
      - /volume1/docker/iventoy/user:/opt/iventoy/user
```


## xiaozhu674/gameservermanager:latest
>  B站用户"[又菜又爱玩的小朱猪](https://space.bilibili.com/401680975)"开发的，一个用于Steam上相关游戏开服的工具。
> 
>  目前支持50多款游戏，还支持MC。但是我部署下来，似乎好像有点bug，可能是映射或者权限问题，不知道怎么修复
> 
>  [使用说明](https://github.com/GSManagerXZ/GameServerManager)
```
services:
  gsmanager3:
    container_name: gsmanager3
    image: xiaozhu674/gameservermanager:latest
    privileged: true
    user: root
    network_mode: bridge
    restart: unless-stopped
    ports:
      - "9015:3001"
      - "27015:27015"
    volumes:
      - ./game_data:/home/.config
      - ./game_data:/home/.local
      - ./game_file:/home/steam/games
      - ./game_data:/root/.config
      - ./game_data:/root/.local
      - ./game_file:/root/steam/games
      - ./gsm3_data:/root/server/data
    environment:
      - TZ=Asia/Shanghai
      - SERVER_PORT=3001
    stdin_open: true
    tty: true
```


## githubyumao/mcsmanager-daemon:v10.6.0
>  比较有名的MC开服面板工具
>
>  网上的建议是局域网的话，拉取web:v10.6.1和daemon:v10.6.0，最新的latest强制只支持公网IP连接
>
>  新增节点后，密钥是在daemon的日志里查看
> 
>  [使用说明](https://docs.mcsmanager.com/zh_cn)
```
networks:
  default:
    name: mcsmanager

services:
  web:
    image: githubyumao/mcsmanager-web:v10.6.1
    container_name: mcsmanager-web
    ports:
      - "9018:23333"
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /volume1/docker/mcsmanager/web/data:/opt/mcsmanager/web/data
      - /volume1/docker/mcsmanager/web/logs:/opt/mcsmanager/web/logs
    networks:
      - default

  daemon:
    image: githubyumao/mcsmanager-daemon:v10.6.0
    container_name: mcsmanager-daemon
    restart: unless-stopped
    ports:
      - "9019:24444"
    environment:
      - MCSM_DOCKER_WORKSPACE_PATH=/volume1/docker/mcsmanager/daemon/data/InstanceData
    volumes:
      - /etc/localtime:/etc/localtime:ro
      - /volume1/docker/mcsmanager/daemon/data:/opt/mcsmanager/daemon/data
      - /volume1/docker/mcsmanager/daemon/logs:/opt/mcsmanager/daemon/logs
      - /var/run/docker.sock:/var/run/docker.sock
    networks:
      - default
```


## nextcloud:latest
>  非All-in-one方式安装Nextcloud，一般也用不上
> 
>  解决一个奇怪的笔记软件[Saber](https://saber.adil.hanney.org)的同步问题，它只支持Nextcloud同步
> 
>  [安装参考](https://www.bilibili.com/opus/828057484080971780)
```
networks:
  default:
    name: nextcloud

services:
  nextcloud:
    image: nextcloud:latest
    container_name: nextcloud
    restart: unless-stopped
    volumes:
      - /volume1/docker/nextcloud/app:/var/www/html
    environment:
      - MYSQL_PASSWORD=adminadmin
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_HOST=db
      - TZ=Asia/Shanghai
    ports:
      - 9016:80
    networks:
      - default

  cache:
    image: redis:latest
    container_name: nextcloud-redis
    restart: unless-stopped
    expose:
     - 6379
    volumes:
     - /volume1/docker/nextcloud/cache:/data
    command: redis-server --requirepass redis_password
    environment:
      - TZ=Asia/Shanghai
    networks:
      - default

  db:
    image: mariadb:latest
    container_name: nextcloud-mariadb
    restart: unless-stopped
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW --innodb-file-per-table=1 --skip-innodb-read-only-compressed
    volumes:
      - /volume1/docker/nextcloud/db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=admin
      - MYSQL_PASSWORD=adminadmin
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - TZ=Asia/Shanghai
    networks:
      - default
```


## yajuhua/podcast2:latest
>  将视频网站转换成播客订阅的一个服务
> 
>  [使用说明](https://github.com/yajuhua/podcast2)
```
services:
  podcast2:
    image: yajuhua/podcast2:latest
    container_name: podcast2
    restart: unless-stopped
    network_mode: bridge
    ports:
      - 9021:8088
    volumes:
      - ./data:/data
```


## ghcr.i0/moontechlab/lunatv:latest
>  一个vod视频聚合工具，空壳无订阅源
> 
>  [使用说明](https://github.c0m/MoonTechLab/LunaTV)
```
networks:
    default:
      name: moontv

services:
    moontv-core:
      image: ghcr.i0/moontechlab/lunatv:latest
      container_name: moontv-core
      restart: unless-stopped
      user: root
      ports:
        - '9025:3000'
      environment:
        - USERNAME=admin
        - PASSWORD=adminadmin
        - NEXT_PUBLIC_STORAGE_TYPE=kvrocks
        - KVROCKS_URL=redis://moontv-kvrocks:6666
      depends_on:
        - moontv-kvrocks
      networks:
        - default

    moontv-kvrocks:
      image: apache/kvrocks
      container_name: moontv-kvrocks
      restart: unless-stopped
      user: root
      volumes:
        - ./kvrocksdata:/var/lib/kvrocks
      networks:
        - default
```


## diygod/rsshub
>  rss订阅项目，几乎很多东西都能订阅
> 
>  [使用说明](https://docs.rsshub.app/zh/guide)
```
networks:
    default:
        name: rsshub

services:
    rsshub:
        image: diygod/rsshub
        container_name: rsshub
        restart: unless-stopped
        ports:
            - "9030:1200"
        environment:
            NODE_ENV: production
            CACHE_TYPE: redis
            REDIS_URL: "redis://redis:6379/"
            PUPPETEER_WS_ENDPOINT: "ws://browserless:3000"
        healthcheck:
            test: ["CMD", "curl", "-f", "http://localhost:1200/healthz"]
            interval: 30s
            timeout: 10s
            retries: 3
        depends_on:
            - redis
            - browserless
        networks:
            - default

    browserless:
        image: browserless/chrome
        container_name: rsshub_browserless
        restart: unless-stopped
        ulimits:
            core:
                hard: 0
                soft: 0
        healthcheck:
            test: ["CMD", "curl", "-f", "http://localhost:3000/pressure"]
            interval: 30s
            timeout: 10s
            retries: 3
        networks:
            - default

    redis:
        image: redis:alpine
        container_name: rsshub_redis
        restart: unless-stopped
        volumes:
            - ./redisdata:/data
        healthcheck:
            test: ["CMD", "redis-cli", "ping"]
            interval: 30s
            timeout: 10s
            retries: 5
            start_period: 5s
        networks:
            - default
```


## ghcr.io/imagegenius/immich:latest
>  一个开源的相册服务，支持识别人和物，以及地理位置相册，参考了初之音的[这篇文章](https://www.himiku.com/archives/immich.html)
>
>  国内则是mt photos，但是要付费，而且部署文档写的比较乱，就不部署了
> 
>  [使用说明](https://immich.app/docs/overview/welcome)
```
networks:
  default:
    name: immich

services:
  immich:
    image: ghcr.io/imagegenius/immich:latest
    container_name: immich
    environment:
      - PUID=${PUID}
      - PGID=${PGID}
      - TZ=${TZ}
      - DB_HOSTNAME=immich_database
      - DB_USERNAME=postgres
      - DB_PASSWORD=${DB_PASSWORD}
      - DB_DATABASE_NAME=immich
      - REDIS_HOSTNAME=immich_redis
      - DB_PORT=5432
      - REDIS_PORT=6379
      - REDIS_PASSWORD=
      - MACHINE_LEARNING_HOST=0.0.0.0
      - MACHINE_LEARNING_PORT=3003
      - MACHINE_LEARNING_WORKERS=1
      - MACHINE_LEARNING_WORKER_TIMEOUT=120
    volumes:
      - ./config:/config
      - ${PHOTOS_LOCATION}:/photos
      - ${IMPORT_LOCATION}:/import
      - ./geodata:/build/geodata
      - ./i18n-iso-countries/langs:/usr/src/app/server/node_modules/i18n-iso-countries/langs
    ports:
      - ${IMMICH_PORT}:8080
    devices:
      - /dev/dri:/dev/dri
    restart: unless-stopped
    networks:
      - default

  immich_redis:
    image: redis
    container_name: immich_redis
    restart: unless-stopped
    networks:
      - default

  immich_database:
    image: ghcr.io/immich-app/postgres:14-vectorchord0.3.0-pgvectors0.2.0
    container_name: immich_database
    user: ${PUID}:${PGID}
    environment:
      - TZ=${TZ}
      - POSTGRES_PASSWORD=${DB_PASSWORD}
      - POSTGRES_USER=postgres
      - POSTGRES_DB=immich
    volumes:
      - ./database:/var/lib/postgresql/data
    restart: unless-stopped
    networks:
      - default
```
>  .env内容如下
```
IMMICH_PORT=9020
PHOTOS_LOCATION=./photos
IMPORT_LOCATION=/volume1/Pictures
PUID=0
PGID=0
TZ=Asia/Shanghai
DB_PASSWORD=immich
```

## couchdb:latest
>  给 MoonFM 配置`couchdb`同步
> 
>  参考了这篇[博客文章](https://www.whrr.cc/article/how-to-set-MoonFM-sync)
>
>  以及这篇[知乎文章](https://zhuanlan.zhihu.com/p/645030276)
> 
>  按照知乎文章配置`local.ini`后，终端里面可以少输入下面的命令，因为`_users`数据库已经生成了
> 
>  `curl -X PUT http://admin:password@IP:端口号/_users -H "Accept: application/json" -H "Content-Type: application/json"`
>  
>  终端里输入以下命令来产生一个`userdb_xxxxxxxx`的数据库
>  
>  `curl -X PUT http://admin:password@ip:端口/_users/org.couchdb.user:admin -H "Accept: application/json" -H "Content-Type: application/json" -d '{"name": "admin", "password": "password", "roles": [], "type": "user"}'`
> 
>  注意最后的`userdb_xxxxxxxx`的中间是横杠`-`还是下划线`_`，新版的应该是下划线
```
services:
  couchdb:
    container_name: couchdb
    image: couchdb:latest
    user: root
    network_mode: bridge
    restart: unless-stopped
    environment:
      - COUCHDB_USER=admin
      - COUCHDB_PASSWORD=password
    volumes:
      - /volume1/docker/couchdb/data:/opt/couchdb/data
      - /volume1/docker/couchdb/data/local.ini:/opt/couchdb/etc/local.ini
    ports:
      - 5984:5984
```
>  `local.ini`内容如下，参考了上面那篇知乎文章
```
[couchdb]
single_node=true

[chttpd]
require_valid_user = true

[chttpd_auth]
require_valid_user = true
authentication_redirect = /_utils/session.html

[httpd]
WWW-Authenticate = Basic realm="couchdb"
enable_cors = true

[cors]
origins = app://obsidian.md,capacitor://localhost,http://localhost
credentials = true
headers = accept, authorization, content-type, origin, referer
methods = GET, PUT, POST, HEAD, DELETE
max_age = 3600

[couch_peruser]
database_prefix = userdb_
delete_dbs = false
enable = true
```

## ghcr.io/katelya77/katelyatv:latest
>  M00nTV二次开发的影视聚合平台
> 
>  [使用说明](https://github.com/katelya77/KatelyaTV?tab=readme-ov-file)
```
networks:
  default:
    name: katelyatv

services:
  katelyatv:
    image: ghcr.io/katelya77/katelyatv:latest
    container_name: katelyatv
    restart: unless-stopped
    ports:
      - "9028:3000"
    environment:
      NEXT_PUBLIC_STORAGE_TYPE: redis
      REDIS_URL: redis://katelyatv-redis:6379
      REDIS_PASSWORD: ${REDIS_PASSWORD:-}
      REDIS_DATABASE: 0
      USERNAME: admin
      AUTH_PASSWORD: password
      NEXTAUTH_SECRET: ${NEXTAUTH_SECRET}
      NEXTAUTH_URL: ${NEXTAUTH_URL:-http://localhost:3000}
    depends_on:
      - katelyatv-redis
    networks:
      - default

  katelyatv-redis:
    image: redis:7-alpine
    container_name: katelyatv-redis
    restart: unless-stopped
    command: redis-server --appendonly yes --maxmemory 256mb --maxmemory-policy allkeys-lru
    volumes:
      - ./katelyatv-redis-data:/data
    networks:
      - default
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 10s
```
>  .env 文件内容如下
```
NEXT_PUBLIC_STORAGE_TYPE=redis
REDIS_URL=redis://katelyatv-redis:6379
REDIS_DATABASE=0
NEXTAUTH_SECRET=your_nextauth_secret_here
NEXTAUTH_URL=http://localhost:3000
NEXT_PUBLIC_SITE_NAME=KatelyaTV
NEXT_PUBLIC_SITE_DESCRIPTION=高性能影视播放平台
NODE_ENV=production
PORT=3000
DOCKER_IMAGE_TAG=latest
IMAGE_PROXY_ENABLED=true
CACHE_TTL=3600
CORS_ORIGIN=*
RATE_LIMIT_MAX=100
RATE_LIMIT_WINDOW=60000
HEALTH_CHECK_ENABLED=true
HEALTH_CHECK_INTERVAL=30
LOG_LEVEL=info
LOG_FORMAT=json
```
## neosmemo/memos:0.21.0
>  InkRoot，对于0.21.0特别优化的一个第三方memos客户端
> 
>  [使用说明](https://github.com/yyyyymmmmm/IntRoot)
```
services:
  inkroot:
    image: neosmemo/memos:0.21.0
    container_name: inkroot
    network_mode: bridge
    restart: unless-stopped
    volumes:
      - /volume1/docker/inkroot/memos:/var/opt/memos
    ports:
      - 9009:5230
```

## dko0/squoosh:latest
>  谷歌开源的图片压缩工具的docker版本
```
services:
  squoosh:
    image: dko0/squoosh:latest
    container_name: squoosh
    restart: unless-stopped
    network_mode: bridge
    ports:
      - 9035:8080
```

## jiangrui1994/cloudsaver:latest
>  一个网盘资源搜索与转存工具
> 
>  [使用说明](https://github.com/jiangrui1994/CloudSaver)
```
services:
  cloudsaver:
    image: jiangrui1994/cloudsaver:latest
    container_name: cloudsaver
    restart: unless-stopped
    network_mode: bridge
    ports:
      - "9031:8008"
    volumes:
      - /volume1/docker/cloudsaver/data:/app/data
      - /volume1/docker/cloudsaver/config:/app/config
```

## ghcr.io/fish2018/pansou-web:latest
>  带前后端的网盘资源搜索工具
> 
>  [使用说明](https://github.com/fish2018/pansou-web)
```
services:
  pansou:
    image: ghcr.io/fish2018/pansou-web:latest
    container_name: pansou
    restart: unless-stopped
    network_mode: bridge
    ports:
      - "9050:80"
    environment:
      - DOMAIN=localhost
      - PANSOU_PORT=8888
      - PANSOU_HOST=127.0.0.1
      - ENABLED_PLUGINS=labi,zhizhen,shandian,duoduo,muou,wanou
    volumes:
      - /volume1/docker/pansou/data:/app/data
      - /volume1/docker/pansou/logs:/app/logs
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost/api/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
```

## wu529778790/panhub.shenzjd.com:latest
>  一个简约的网盘资源搜索工具
> 
>  [使用说明](https://github.com/wu529778790/panhub.shenzjd.com)
```
services:
  panhub:
    image: wu529778790/panhub.shenzjd.com:latest
    container_name: panhub
    restart: unless-stopped
    network_mode: bridge
    ports:
      - 9032:3000
```

## dockpeek/dockpeek:latest
>  查看docker部署在哪些端口的工具
>  
>  实测并不能看到没有启动的容器的端口，只能看那些已经启动的容器
> 
>  [使用说明](https://github.com/dockpeek/dockpeek)
```
services:
  dockpeek:
    image: dockpeek/dockpeek:latest
    container_name: dockpeek
    restart: unless-stopped
    network_mode: bridge
    privileged: true
    environment:
      - SECRET_KEY=password
      - USERNAME=admin
      - PASSWORD=password
    ports:
      - "9060:8000"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```

## dr34m/tao-sync:latest
>  一个用于Alist/Openlist之间自动化同步的工具
> 
>  [使用说明](https://github.com/dr34m-cn/taosync)
```
services:
  taosync:
    image: dr34m/tao-sync:latest
    container_name: taosync
    restart: unless-stopped
    network_mode: bridge
    ports:
      - 9051:8023
    volumes:
      - /volume1/docker/taosync/data:/app/data
```

## hslr/sun-panel:latest
>  一款NAS服务器的导航面板
> 
>  [使用说明](https://github.com/hslr-s/sun-panel)
```
services:
  sunpanel:
    image: hslr/sun-panel:latest
    container_name: sunpanel
    restart: unless-stopped
    network_mode: bridge
    volumes:
      - /volume1/docker/sunpanel/conf:/app/conf
    ports:
      - 9055:3002
```

## jgraph/drawio:latest
>  一款开源绘图工具，用于流程图建模、经济分析图、系统结构图与学术演示
> 
>  [使用说明](https://www.drawio.com)
```
services:
  drawio:
    image: jgraph/drawio:latest
    container_name: drawio
    restart: unless-stopped
    network_mode: bridge
    ports:
      - 9052:8080
```

## doocs/md:latest
>  一款高度简洁的微信 Markdown 编辑器
> 
>  [使用说明](https://github.com/doocs/md)
```
services:
  doocs:
    image: doocs/md:latest
    container_name: doocs
    restart: unless-stopped
    network_mode: bridge
    ports:
      - 9053:80
```

## surveyking/surveyking:latest
>  卷王问卷考试系统，用来发布和回答问卷的工具
> 
>  [使用说明](https://surveyking.cn/open-source/quickstart)
```
services:
  surveyking:
    image: surveyking/surveyking:latest
    container_name: surveyking
    restart: unless-stopped
    network_mode: bridge
    volumes:
      - /volume1/docker/surveyking/files:/app/files
      - /volume1/docker/surveyking/logs:/app/logs
    ports:
      - 9056:1991
```

## b3log/siyuan:latest
>  思源笔记docker版本
> 
>  不支持桌面端和移动端应用连接，仅支持在浏览器上使用，不支持导出 PDF、HTML 和 Word 格式，不支持导入 Markdown 文件
> 
>  [使用说明](https://github.com/siyuan-note/siyuan/blob/master/README_zh_CN.md)
```
services:
  siyuan:
    image: b3log/siyuan:latest
    restart: unless-stopped
    user: root
    container_name: siyuan
    network_mode: bridge
    ports:
      - "9070:6806"
    volumes:
      - /volume1/docker/siyuan/workspace:/siyuan/workspace
    command: --workspace=/siyuan/workspace --accessAuthCode=password --lang=zh_CN
```
