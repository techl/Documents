# Server Management

## Time Sync

�ð�����ȭ ���� ���� Ȯ��
> w32tm /resync

���� ���� ����
> w32tm /query / configuration

�ð�����ȭ ���� ����
> w32tm /config /manualpeerlist:"time.windows.com,0x9" /syncfromflags:MANUAL

�ð�����ȭ ���� �����
> net stop w32time
> net start w32time

�ð�����ȭ ����
> w32tm /resync

���� : http://blog.daum.net/jungsangun/7691206