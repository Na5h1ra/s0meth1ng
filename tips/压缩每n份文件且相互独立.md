��1����
DIR /B >> listfile.txt
���Ŀ¼�������ļ�


��2����
TXTKiller���߱���ı����,�ָ�listfile.txtΪlistfile_1.txt,listfile_2.txtֱ��listfile_%i.txt


��3����
����7zip�������
���磺https://documentation.help/7-Zip/start.htm

"7z a -tzip archive.zip @listfile.txt -mx9 -mmt=8 -m0=LZMA:d=25 -ppassword
��Ϊ����listfile.txt��ָ�����ļ���ӽ�archive.zip�У��Զ�����zip�ļ������趨���ѹ��ģʽ��CPU�߳���Ϊ8����һ�㷨ΪLZMA�㷨���ֵ��СΪ32MB���趨����Ϊpassword"

��Դ��https://www.zhihu.com/question/379054502/answer/1077926871


��4����
����forѭ���������
���磺https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/for
�Լ���https://ss64.com/nt/for.html

for /L %[variable] in ([start],[step],[stop]) do [command]


��5����
д���������
��ѹ��5000���ļ������ѹ��ģʽΪ������5000���ļ����ļ���д��listfile.txt����ÿ100�зָ��50��listfile_%i.txt��%iΪ��ţ��ļ���

��for /L %i in (1,1,50) do 7z a -tzip archive_%i.zip @listfile_%i.txt -mx9 -mmt=8 -m0=LZMA:d=27 -psecret��

��Դ��https://www.zhihu.com/question/379054502/answer/1077926871