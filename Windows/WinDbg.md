### How to use WinDbg 

SRV*c:\symbols*http://msdl.microsoft.com/download/symbols

.loadby sos clr

!dumpheap -stat -live

!threads

!address -summary // all memory usage

!eeheap -gc // Gc heap size

!heap -s // heap list, heap �ּҸ� Ȯ�� 00270000

!heap -stat -h 0 //����߿� �ּҰ� 00270000�� ���� ã��.

!heap -flt s 210690 // 210690������ �˻�

dc 1ca20018 L 2000 // HEAP_ENTRY 1ca20018, 2000�� ������ �б�

#### ����
- http://kate-butenko.blogspot.kr/2012/07/investigating-issues-with-unmanaged.html