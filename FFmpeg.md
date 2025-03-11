# FFmpeg自用命令

## 更新时间 2025.03.11

## 1.iPod相关
  见[这篇文章](https://github.com/Na5h1ra/s0meth1ng/blob/main/tips/iPodClassic.md)
## 2.音视频提取与转换
### 2.1 批量切割片头片尾
网上找到的bat代码，设置好片头片尾长度即可
```
@echo off & setlocal enabledelayedexpansion

rem ===================需手动设置===================
rem 设定片头片尾长度，格式为 HH:mm:ss.fff
set "s1=00:01:01.0"
set "s2=00:01:00.0"
rem ================================================

for /f "tokens=1-4delims=:." %%a in ("%s2%") do (
    set /a "t2=(1%%a %% 100 *3600 + 1%%b %% 100 * 60 + 1%%c %% 100) * 1000 + 1%%d %% 1000"
)

md myvideo 2>nul
for %%i in (*.avi *.mkv *.mp4 *.flv) do (
    for /f "tokens=2-5delims=:., " %%a in ('ffmpeg -i "%%i" 2^>^&1 ^| find "Duration:"') do (
        set /a "t=(1%%a%%100*3600+1%%b%%100*60+1%%c%%100)*1000+1%%d0%%1000,t-=t2,ms=t%%1000,t/=1000"
        set /a h=t/3600,m=t%%3600/60,s=t%%60,h+=100,m+=100,s+=100,ms+=1000
        set "t=!h:~1!:!m:~1!:!s:~1!.!ms:~1!"
        ffmpeg -ss !s1! -to !t! -accurate_seek -i "%%i"  -c copy -avoid_negative_ts 1 "myvideo\%%i" -y
    )
)
pause
```


### 2.2 批量提取视频中的音频
通常是aac，`-vn`表示不输出视频，`-c:a copy`表示不重新编码直接复制源文件的音频流，其bat代码为
```
for %%i in (.\*.mp4) do ffmpeg -i "%%i" -vn -c:a copy "%%~dpni.aac"
```


### 2.3 批量转换音频文件的格式

如此处批量将aac音频文件，转换为比特率192kbps，采样频率为44100Hz，双声道的有损mp3音频文件，其bat代码为
```
for %%i in (.\*.aac) do ffmpeg -i "%%i" -codec:a libmp3lame -b:a 192k -ar 44100 -ac 2 "%%~dpni.mp3"
```
