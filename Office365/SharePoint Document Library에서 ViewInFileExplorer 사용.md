# SharePoint Document Library���� View in file explorer ����ϱ�

## �����ϱ�

```
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Edge" /v ConfigureViewInFileExplorer /t REG_SZ /d "[{\"cookies\": [\"rtFa\", \"FedAuth\"], \"domain\": \"emctkr.sharepoint.com\"}]"
```

## ����� ���� Ȯ���ϱ�

edge://policy ���� ConfigureViewInFileExplorer Ȯ���ϱ�

## Troubleshooting

### edge://policy Ȯ������ �� The policy is blocked�� ������ ���

AD Join�ǰų� Pro, Enterprise�� Device Management����ϴ� ��츸 Ȱ��ȭ�ȴٰ� �Ѵ�.

��¥�� �� ȯ���� �����ϱ� ���� �Ʒ� ��ɾ cmd���� ������ �������� �����Ѵ�.

���� : https://hitco.at/blog/apply-edge-policies-for-non-domain-joined-devices/

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

���� Edge��å ������ ���� Edge Template�� �ٿ�޴´�.

- https://www.microsoft.com/ko-kr/edge/business/download ���� Windows 64��Ʈ ��å �ٿ�ε�

- MicrosoftEdgePolicyTemplates.cab���� ��� ���ο� MicrosoftEdgePolicyTemplates.zip���� ����

- windows/admx/msedge.admx���ϰ� en-US ko-KR������ �Բ� C:\windows\PolicyDefinitions�� ����

gpedit.msc����

Administrative Templates ������ Microsoft Edge���̴��� Ȯ��. �Ⱥ��̸� ���� msedge.admx������ ����� ������� ���� ����.

Microsoft Edge ��� Ŭ�� �� Configure the View in File Explorer feature for SharePoint pages in Microsoft Edge ����Ŭ���ؼ� Enabled �� Options���� ���� ���� ����

```
[{"cookies": ["rtFa", "FedAuth"], "domain": "emctkr.sharepoint.com"}]
```

���� : https://docs.microsoft.com/en-us/sharepoint/sharepoint-view-in-edge