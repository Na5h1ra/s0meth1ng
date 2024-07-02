# Docker

> 自用Docker安装命令
>> 用于群晖和N1盒子。
>> 
>> N1盒子使用root权限登录，命令行安装，默认网络模式是bridge。
>> 
>> 群晖需要考虑权限问题,可添加privileged: true，user: root等命令。


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
