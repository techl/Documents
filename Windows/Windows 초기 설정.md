﻿# Windows 초기 설정

## User Folder 위치 변경

탐색기에서 c:\Users\{UserID} 폴더로 이동하여 모든 폴더를 각각 오른쪽 클릭후 Location을 바꿔준다. C드라이브에 저장하지 않도록 하기 위함이다.

OneDrive 동기화 폴더 설정

## 윈도우 구성 요소 추가 설치

IIS with WebSocket Protocol

Hyper-V
- Enable-WindowsOptionalFeature -Online -FeatureName:Microsoft-Hyper-V -All


Telnet Client

Hyper-V에서 New Virtual Switch 추가

IP, MAC 설정

Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux

- 이후 Store에서 Ubuntu 설치

Use Developer Features 메뉴에서 Developer mode 선택

## 초기 설정

Computer Name 설정

Taskbar Settings

- Combine taskbar buttons = When taskbar is full
- Show taskbar buttons on = Taskbar where window is open
- Combine buttons on other taskbars = When taskbar is full

Edge Pin제거 후 Internet Explorer pin 설정. 

IE설정에서 Homepage를 about:Tabs로 설정. ​Favorites Bar 보이기. 기본 검색 엔진을 Google로 설정.

Google에서 검색 결과 새창에 띄우기 설정

Explorer View Options View -> Show hidden files, uncheck Hide extensions for known types

Remote Desktop

Power Options에서 Sleep들어가지 않도록 설정

Taskbar의 Jump List 수 증대 - 설정 후 바로 적용된다.

> REG ADD HKCU\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced /t REG_DWORD /v JumpListItems_Maximum /d 20

Snap Assist 끄기

- Multitasking Settings에서 "When I snap a window, show what I can snap next to it" Off

Keyboard Setting

- Region & language settings -> Prefered language -> 한국어 위로

Language for non-Unicode programs

- Region & language settings -> Additional date, time & regional settings -> Region -> Administrative -> Language for non-Unicode programs -> Change system locale...

WebDAV 크기 설정

- 1-> 2
> REG ADD HKLM\SYSTEM\CurrentControlSet\Services\WebClient\Parameters /t REG_DWORD /v BasicAuthLevel /d 2
- 50 MB -> 4GB
> REG ADD HKLM\SYSTEM\CurrentControlSet\Services\WebClient\Parameters /t REG_DWORD /v FileSizeLimitInBytes /d 4294967295

For use Windows PowerShell, you have to run below command

```
set-executionpolicy remotesigned
```

예전 SMB 접속을 위한 설정
```
reg add HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\LanmanWorkstation /v AllowInsecureGuestAuth /t REG_DWORD /d 1 /f
```

## 초기 설치 프로그램

* Visual Studio 2015 & Update 3 - NetMF용
* [ThinkPad USB Keyboard with TrakPoint Driver(55Y9025)](https://support.lenovo.com/kr/ko/solutions/migr-73183)
* [KakaoTalk](http://www.kakao.com/talk/)
  * Setting -> Alerts -> Pop-up -> Show : None
* [Slack](https://slack.com/downloads/windows)
* [notepad++](https://notepad-plus-plus.org/download)
* Office 2016
  * Outlook 설정
  * Word, Excel pin to taskbar
  * Project, Visio 설치
  * [Language Accessory Pack Korean](https://support.office.com/en-us/article/Language-Accessory-Pack-for-Office-82ee1236-0f9a-45ee-9c72-05b026ee809f)
* [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms) - pin to start
* Visual Studio 2017 & Update
  * Extensions
    * Web Essetials 2017
    * MonoRemoteDebugger
    * Code Compare
    * Microsoft Visual Studio 2017 Installer Projects
    * Productivity Power Tools VS2017
* [Visual Studio Code](https://code.visualstudio.com/)
* [Bandizip](http://bandizip.com)
  * Settings -> Extraction -> Uncheck *Do not close the progress window after extracting*
  * Settings -> Compression -> Uncheck *Do not close the progress window after archiving*

* putty : pin to start 설정
* [Rufus](https://rufus.akeo.ie/)
* [DWG TrueView - AutoCAD Viewer](https://www.autodesk.com/products/dwg/viewers#)
* Altium Designer Viewer
* 한글 Viewer
* [OrCAD PCB Designer Lite](http://www.orcad.com/resources/orcad-downloads)
* MDK Lite
* [AIMP mp3 player](http://www.aimp.ru/)
* GNU ARM Embedded Toolchain(https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads)
* [.Net Micro Framework](https://github.com/NETMF/netmf-interpreter/releases)
* [Intel RST](https://downloadcenter.intel.com/download/26865/Intel-Rapid-Storage-Technology-Intel-RST-?product=55005)
* Acrobat
  * SharePoint function disable
    > REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Adobe\Adobe Acrobat\11.0\FeatureLockDown\cSharePoint" /v bDisableSharePointFeatures /t REG_DWORD /d 1
  * Disable the confirmation dialog in the Preferences
    > REG ADD "HKCU\SOFTWARE\Adobe\Adobe Acrobat\11.0\Accessibility" /t REG_DWORD /v bCheckReadMode /d 0
  * Ctrl + K -> Reading -> Screen Reader Options -> Only read the currently visible pages, uncheck Confirm before tagging documents
* Adobe Reader
  * SharePoint function disable
    > REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Adobe\Acrobat Reader\DC\FeatureLockDown\cSharePoint" /v bDisableSharePointFeatures /t REG_DWORD /d 1
* [PADS Viewer](https://www.pads.com/downloads/pads-pcb-viewer/)

## Outlook 기본 설정

### 기본 폴더 위치 변경

REG ADD HKCU\Software\Microsoft\Office\16.0\Outlook /t REG_EXPAND_SZ /v ForcePSTPath /d d:\Documents\Mail

REG ADD HKCU\Software\Microsoft\Office\16.0\Outlook /t REG_EXPAND_SZ /v ForceOSTPath /d d:\Documents\Mail

### 발송 지연 1분 설정 - 잘못 보냈을 경우 취소하기 위함

Rules -> Manage Rules -> New Rule -> Start from a blank rule -> Apply rule on messages I send -> defer delivery by 1 minutes

### 기타 설정

Outlook Options -> Mail -> Replies and forwards -> Open replies and forwards in a new window 체크

Outlook Options -> Mail -> Message arrival -> Uncheck Display a Desktop Alert

Signature 설정

## 기타

불필요한 Context Menu 항목 지우기

HKCR\*\shellex\ContextMenuHandlers 에서 필요없는 Key를 삭제하면 됨.

> reg DELETE HKCR\*\shellex\ContextMenuHandlers\Adobe.Acrobat.ContextMenu


Microsoft Compatibility Telemetry 끄기

- 가끔 CPU를 높게 사용하므로 끄는게 좋다.
- Diagnostics & feedback 메뉴에서 Feeback frequency를 Never로 변경.
- 아레와 같이 Registry 추가

> Reg ADD HKLM\SOFTWARE\Policies\Microsoft\Windows\DataCollection /t REG_DWORD /v AllowTelemetry /d 0

- 이후 재부팅.