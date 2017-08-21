## Windows Server 2016 UEFI ��ġ

�Ʒ� ��ũ��Ʈ�� USB�� �����.

��ó : https://gist.github.com/p0w3rsh3ll/9106e3dc1bd2023ee5afd8cd85054613

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

���� Execution Policy������ ������ �ȵǸ� ���� ��ɾ �������ش�.

- Set-ExecutionPolicy Unrestricted


## Windows Server 2016 ����

### Server Manager

Local Server

- IE Enhanced Security Configuration : Administrators Off, Users On


Remote Desktop ����

��ȭ��
- Remote Desktop ����.
- Ping �ǵ��� ����


DDNS ���� dnszi.com ����

IIS ��ġ
- Install-WindowsFeature -name Web-Server -IncludeManagementTools
- IIS Manager�� Server Manager ���ؼ� ����
- ��ġ �ɼǿ��� Windows Authentication�� �߰�

### ��ġ ���α׷�

- FileZilla
- Air Video Server HD
    - VLC
- [ServeToMe](https://www.zqueue.com/servetome/)
- iTunes
- [eMule](http://www.emule-project.net/home/perl/general.cgi?l=1&rm=download)
- uTorrent
- JRiver Media Center

