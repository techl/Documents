# SharePoint Document Library에서 View in file explorer 사용하기

## 설정하기

```
REG ADD "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Edge" /v ConfigureViewInFileExplorer /t REG_SZ /d "[{\"cookies\": [\"rtFa\", \"FedAuth\"], \"domain\": \"emctkr.sharepoint.com\"}]"
```

## 적용된 내용 확인하기

edge://policy 에서 ConfigureViewInFileExplorer 확인하기

