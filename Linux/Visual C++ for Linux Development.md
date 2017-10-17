# Visual C++ for Linux Development

Visual Studio로 리눅스 원격 디버깅이 가능함.

아래 명령어로 include파일을 로컬로 복사한 후 사용하면 Intellisense도 사용할 수 있음.
```
pscp -r root@192.168.0.90:/usr/include ./include
```

Include파일을 복사한 후 프로젝트 속성 -> VC++ Directories -> Include Directories에 $(MSBuildProjectDirectory)\Include 를 추가한다.
