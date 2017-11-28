### How to use WinDbg 

SRV*c:\symbols*http://msdl.microsoft.com/download/symbols

.loadby sos clr

!dumpheap -stat -live

!threads

!address -summary // all memory usage

!eeheap -gc // Gc heap size

!heap -s // heap list, heap 주소를 확인 00270000

!heap -stat -h 0 //목록중에 주소가 00270000인 것을 찾음.

!heap -flt s 210690 // 210690사이즈 검색

dc 1ca20018 L 2000 // HEAP_ENTRY 1ca20018, 2000개 데이터 읽기

#### 참고
- http://kate-butenko.blogspot.kr/2012/07/investigating-issues-with-unmanaged.html