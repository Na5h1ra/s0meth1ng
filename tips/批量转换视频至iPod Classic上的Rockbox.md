ffmpeg�ĵ���https://ffmpeg.org/ffmpeg.html
iPod Classic��Rockbox�ĵ���https://download.rockbox.org/release/3.15/rockbox-ipod6g-3.15.pdf
iPod Classic���ܣ�https://en.wikipedia.org/wiki/IPod_classic


iPod Classic��Rockbox���Mpeg Player plugin���ܣ� "The Mpeg Player is a video player plugin capable of playing back MPEG-1 and MPEG-2"
video streams with MPEG audio multiplexed into .mpg files.

iPod Classic 6th gen�� "The iPod Classic has a 2.5" backlit display at a resolution of 320��240."




����flv�ļ�ת��ΪRockbox֧�ֵ�mpeg��Ƶ��ʽ������Ϊ��
ffmpeg -i input.flv -s 320x180 -vcodec mpeg2video -b:a 192k -ac 2 -ar 44100 -acodec mp3 output.mpg 
 
����ת���ļ����µ�flvΪmpeg��Ƶ������Ϊ
for %%i in (.\*.flv) do ffmpeg -i "%%i" -s 320x180 -vcodec mpeg2video -b:v 320k -b:a 192k -ac 2 -ar 44100 -acodec mp3 "%%~dpni.mpg"