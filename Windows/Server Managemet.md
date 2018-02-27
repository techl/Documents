# Server Management

## Time Sync

시간동기화 동작 여부 확인
> w32tm /resync

현재 설정 정보
> w32tm /query / configuration

시간동기화 서버 변경
> w32tm /config /manualpeerlist:"time.windows.com,0x9" /syncfromflags:MANUAL

시간동기화 서비스 재시작
> net stop w32time
> net start w32time

시간동기화 실행
> w32tm /resync

참고 : http://blog.daum.net/jungsangun/7691206