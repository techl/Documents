# Remote Desktop Connection 접속 기록 지우기

Command Prompt창 열고 다음 실행

> reg delete "HKEY_CURRENT_USER\Software\Microsoft\Terminal Server Client\Default" /va /f

Reference : http://woshub.com/how-to-clear-rdp-connections-history/
