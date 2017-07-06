# Windows 초기 설정

## User Folder 위치 변경

탐색기에서 c:\Users\{UserID} 폴더로 이동하여 모든 폴더를 각각 오른쪽 클릭후 Location을 바꿔준다. C드라이브에 저장하지 않도록 하기 위함이다.


## 윈도우 구성 요소 추가 설치

IIS, Hyper-V with WebSocket Protocol

Telnet Client

Hyper-V에서 New Virtual Switch 추가

IP, MAC 설정


## 초기 설정

Edge Pin제거 후 Internet Explorer pin 설정. 

IE설정에서 New Tab 사용. ​Favorites Bar 보이기. 기본 검색 엔진을 Google로 설정.

Google에서 검색 결과 새창에 띄우기 설정

Taskbar 설정 - Combine when taskbar full

Explorer View Options View -> Show hidden files, uncheck Hide extensions for known types

Remote Desktop

Power Options에서 Sleep들어가지 않도록 설정

Taskbar의 Jump List 수 증대 - 설정 후 바로 적용된다.

> REG ADD HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced /t REG_DWORD /v JumpListItems_Maximum /d 20


## 초기 설치 프로그램

* notepad++
* Office
* SQL
* Visual Studio & update
* Visual Studio Code
* bandizip.com


## Outlook 기본 설정

#### 기본 폴더 위치 변경

REG ADD HKCU\Software\Microsoft\Office\16.0\Outlook /t REG_EXPAND_SZ /v ForcePSTPath /d d:\Documents\Mail

REG ADD HKCU\Software\Microsoft\Office\16.0\Outlook /t REG_EXPAND_SZ /v ForceOSTPath /d d:\Documents\Mail

#### 발송 지연 1분 설정 - 잘못 보냈을 경우 취소하기 위함

Rules -> Manage Rules -> New Rule -> Start from a blank rule -> Apply rule on messages I send -> defer delivery by 1 minutes
