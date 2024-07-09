# Docker

> 自用Docker安装命令
>> 用于群晖和N1盒子。
>> 
>> N1盒子使用root权限登录，命令行安装，默认网络模式是bridge。
>> 
>> 群晖需要考虑权限问题,可添加privileged: true，user: root等命令。网络需要指定network_mode: bridge或者host，否则会创建新的桥接网络。


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
