ffmpeg文档：https://ffmpeg.org/ffmpeg.html
iPod Classic的Rockbox文档：https://download.rockbox.org/release/3.15/rockbox-ipod6g-3.15.pdf
iPod Classic介绍：https://en.wikipedia.org/wiki/IPod_classic


iPod Classic的Rockbox里的Mpeg Player plugin介绍：https://www.rockbox.org/wiki/PluginMpegplayer

"The Mpeg Player is a video player plugin capable of playing back MPEG-1 and MPEG-2"
video streams with MPEG audio multiplexed into .mpg files.

iPod Classic 6th gen： "The iPod Classic has a 2.5" backlit display at a resolution of 320×240."




单个flv文件转码为Rockbox支持的mpeg视频，代码为：
ffmpeg -i input.flv -s 320x180 -vcodec mpeg2video -b:v 320k -b:a 192k -ac 2 -ar 44100 -acodec mp3 output.mpg 

批量转换文件夹下的flv为mpeg视频，代码为
for %%i in (.\*.flv) do ffmpeg -i "%%i" -s 320x180 -vcodec mpeg2video -b:v 320k -b:a 192k -ac 2 -ar 44100 -acodec mp3 "%%~dpni.mpg"
