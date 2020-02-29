# Complete Clean

Visual Studio의 Clean은 Build Output만 제거하기 때문에 다른 파일들이 남을 수 있다.
필요한 경우 아래 PowerShell 스크립트로 bin, obj폴더를 지운다.

 > Get-ChildItem .\ -include bin,obj -Recurse | foreach ($_) { remove-item $_.fullname -Force -Recurse }