# Complete Clean

Visual Studio�� Clean�� Build Output�� �����ϱ� ������ �ٸ� ���ϵ��� ���� �� �ִ�.
�ʿ��� ��� �Ʒ� PowerShell ��ũ��Ʈ�� bin, obj������ �����.

 > Get-ChildItem .\ -include bin,obj -Recurse | foreach ($_) { remove-item $_.fullname -Force -Recurse }