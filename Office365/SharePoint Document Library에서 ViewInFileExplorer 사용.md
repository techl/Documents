# SharePoint Document Library에서 View in file explorer 사용하기

## 설정하기

```
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Edge" /v ConfigureViewInFileExplorer /t REG_SZ /d "[{\"cookies\": [\"rtFa\", \"FedAuth\"], \"domain\": \"emctkr.sharepoint.com\"}]"
```

## 적용된 내용 확인하기

edge://policy 에서 ConfigureViewInFileExplorer 확인하기

## Troubleshooting

### edge://policy 확인했을 때 The policy is blocked로 나오는 경우

AD Join되거나 Pro, Enterprise가 Device Management사용하는 경우만 활성화된다고 한다.

가짜로 이 환경을 구현하기 위해 아래 명령어를 cmd에서 관리자 권한으로 실행한다.

참고 : https://hitco.at/blog/apply-edge-policies-for-non-domain-joined-devices/

```
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Enrollments\FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF" /v EnrollmentState /t REG_DWORD /d 1
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Enrollments\FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF" /v EnrollmentType /t REG_DWORD /d 0
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Enrollments\FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF" /v IsFederated /t REG_DWORD /d 0
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Provisioning\OMADM\Accounts\FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF" /v Flags /t REG_DWORD /d 0x00d6fb7f
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Provisioning\OMADM\Accounts\FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF" /v AcctUId /t REG_SZ /d 0x000000000000000000000000000000000000000000000000000000000000000000000000 
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Provisioning\OMADM\Accounts\FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF" /v RoamingCount /t REG_DWORD /d 0
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Provisioning\OMADM\Accounts\FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF" /v SslClientCertReference /t REG_SZ /d MY;User;0000000000000000000000000000000000000000
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Provisioning\OMADM\Accounts\FFFFFFFF-FFFF-FFFF-FFFF-FFFFFFFFFFFF" /v ProtoVer /t REG_SZ /d 1.2
```

이후 Edge정책 설정을 위해 Edge Template을 다운받는다.

- https://www.microsoft.com/ko-kr/edge/business/download 에서 Windows 64비트 정책 다운로드

- MicrosoftEdgePolicyTemplates.cab파일 열어서 내부에 MicrosoftEdgePolicyTemplates.zip파일 열기

- windows/admx/msedge.admx파일과 en-US ko-KR폴더를 함께 C:\windows\PolicyDefinitions로 복사

gpedit.msc실행

Administrative Templates 하위에 Microsoft Edge보이는지 확인. 안보이면 위의 msedge.admx파일이 제대로 복사되지 않은 것임.

Microsoft Edge 노드 클릭 후 Configure the View in File Explorer feature for SharePoint pages in Microsoft Edge 더블클릭해서 Enabled 후 Options값에 다음 값을 넣음

```
[{"cookies": ["rtFa", "FedAuth"], "domain": "emctkr.sharepoint.com"}]
```

참고 : https://docs.microsoft.com/en-us/sharepoint/sharepoint-view-in-edge