## Windows Server 2016 UEFI 설치

아래 스크립트로 USB를 만든다.

출처 : https://gist.github.com/p0w3rsh3ll/9106e3dc1bd2023ee5afd8cd85054613

WS2016-UEFI-USB-boot-stick.ps1 
``` 
# minimum size of USB stick 5.29GB

# Set here the path of your ISO file
$iso = 'D:\Backup\Msdn\os\en_windows_server_2016_x64_dvd_9718492.iso'

# Clean ! will clear any plugged-in USB stick!!
Get-Disk | Where BusType -eq 'USB' | 
Clear-Disk -RemoveData -Confirm:$true -PassThru

# Convert GPT
if ((Get-Disk | Where BusType -eq 'USB').PartitionStyle -eq 'RAW') {
    Get-Disk | Where BusType -eq 'USB' | 
    Initialize-Disk -PartitionStyle GPT
} else {
    Get-Disk | Where BusType -eq 'USB' | 
    Set-Disk -PartitionStyle GPT
}

# Create partition primary and format to FAT32
$volume = Get-Disk | Where BusType -eq 'USB' | 
New-Partition -UseMaximumSize -AssignDriveLetter | 
Format-Volume -FileSystem FAT32

if (Test-Path -Path "$($volume.DriveLetter):\") {

    # Mount iso
    $miso = Mount-DiskImage -ImagePath $iso -StorageType ISO -PassThru

    # Driver letter
    $dl = ($miso | Get-Volume).DriveLetter
}

if (Test-Path -Path "$($dl):\sources\install.wim") {

    # Copy ISO content to USB except install.wim
    & (Get-Command "$($env:systemroot)\system32\robocopy.exe") @(
        "$($dl):\",
        "$($volume.DriveLetter):\"
        ,'/S','/R:0','/Z','/XF','install.wim','/NP'
    )

    # Split install.wim
    & (Get-Command "$($env:systemroot)\system32\dism.exe") @(
        '/split-image',
        "/imagefile:$($dl):\sources\install.wim",
        "/SWMFile:$($volume.DriveLetter):\sources\install.swm",
        '/FileSize:4096'
    )
}

# Eject USB
(New-Object -comObject Shell.Application).NameSpace(17).
ParseName("$($volume.DriveLetter):").InvokeVerb('Eject')

# Dismount ISO
Dismount-DiskImage -ImagePath $iso

```

만약 Execution Policy문제로 실행이 안되면 다음 명령어를 실행해준다.

- Set-ExecutionPolicy Unrestricted


## Windows Server 2016 설정

### Server Manager

Local Server

- IE Enhanced Security Configuration : Administrators Off, Users On


Remote Desktop 설정

방화벽
- Remote Desktop 예외.
- Ping 되도록 설정


DDNS 설정 dnszi.com 참고

IIS 설치
- Install-WindowsFeature -name Web-Server -IncludeManagementTools
- IIS Manager는 Server Manager 통해서 실행
- 설치 옵션에서 Windows Authentication을 추가

### 설치 프로그램

- FileZilla
- Air Video Server HD
    - VLC
- [ServeToMe](https://www.zqueue.com/servetome/)
- iTunes
- [eMule](http://www.emule-project.net/home/perl/general.cgi?l=1&rm=download)
- uTorrent
- JRiver Media Center
- OneDrive
    설치 후 Context Menu가 안나올 경우 OneDriveSetup.exe /allusers로 설치한다.
    
