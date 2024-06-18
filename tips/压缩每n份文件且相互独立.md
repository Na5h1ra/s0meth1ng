## 第1步
  右键打开Powershell，输入命令： cmd /r dir /b >listfile.txt 输出目录下所有文件
## 第2步
  TXTKiller或者别的文本软件,分割listfile.txt为listfile_1.txt,listfile_2.txt直到listfile_%i.txt

## 第3步
  查找7zip相关命令 例如：[https://documentation.help/7-Zip/start.htm](https://documentation.help/7-Zip/start.htm)

  7z a -tzip archive.zip @listfile.txt -mx9 -mmt=8 -m0=LZMA:d=25 -ppassword 意为：将listfile.txt中指定的文件添加进archive.zip中（自动创建zip文件），设定最高压缩模式，CPU线程数为8，第一算法为LZMA算法，字典大小为32MB，设定密码为password

## 第4步
  查找for循环相关命令 例如：[https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/for](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/for) 以及：[https://ss64.com/nt/for.html](https://ss64.com/nt/for.html)

  for /L %[variable] in ([start],[step],[stop]) do [command]

## 第5步
 写出相关命令 以压缩5000份文件，最高压缩模式为例，这5000份文件的文件名写入listfile.txt并按每100行分割成50份listfile_%i.txt（%i为序号）文件。

for /L %i in (1,1,50) do 7z a -tzip archive_%i.zip @listfile_%i.txt -mx9 -mmt=8 -m0=LZMA:d=27 -psecret

### 来源：[知乎](https://www.zhihu.com/question/379054502/answer/1077926871)
