# GOAD FULL

1.Énumération

**<span style="color: #dddddd;">🖥️</span> NetExec**

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc smb 192.168.56.1/24                                       
SMB         192.168.56.23   445    BRAAVOS          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:BRAAVOS) (domain:essos.local) (signing:False) (SMBv1:True)
SMB         192.168.56.22   445    CASTELBLACK      [*] Windows 10 / Server 2019 Build 17763 x64 (name:CASTELBLACK) (domain:north.sevenkingdoms.local) (signing:False) (SMBv1:False)
SMB         192.168.56.12   445    MEEREEN          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:MEEREEN) (domain:essos.local) (signing:True) (SMBv1:True)
SMB         192.168.56.11   445    WINTERFELL       [*] Windows 10 / Server 2019 Build 17763 x64 (name:WINTERFELL) (domain:north.sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.10   445    KINGSLANDING     [*] Windows 10 / Server 2019 Build 17763 x64 (name:KINGSLANDING) (domain:sevenkingdoms.local) (signing:True) (SMBv1:False)
Running nxc against 5 targets ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 0:00:00

```

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc smb 192.168.56.1/24 --users
SMB         192.168.56.23   445    BRAAVOS          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:BRAAVOS) (domain:essos.local) (signing:False) (SMBv1:True)
SMB         192.168.56.12   445    MEEREEN          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:MEEREEN) (domain:essos.local) (signing:True) (SMBv1:True)
SMB         192.168.56.11   445    WINTERFELL       [*] Windows 10 / Server 2019 Build 17763 x64 (name:WINTERFELL) (domain:north.sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.10   445    KINGSLANDING     [*] Windows 10 / Server 2019 Build 17763 x64 (name:KINGSLANDING) (domain:sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.22   445    CASTELBLACK      [*] Windows 10 / Server 2019 Build 17763 x64 (name:CASTELBLACK) (domain:north.sevenkingdoms.local) (signing:False) (SMBv1:False)
SMB         192.168.56.11   445    WINTERFELL       -Username-                    -Last PW Set-       -BadPW- -Description-                                               
SMB         192.168.56.11   445    WINTERFELL       Guest                         <never>             0       Built-in account for guest access to the computer/domain 
SMB         192.168.56.11   445    WINTERFELL       arya.stark                    2025-07-22 13:55:28 0       Arya Stark 
SMB         192.168.56.11   445    WINTERFELL       sansa.stark                   2025-07-22 13:56:04 0       Sansa Stark 
SMB         192.168.56.11   445    WINTERFELL       brandon.stark                 2025-07-22 13:56:12 0       Brandon Stark 
SMB         192.168.56.11   445    WINTERFELL       rickon.stark                  2025-07-22 13:56:21 0       Rickon Stark 
SMB         192.168.56.11   445    WINTERFELL       hodor                         2025-07-22 13:56:30 0       Brainless Giant 
SMB         192.168.56.11   445    WINTERFELL       jon.snow                      2025-07-22 13:56:38 0       Jon Snow 
SMB         192.168.56.11   445    WINTERFELL       samwell.tarly                 2025-07-22 13:56:46 0       Samwell Tarly (Password : Heartsbane) 
SMB         192.168.56.11   445    WINTERFELL       jeor.mormont                  2025-07-22 13:56:54 0       Jeor Mormont 
SMB         192.168.56.11   445    WINTERFELL       sql_svc                       2025-07-22 13:57:02 0       sql service 
SMB         192.168.56.11   445    WINTERFELL       [*] Enumerated 10 local users: NORTH
Running nxc against 5 targets ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 100% 0:00:00

```
